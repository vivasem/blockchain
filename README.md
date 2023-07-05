1 A) Aim : A simple client class that generates the private and public keys by using the
built- in Python RSA algorithm and test it.
STEPS:
Setup the Environment Variable to appropriate path Install Pycryptodome using “pip intsall
pycryptodome”
#import libraries
import hashlib
import random
import string
import json
import binascii
import numpy as np
import pandas as pd
import pylab as pl
import logging
import datetime
import collections
# following imports are required by PKI
import Crypto
import Crypto.Random
from Crypto.Hash import SHA
from Crypto.PublicKey import RSA
from Crypto.Signature import PKCS1_v1_5
class Client:
def __init__(self):
random = Crypto.Random.new().read
self._private_key = RSA.generate(1024, random)
self._public_key = self._private_key.publickey()
self._signer = PKCS1_v1_5.new(self._private_key)
@property
def identity(self):
return binascii.hexlify(self._public_key.exportKey(format='DER')).decode('ascii')
Sana = Client()
print(Sana.identity)

1 B) A transaction class to send and receive money and test it.
Steps: Install “client” module
class Bank:
 def __init__(self):
 self.balance = 0
 print("sri \n")
 print("The account is created")
 def deposit(self):
 amount = float(input("Enter the amount to be deposit: "))
 self.balance = self.balance + amount
 print ("The deposit is successful and the balance in the account is Xf", self.balance)
 def withdraw(self):
 amount = float(input("Enter the amount to withdraw: "))
 if (self.balance >= amount):
 self.balance = self.balance - amount
 print ("The withdraw is successful and the balance is xf", self.balance)
 else:
 print("Insuficient Balance")
 def enquiry(self):
 print ("Balance in the account is 3f",self.balance)
acc = Bank()
acc.deposit()
acc.withdraw()
acc.enquiry()

OR

import hashlib
import random
import string
import json
import binascii
import numpy as np
import pandas as pd
import pylab as pl
import logging
import datetime
import collections
import Crypto
import Crypto.Random
from Crypto.Hash import SHA
from Crypto.PublicKey import RSA
from Crypto.Signature import PKCS1_v1_5
class Client:
def __init__(self):
random = Crypto.Random.new().read
self._private_key = RSA.generate(1024, random)
self._public_key = self._private_key.publickey()
self._signer = PKCS1_v1_5.new(self._private_key)
@property
def identity(self):
return binascii.hexlify(self._public_key.exportKey(format='DER')).decode('ascii')
class Transaction:
def __init__(self, sender, recipient, value):
self.sender = sender
self.recipient = recipient
self.value = value
self.time = datetime.datetime.now()
def to_dict(self):
if self.sender == "Genesis":
identity = "Genesis"
else:
identity = self.sender.identity
return collections.OrderedDict({
'sender': identity,
'recipient': self.recipient,
'value': self.value,
'time' : self.time})
def sign_transaction(self):
private_key = self.sender._private_key
signer = PKCS1_v1_5.new(private_key)
h = SHA.new(str(self.to_dict()).encode('utf8'))
return binascii.hexlify(signer.sign(h)).decode('ascii')
Sana = Client()
Sarah = Client()
t = Transaction(
Sana,
Sarah.identity,
5.0
)
signature = t.sign_transaction()
print (signature)

1 C) Create multiple transactions and display them.
from client import client
from transaction_class import transaction
Dinesh = client()
Ramesh = client()
t = Transaction(Dinesh, Ramesh.identity, 5.0)
print("\nTransaction Recipient:\n", t.recipient)
# print("\nTransaction Sender:\n", t.sender)
print("\nTransaction Value:\n", t.value)
signature = t.sign_transaction()
print("\nSignature:\n", signature)
Dinesh = Client()
Ramesh = Client()
Seema = Client()
Vijay = Client()
t1 = Transaction(Dinesh, Ramesh.identity, 15.0)
t1.sign_transaction()
transactions = [t1]
t2 = Transaction(Dinesh, Seema.identity, 6.0)
t2.sign_transaction()
transactions.append(t2)
t3 = Transaction(Ramesh, Vijay.identity, 2.0)
t3.sign_transaction()
transactions.append(t3)
t4 = Transaction(Seema, Ramesh.identity, 4.0)
t4.sign_transaction()
transactions.append(t4)
for transaction in transactions:
 Transaction.display_transaction(transaction)
 print("--------------")
 
OR

import hashlib
import random
import string
import json
import binascii
import numpy as np
import pandas as pd
import pylab as pl
import logging
import datetime
import collections
import Crypto
import Crypto.Random
from Crypto.Hash import SHA
from Crypto.PublicKey import RSA
from Crypto.Signature import PKCS1_v1_5
class Client:
def __init__(self):
random = Crypto.Random.new().read
self._private_key = RSA.generate(1024, random)
self._public_key = self._private_key.publickey()
self._signer = PKCS1_v1_5.new(self._private_key)
@property
def identity(self):
return binascii.hexlify(self._public_key.exportKey(format='DER')).decode('ascii')
class Transaction:
def __init__( self, sender, recipient, value ):
self.sender = sender
self.recipient = recipient
self.value = value
self.time = datetime.datetime.now()
def to_dict( self ):
if self.sender == "Genesis":
identity = "Genesis"
else:
identity = self.sender.identity
return collections.OrderedDict( {
'sender': identity,
'recipient': self.recipient,
'value': self.value,
'time' : self.time } )
def sign_transaction( self ):
private_key = self.sender._private_key
signer = PKCS1_v1_5.new(private_key)
h = SHA.new(str(self.to_dict()).encode('utf8'))
return binascii.hexlify(signer.sign(h)).decode('ascii')
def display_transaction(transaction):
#for transaction in transactions:
dict = transaction.to_dict()
print ("sender: " + dict['sender'])
print ('-----')
print ("recipient: " + dict['recipient'])
print ('-----')
print ("value: " + str(dict['value']))
print ('-----')
print ("time: " + str(dict['time']))
print ('-----')
transactions = []
Dinesh = Client()
Ramesh = Client()
Seema = Client()
Vijay = Client()
t1 = Transaction(
Dinesh,
Ramesh.identity,
15.0 )
t1.sign_transaction()
transactions.append(t1)
t2 = Transaction(
Dinesh,
Seema.identity,
6.0 )
t2.sign_transaction()
transactions.append(t2)
t3 = Transaction(
Ramesh,
Vijay.identity,
2.0 )
t3.sign_transaction()
transactions.append(t3)
t4 = Transaction(
Seema,
Ramesh.identity,
4.0 )
t4.sign_transaction()
transactions.append(t4)
t5 = Transaction(
Vijay,
Seema.identity,
7.0 )
t5.sign_transaction()
transactions.append(t5)
t6 = Transaction(
Ramesh,
Seema.identity,
3.0 )
t6.sign_transaction()
transactions.append(t6)
t7 = Transaction(
Seema,
Dinesh.identity,
8.0 )
t7.sign_transaction()
transactions.append(t7)
t8 = Transaction(
Seema,
Ramesh.identity,
1.0 )
t8.sign_transaction()
transactions.append(t8)
t9 = Transaction(
Vijay,
Dinesh.identity,
5.0 )t9.sign_transaction()
transactions.append(t9)
t10 = Transaction(
Vijay,
Ramesh.identity,
3.0 )
t10.sign_transaction()
transactions.append(t10)
for transaction in transactions:
display_transaction (transaction)
print ('--------------')

1 D) Create a blockchain, a genesis block and execute it.
from client import Client
from transaction_class import Transaction
class Block:
 def __init__(self, client):
self.verified_transactions = []
self.previous_block_hash = ""
self.Nonce = ""
self.client = client
def dump_blockchain(blocks):
 print(f"\nNumber of blocks in the chain: {len(blocks)}")
 for i, block in enumerate(blocks):
print(f"block # {i}")
 for transaction in block.verified_transactions:
Transaction.display_transaction(transaction)
print("--------------")
print("=====================================")
Dinesh = Client()
t0 = Transaction("Genesis", Dinesh.identity(), 500.0)
block0 = Block(Dinesh)
block0.previous_block_hash = ""
NONCE = None
block0.verified_transactions.append(t0)
digest = hash(block0)
last_block_hash = digest
TPCoins = [block0]
dump_blockchain(TPCoins)

OR

import hashlib
import random
import string
import json
import binascii
import numpy as np
import pandas as pd
import pylab as pl
import logging
import datetime
import collections
import Crypto
import Crypto.Random
from Crypto.Hash import SHA
from Crypto.PublicKey import RSA
from Crypto.Signature import PKCS1_v1_5
class Client:
def __init__(self):
random = Crypto.Random.new().read
self._private_key = RSA.generate(1024, random)
self._public_key = self._private_key.publickey()
self._signer = PKCS1_v1_5.new(self._private_key)
@property
def identity(self):
return binascii.hexlify(self._public_key.exportKey(format='DER')).decode('ascii')
class Transaction:
def __init__( self, sender, recipient, value ):
self.sender = sender
self.recipient = recipient
self.value = value
self.time = datetime.datetime.now()
def to_dict( self ):
if self.sender == "Genesis":
identity = "Genesis"
else:
identity = self.sender.identity
return collections.OrderedDict( {
'sender': identity,
'recipient': self.recipient,
'value': self.value,
'time' : self.time } )
def sign_transaction( self ):
private_key = self.sender._private_key
signer = PKCS1_v1_5.new(private_key)
h = SHA.new(str(self.to_dict()).encode('utf8'))
return binascii.hexlify(signer.sign(h)).decode('ascii')
def display_transaction(transaction):
#for transaction in transactions:
dict = transaction.to_dict()
print ("sender: " + dict['sender'])
print ('-----')
print ("recipient: " + dict['recipient'])
print ('-----')
print ("value: " + str(dict['value']))
print ('-----')
print ("time: " + str(dict['time']))
print ('-----')
class Block:
def __init__(self):
self.verified_transactions = []
self.previous_block_hash = ""
self.Nonce = ""
last_block_hash = ""
def dump_blockchain (self):
print ("Number of blocks in the chain: " + str(len (self)))
for x in range (len(TPCoins)):
block_temp = TPCoins[x]
print ("block # " + str(x))
for transaction in block_temp.verified_transactions:
display_transaction (transaction)
print ('--------------')
print ('=====================================')
Dinesh = Client()
t0 = Transaction (
"Genesis",
Dinesh.identity,
500.0
)
block0 = Block()
block0.previous_block_hash = None
Nonce = None
block0.verified_transactions.append (t0)
digest = hash (block0)
last_block_hash = digest
TPCoins = []
TPCoins.append (block0)
dump_blockchain(TPCoins)

1 E) Create a mining function and test it.
import hashlib
def sha256(message):
 return hashlib.sha256(message.encode("ascii")).hexdigest()
def mine(message, difficulty=1):
assert difficulty = 1
prefix = "1" * difficulty
for i in range(1000):
digest = sha256(str(hash(message)) + str(i))
If digest.startswith(prefix):
print(f"after {str(i)} iterations found nonce: {digest}")
# return print(digest)
mine("test message", 2)

OR

import hashlib
import random
import string
import json
import binascii
import numpy as np
import pandas as pd
import pylab as pl
import logging
import datetime
import collections

import Crypto
import Crypto.Random
from Crypto.Hash import SHA
from Crypto.PublicKey import RSA
from Crypto.Signature import PKCS1_v1_5
def sha256(message):
return hashlib.sha256(message.encode('ascii')).hexdigest()
def mine(message, difficulty=1):
assert difficulty >= 1
prefix = '1' * difficulty
for i in range(1000):
digest = sha256(str(hash(message)) + str(i))
if digest.startswith(prefix):
print ("after " + str(i) + " iterations found nonce: "+ digest)
return digest
mine ("test message", 2)

1 F) Add blocks to the miner and dump the blockchain.
import datetime
import hashlib
# Create a class with two functions
class Block:
 def __init__(self, data, previous_hash):
self.timestamp = datetime.datetime.now(datetime.timezone.utc)
self.data = data
self.previous_hash = previous_hash
self.hash = self.calc_hash()
 def calc_hash(self):
sha = hashlib.sha256()
hash_str = self.data.encode("utf-8")
sha.update(hash_str)
return sha.hexdigest()
# Instantiate the class
blockchain = [Block("First block", "0")]
blockchain.append(Block("Second block", blockchain[0].hash))
blockchain.append(Block("Third block", blockchain[1].hash))
# Dumping the blockchain
for block in blockchain:
print(f"Timestamp: {block.timestamp}\nData: {block.data}\nPrevious
Hash:{block.previous_hash}\nHash: {block.hash}\n")

2 Install and configure Go Ethereum and the Mist browser. Develop and test a
sample application.(MetaMask & Remix)

Step 1 -> Install MetaMask extension for chrome from Chrome Web Store

Step 2-> Click on Metamask Extension in Extensions. Below page will open in a
new tab. Click on Create a New Wallet. Click on I agree.

Step 3-> Create a password. This password can be used only on the device it
was created on. Create a Strong password and click on Create a new Wallet
button

Step 4-> Click on Secure my wallet button, following window will appear

Step 5-> Click on Reveal Secret Recovery Phrase button and save the words in
the same sequence

Step 6-> Enter the respective words in the empty positions and click Confirm.

Step 7-> Click Got it!
Step 8-> Click on Next
Step 9-> Following will be the Dashboard (Dashboard will be appear)
Step 10-> Click on Ethereum Mainnet button. Next click on Show/hide test
networks
Step 11-> Check if tesnets are shown by clicking on Etherum Mainnet button. Click
on Sepolia test network.
Step 12-> Go to https://sepoliafaucet.com/ and Click on Alchemy Login button.
Step 13-> Login to a gmail account in another browser tab and click on Sign in with
Google
Step 14-> Now go to MetaMask and copy the account address.
Step 15-> Paste the address and click on Send Me ETH
Step 16-> Your ETH transfer is succesfull. You should see a similar animation
Step 17-> Check your MetaMask account for Sepolia test network. 0.5 ETH will be
added.

OR

Installing GETH (Go Ethereum)
Step 1: Go to website https://geth.ethereum.org/downloads/
Step 2: From stable releases Geth 1.5.8 (kind = installer)
Step 3: once downloaded run it then click next
Step 4: Select Geth and Development tools click next
Step 5: Select location to install click next
Step 6: Once Installation is finished Click Close and its done
Installing Mist Browser
Step 1: https://github.com/ethereum/mist/releases
Step 2: Under Ethereum Wallet and Mist 0.8.9 - "The Wizard" download mist-installer-0-8-
9.exe
Step 3: For installation click, I agree -> next -> install
Run Mist
Step 1: Open the Mist from the start menu
Step 2: It will start downloading Blockchain data once you open it
Step 3: Once it finishes downloading it is ready to use

Run Geth
Step 1: Open CMD
Step 2: Type GETH and press enter
Step 3: After it finishes loading press ctrl+c to exit the process.
Step 4: Now it's ready to use


3 Implement and demonstrate the use of the following in solidity
STEPS:
1. To execute solidity scripts go to ->https://remix.ethereum.org/
2. Open contracts folder and starting writing scripts. The scripts are compiled using solidity compiler.
3. The following scripts were compiled using 0.5.0+commit.1d4f565a solidity compiler
4. Deploy the scripts to execute code

A) Aim : Variable, Operators, Loops, Decision Making, Strings, Arrays, Enums, Structs,
Mappings, Conversions, Ether Units, Special Variables
1. Variables
pragma solidity ^0.5.0;
contract variable_demo {
uint256 sum = 4; //state variable
uint256 x;
address a;
string s = "welcome";
function add(uint256) public {
uint256 y = 2; //local variable sum = sum+x+y:
sum = sum + x + y;
}
function display() public view returns (uint256) {
return sum;
}
function displayMsg() public view returns (string memory) {
return s;
 }
}

OR

// Solidity program to demonstrate state variables
pragma solidity ^0.5.0;
// Creating a contract
contract Solidity_var_Test {
// Declaring a state variable
uint8 public state_var;
// Defining a constructor
constructor() public {
state_var = 16;
}
}

2. Strings
pragma solidity ^0.5.0;
contract LearningStrings {
string text;
 function getText() public view returns (string memory) {
return text;
}
 function setText() public {
 text = "hello";
 }
 function setTextByPassing(string memory message) public {
text = message;
 }
} 

OR

pragma solidity ^0.5.0;
contract SolidityTest {
constructor() public{
}
function getResult() public view returns(string memory){
uint a = 1;
uint b = 2;
uint result = a + b;
return integerToString(result);
}
function integerToString(uint _i) internal pure
returns (string memory) {
if (_i == 0) {
return "0";
}
uint j = _i;
uint len;
while (j != 0) {
len++;
j /= 10;
}
bytes memory bstr = new bytes(len);
uint k = len - 1;
while (_i != 0) {
bstr[k--] = byte(uint8(48 + _i % 10));
_i /= 10;
}
return string(bstr);
}
}

3. Operators
pragma solidity ^0.5.0;
contract SolidityTest {
uint16 public a = 20;
uint16 public b = 10;
uint256 public sum = a + b;
uint256 public diff = a - b;
uint256 public mul = a * b;
uint256 public div = a / b;
uint256 public mod = a % b;
uint256 public dec = --b;
uint256 public inc = ++a;
}

OR

a. Arithmetic Operator
Code:
// Solidity contract to demonstrate
// Arithmetic Operator
pragma solidity ^0.5.0;
// Creating a contract
contract SolidityTest {
// Initializing variables
uint16 public a = 20;
uint16 public b = 10;
// Initializing a variable
// with sum
uint public sum = a + b;
// Initializing a variable
// with the difference
uint public diff = a - b;
// Initializing a variable
// with product
uint public mul = a * b;
// Initializing a variable
// with quotient
uint public div = a / b;
// Initializing a variable
// with modulus
uint public mod = a % b;
// Initializing a variable
// decrement value
uint public dec = --b;
// Initializing a variable
// with increment value
uint public inc = ++a;
}

b. Relational Operator
Code:
// Solidity program to demonstrate
// Relational Operator
pragma solidity ^0.5.0;
// Creating a contract
contract SolidityTest {
// Declaring variables
uint16 public a = 20;
uint16 public b = 10;
// Initializing a variable
// with bool equal result
bool public eq = a == b;
// Initializing a variable
// with bool not equal result
bool public noteq = a != b;
// Initializing a variable
// with bool greater than result
bool public gtr = a > b;
// Initializing a variable
// with bool less than result
bool public les = a < b;
// Initializing a variable
// with bool greater than equal to result
bool public gtreq = a >= b;
// Initializing a variable
// bool less than equal to result
bool public leseq = a <= b;
}

c. Logical Operator
Code:
// Solidity program to demonstrate
// Logical Operators
pragma solidity ^0.5.0;
// Creating a contract
contract logicalOperator{
// Defining function to demonstrate
// Logical operator
function Logic(
bool a, bool b) public view returns(
bool, bool, bool){
// Logical AND operator
bool and = a&&b;
// Logical OR operator
bool or = a||b;
// Logical NOT operator
bool not = !a;
return (and, or, not);
}
}

d. Bitwise Operator.
Code:
// Solidity program to demonstrate
// Bitwise Operator
pragma solidity ^0.5.0;
// Creating a contract
contract SolidityTest {
// Declaring variables
uint16 public a = 20;
uint16 public b = 10;
// Initializing a variable
// to '&' value
uint16 public and = a & b;
// Initializing a variable
// to '|' value
uint16 public or = a | b;
// Initializing a variable
// to '^' value
uint16 public xor = a ^ b;
// Initializing a variable
// to '<<' value
uint16 public leftshift = a << b;
// Initializing a variable
// to '>>' value
uint16 public rightshift = a >> b;
// Initializing a variable
// to '~' value
uint16 public not = ~a ;
}

e. Assignment Operator.
Code:
// Solidity program to demonstrate
// Assignment Operator
pragma solidity ^0.5.0;
// Creating a contract
contract SolidityTest {

// Declaring variables
uint16 public assignment = 20;
uint public assignment_add = 50;
uint public assign_sub = 50;
uint public assign_mul = 10;
uint public assign_div = 50;
uint public assign_mod = 32;
// Defining function to
// demonstrate Assignment Operator
function getResult() public{
assignment_add += 10;
assign_sub -= 20;
assign_mul *= 10;
assign_div /= 10;
assign_mod %= 20;
return ;
}

}

f. Conditional Operator.
Code:
// Solidity program to demonstrate
// Conditional Operator
pragma solidity ^0.5.0;
// Creating a contract
contract SolidityTest{
// Defining function to demonstrate
// conditional operator
function sub(
uint a, uint b) public view returns(
uint){
uint result = (a > b? a-b : b-a);
return result;
}
}


4. Array
pragma solidity ^0.5.0;
contract arraydemo
{
 //Static Array
 uint[6] arr2=[10,20,30];
 function dispstaticarray() public view returns(uint[6] memory)
 {
 return arr2;
 }
//Dynamic Array
uint x=5;
uint [] arr1;
function arrayDemo() public
{
while(x>0)
{
arr1.push(x);
 x=x-1;
}
}
function dispdynamicarray() public view returns(uint[] memory)
 {
 return arr1;
 }
}

OR

Arrays
Code:
// Solidity program to demonstrate
// creating a fixed-size array
pragma solidity ^0.5.0;
// Creating a contract
contract Types {
// Declaring state variables
// of type array
uint[6] data1;
// Defining function to add
// values to an array
function array_example() public returns (
int[5] memory, uint[6] memory){
int[5] memory data
= [int(50), -63, 77, -28, 90];
data1
= [uint(10), 20, 30, 40, 50, 60];
return (data, data1);
}
}

5. Decision Making
If else statement
Code:
pragma solidity ^0.5.0;
contract SolidityTest {
uint storedData;
constructor() public{
storedData = 10;
}
function getResult() public view returns(string memory){
uint a = 1;
uint b = 2;
uint result;
if( a > b) { // if else statement
result = a;
}
else {
result = b;
}
return integerToString(result);
}
function integerToString(uint _i) internal pure
returns (string memory) {
if (_i == 0) {
return "0";
}
uint j = _i;
uint len;

while (j != 0) {
len++;
j /= 10;
}
bytes memory bstr = new bytes(len);
uint k = len - 1;

while (_i != 0) {
bstr[k--] = byte(uint8(48 + _i % 10));
_i /= 10;
}
return string(bstr);//access local variable
}
}

If Statement
Code:
pragma solidity ^0.5.0;
contract SolidityTest {
uint storedData;
constructor() public {
storedData = 10;
}
function getResult() public view returns(string memory){
uint a = 1;
uint b = 2;
uint result = a + b;
return integerToString(result);
}
function integerToString(uint _i) internal pure
returns (string memory) {
if (_i == 0) { // if statement
return "0";
}
uint j = _i;
uint len;
while (j != 0) {
len++;
j /= 10;
}
bytes memory bstr = new bytes(len);
uint k = len - 1;
while (_i != 0) {
bstr[k--] = byte(uint8(48 + _i % 10));
_i /= 10;
}
return string(bstr);//access local variable
}
}

If-else-If statement
Code:
pragma solidity ^0.5.0;
contract SolidityTest {
uint storedData; // State variable
constructor() public {
storedData = 10;
}
function getResult() public view returns(string memory) {
uint a = 1;
uint b = 2;
uint c = 3;
uint result

if( a > b && a > c) { // if else statement
result = a;
} else if( b > a && b > c ){
result = b;
} else {
result = c;
}
return integerToString(result);
}
function integerToString(uint _i) internal pure
returns (string memory) {

if (_i == 0) {
return "0";
}
uint j = _i;
uint len;

while (j != 0) {
len++;
j /= 10;
}
bytes memory bstr = new bytes(len);
uint k = len - 1;

while (_i != 0) {
bstr[k--] = byte(uint8(48 + _i % 10));
_i /= 10;
}
return string(bstr);//access local variable
}
}

6. Loops
For Loop
// Solidity program to
// demonstrate the use
// of 'For loop'
pragma solidity ^0.5.0;
// Creating a contract
contract Types {
// Declaring a dynamic array
uint[] data;
// Defining a function
// to demonstrate 'For loop'
function loop(
) public returns(uint[] memory){
for(uint i=0; i<5; i++){
data.push(i);
}
return data;
}
}

While Loop
// Solidity program to
// demonstrate the use
// of 'While loop'
pragma solidity ^0.5.0;
// Creating a contract
contract Types {
// Declaring a dynamic array
uint[] data;
// Declaring state variable
uint8 j = 0;
// Defining a function to
// demonstrate While loop'
function loop(
) public returns(uint[] memory){
while(j < 5) {
j++;
data.push(j);
}
return data;
}
}

Do While
// Solidity program to
// demonstrate the use of
// 'Do-While loop'
pragma solidity ^0.5.0;
// Creating a contract
contract Types {
// Declaring a dynamic array
uint[] data;
// Declaring state variable
uint8 j = 0;
// Defining function to demonstrate
// 'Do-While loop'
function loop(
) public returns(uint[] memory){
do{
j++;
data.push(j);
}while(j < 5) ;
return data;
}
}

7. Enums
pragma solidity ^0.5.0;
contract enumdemo {
 enum week_days {
Monday,
Tuesday,
Wednesday,
Thursday,
Friday,
Saturday,
Sunday
}
week_days week;
week_days choice;
week_days constant default_value = week_days.Sunday;
function set_value() public {
choice = week_days.Tuesday;
}
function get_choice() public view returns (week_days) {
return choice;
}
function get_defaultvalue() public view returns (week_days) {
return default_value;
 }
}

OR 

Enums
Code:
pragma solidity ^0.5.0;
contract test {
enum FreshJuiceSize{ SMALL, MEDIUM, LARGE }
FreshJuiceSize choice;
FreshJuiceSize constant defaultChoice = FreshJuiceSize.MEDIUM;
function setLarge() public {
choice = FreshJuiceSize.LARGE;
}
function getChoice() public view returns (FreshJuiceSize) {
return choice;
}
function getDefaultChoice() public pure returns (uint) {
return uint(defaultChoice);
}
}

8. Structs
pragma solidity ^0.5.0;
contract structdemo {
 struct Book {
string name;
string author;
uint256 id;
bool availability;
}
Book book2;
Book book1 = Book("A Little Life", "Hanya Yanagihara", 2, false);
function set_details() public {
book2 = Book("Almond", "Sohn won-pyung", 1, true);
}
function book_info()
 public
 view
 returns (
string memory,
string memory,
uint256,
bool
 )
{
return (book1.name, book1.author, book1.id, book1.availability);
}
function get_details()
public
view
returns (
string memory, string memory, uint256, bool
)
{
return (book2.name, book2.author, book2.id, book2.availability);
 }
}

OR 

Structs
Code:
pragma solidity ^0.5.0;
contract test {
struct Book {
string title;
string author;
uint book_id;
}
Book book;
function setBook() public {
book = Book('Learn Java', 'TP', 1);
}
function getBookId() public view returns (uint) {
return book.book_id;
}
}

9. Mappings
pragma solidity ^0.5.0;
contract LedgerBalance {
 mapping(address => uint256) public balances;
 function updateBalance(uint256 newBalance) public {
 balances[msg.sender] = newBalance;
 }
}
contract Updater {
 function updateBalance() public returns (uint256) {
LedgerBalance ledgerBalance = new LedgerBalance();
ledgerBalance.updateBalance(10);
return ledgerBalance.balances(address(this));
 }
}

10. Conversions
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
contract ImplicitConversion {
 function add() public pure returns (uint256) {
 uint256 a = 10;
 uint256 b = 20;
return a + b;
 }
}
contract ExplicitConversion {
function convert() public pure returns (bytes memory) {
string memory str = "Hello World";
bytes memory b = bytes(str);
return b;
 }
}
Steps:
1) Deploy both contracts
2) Open Implicit Conversion and click on add button to sum and display
3) Value
4) Open Explicit Conversion and click on convert button

11. Ether Units
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
 contract SolidityTest {
function convert_Amount_to_Wei(uint256 Amount)
public
pure
returns (uint256)
{
return Amount * 1 wei;
 }
function convert_Amount_To_Ether(uint256 Amount)
public
pure
returns (uint256)
{
return Amount * 1 ether;
}
function convert_Amount_To_Gwei(uint256 Amount)
public
pure
returns (uint256)
{
return Amount * 1 gwei;
}
function convert_seconds_To_mins(uint256 _seconds)
public
pure
returns (uint256)
{
return _seconds / 60;
}
function convert_seconds_To_Hours(uint256 _seconds)
public
pure
returns (uint256)
{
return _seconds / 3600;
}
function convert_Mins_To_Seconds(uint256 _mins)
public
pure
returns (uint256)
{
return _mins * 60;
}
}

12. Special Variables
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
contract Special_Variables {
 mapping(address => uint256) rollNo;
function setRollNO(uint256 _myNumber) public {
 rollNo[msg.sender] = _myNumber;
}
 function whatIsMyRollNumber() public view returns (uint256) {
return rollNo[msg.sender];
}
}
STEPS :
1) Deploy contract Special Variables
2) Input a number for setRollNO function and click on it & whatIsMyRollNumber button

3 B) Aim : Functions, Function Modifiers, View functions, Pure Functions, Fallback
Function, Function Overloading, Mathematical functions, Cryptographic functions
1. View Functions
pragma solidity ^0.8.18;
contract view_demo {
uint256 num1 = 2;
uint256 num2 = 4;
 function getResult() public view returns (uint256 product, uint256 sum) {
product = num1 * num2;
 sum = num1 + num2;
 }
} 

OR 

View Funciton
Code:
pragma solidity ^0.5.0;
contract Test {
function getResult() public view returns(uint product, uint sum){
uint a = 1; // local variable
uint b = 2;
product = a * b;
sum = a + b;
}
}

Functions
Code:
pragma solidity ^0.5.0;
contract SolidityTest {
constructor() public{
}
function getResult() public view returns(string memory){
uint a = 1;
uint b = 2;
uint result = a + b;
return integerToString(result);
}
function integerToString(uint _i) internal pure
returns (string memory) {
if (_i == 0) {
return "0";
}
uint j = _i;
uint len;
while (j != 0) {
len++;
j /= 10;
}
bytes memory bstr = new bytes(len);
uint k = len - 1;
while (_i != 0) {
bstr[k--] = byte(uint8(48 + _i % 10));
_i /= 10;
}
return string(bstr);//access local variable
}
}

2. Pure Functions
pragma solidity ^0.8.18;
contract pure_demo {
function getResult() public pure returns (uint256 product, uint256 sum) {
uint256 num1 = 2;
uint256 num2 = 4;
product = num1 * num2;
 sum = num1 + num2;
 }
}

OR

Pure Function
Code:
pragma solidity ^0.5.0;
contract Test {
function getResult() public pure returns(uint product, uint sum){
uint a = 10;
uint b = 2;
product = a * b;
sum = a + b;
}
string public str = "Pure Function Test";
}

3. Mathematical Functions
pragma solidity ^0.8.18; contract Test{
 function CallAddMod() public pure returns(uint){
return addmod(7,3,3);
}
 function CallMulMod() public pure returns(uint){
return mulmod(7,3,3);
 }
} 

4. Cryptographic Functions
pragma solidity ^0.8.18; contract Test{
 function callKeccak256() public pure returns(bytes32 result){
return keccak256("BLOCKCHAIN");
 }
 function callsha256() public pure returns(bytes32 result){
return sha256("BLOCKCHAIN");
 }
 function callripemd() public pure returns (bytes20 result){
return ripemd160("BLOCKCHAIN");
 }
} 

5. Functions
pragma solidity >=0.4.22 <0.9.0;
contract Test {
 function return_example()
public
pure
returns (
uint256,
uint256,
uint256,
 string memory
)
{
uint256 num1 = 10;
uint256 num2 = 16;
uint256 sum = num1 + num2;
uint256 prod = num1 * num2;
uint256 diff = num2 - num1;
string memory message = "Multiple return values";
return (sum, prod, diff, message);
}
}

6. Fallback Function
pragma solidity ^0.5.12;
contract A {
 uint256 n;
 function set(uint256 value) external {
 n = value;
 }
function() external payable {
 n = 0;
 }
}
contract example {
function callA(A a) public returns (bool) {
(bool success, ) = address(a).call(abi.encodeWithSignature("setter()"));
require(success);
address payable payableA = address(uint160(address(a)));
return (payableA.send(2 ether));
}
}
Output :
Provide values to both deployed contracts accordingly(use any address)

OR

Fallback Function:
Code:
pragma solidity ^0.5.0;
contract Test {
uint public x ;
function() external { x = 1; }
}
contract Sink {
function() external payable { }
}
contract Caller {
function callTest(Test test) public returns (bool) {
(bool success,) = address(test).call(abi.encodeWithSignature("nonExistingFunction()"));
require(success);
// test.x is now 1
address payable testPayable = address(uint160(address(test)));
// Sending ether to Test contract,
// the transfer will fail, i.e. this returns false here.
return (testPayable.send(2 ether));
}
function callSink(Sink sink) public returns (bool) {
address payable sinkPayable = address(sink);
return (sinkPayable.send(2 ether));
}
string public str = "Function Callback successfully executed!";
}

7. Function Overloading
pragma solidity ^0.8.0;
contract OverloadingExample {
function add(uint256 a, uint256 b) public pure returns (uint256) {
return a + b;
}
function add(string memory a, string
memory b)public
pure
returns (string memory)
{
return string(abi.encodePacked(a, b));
}
}
Output :
Steps:
1) Deploy Overloading Example contract
2) Give integer and string values to both add functions as below 

OR

Function Overloading:
Code:
pragma solidity ^0.5.0;
contract Test {
string public str="Program ran successfully :)";
function getSum(uint a, uint b) public pure returns(uint){
return a + b;
}
function getSum(uint a, uint b, uint c) public pure returns(uint){
return a + b + c;
}
function callSumWithTwoArguments() public pure returns(uint){
return getSum(1,2);
}
function callSumWithThreeArguments() public pure returns(uint){
return getSum(1,2,3);
}
}


8. Function modifiers
pragma solidity ^0.5.0;
contract ExampleContract {
address public owner =
0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;uint256 public
counter;
modifier onlyowner() {
require(msg.sender == owner, "Only the contract owner can call");
_;
}
function incrementcounter() public
onlyowner {counter++;
}
}
Output :
Steps
1) Click on owner button
2) Click on counter button initially it is 0. 
3) Then click on increment counter button and again click on counter button, the counter
has been increased. 

Function Modifiers
Code:
pragma solidity ^0.5.0;
contract Owner {
address owner;
string public str = "Function Modifiers Example";
constructor() public {
owner = msg.sender;
}
modifier onlyOwner {
require(msg.sender == owner);
_;
}
modifier costs(uint price) {
if (msg.value >= price) {
_;
}
}
}
contract Register is Owner {
mapping (address => bool) registeredAddresses;
uint price;
constructor(uint initialPrice) public { price = initialPrice; }
function register() public payable costs(price) {
registeredAddresses[msg.sender] = true;
}
function changePrice(uint _price) public onlyOwner {
price = _price;
}
}

Mathematical Functions:
Code:
pragma solidity ^0.5.0;
contract Test {
string public disp="Running Mathematical Function";
function callAddMod() public pure returns(uint){
return addmod(4, 5, 3);
}
function callMulMod() public pure returns(uint){
return mulmod(4, 5, 3);
}
}

Cryptographic Functions:
Code:
pragma solidity ^0.5.0;
contract Test {
function callKeccak256() public pure returns(bytes32 result){
return keccak256("ABC");
}
}

4 Implement and demonstrate the use of the following in Solidity
A) Aim : Withdrawal Pattern, Restricted Access
1. Withdrawal Pattern
pragma solidity 0.8.18;
contract
WithdrawalPat
tern {address
public owner;
uint256 public lockedbalance;
uint256 public withdrawablebalance;
constructor() {
owner = msg.sender;
}
modifier onlyowner() {
require(msg.sender == owner, "Only the owner can call this function");
_;
}
function deposit(uint256 amount) public payable {
require(amount > 0, "Amount must be greater than
zero");lockedbalance += amount;
}
function withdraw(uint256 amount) public payable onlyowner
{require(
amount <= withdrawablebalance,
"Insufficient withdrawable balance"
);
withdrawablebalance -= amount;
payable(msg.sender).transfer(amount);
}
function unlock(uint256 amount) public onlyowner {
require(amount <= lockedbalance, "Insufficient locked balance");
lockedbalance -= amount;
withdrawablebalance += amount;
}
}
Steps:
Click on owner
Enter an amount and click on deposit 
Click on locked balance button to display the locked amount in the account 
Click on withdrawable balance button
Click on unlock button and enter any amount to transfer amount to withdrawable balance. Check
locked balance and withdrawable balance. 
Enter any amount you want to withdraw and click the withdraw button. You should get an error
and the transaction should be reverted. 

2. Restricted Access
pragma solidity ^0.8.18;
contract RestrictedAccess {
address public owner = msg.sender;
uint256 public creationTime = block.timestamp;
modifier onlyBy(address _account) {
require(msg.sender == _account, "Sender not authorized!");
_;
}
modifier onlyAfter(uint256 _time) {
require(block.timestamp >= _time, "Function was called too early!");
_;
}
modifier costs(uint256 _amount) {
require(msg.value >= _amount, "Not enough Ether provided!");
_;
}
function forceOwnerChange(address
_newOwner)public
payable
costs(200 ether)
{
owner = _newOwner;
}
function changeOwner(address _owner) public
onlyBy(owner) {owner = _owner;
}
function disown() public onlyBy(owner) onlyAfter(creationTime + 3 weeks) {
delete owner;
}
}

B) Aim: Contracts, Inheritance, Constructors, Abstract Contracts, Interfaces
1. Contracts
pragma solidity ^0.5.0;
contract Contract_demo {
string message = "Hello";
function dispMsg() public view returns (string memory)
{
return message;
}
}

OR

Contracts:
Code:
pragma solidity ^0.5.0;
contract C {
//private state variable
uint private data;
//public state variable
uint public info;
//constructor
constructor() public {
info = 10;
}
//private function
function increment(uint a) private pure returns(uint) { return a + 1; }
//public function
function updateData(uint a) public { data = a; }
function getData() public view returns(uint) { return data; }
function compute(uint a, uint b) internal pure returns (uint) { return a + b; }
}
//External Contract
contract D {
function readData() public returns(uint) {
C c = new C();
c.updateData(7);
return c.getData();
}
}
//Derived Contract
contract E is C {
uint private result;
C private c;
constructor() public {
c = new C();
}
function getComputedResult() public {
result = compute(3, 5);
}
function getResult() public view returns(uint) { return result; }
function getData() public view returns(uint) { return c.info(); }
}


2. Inheritance
pragma solidity >=0.4.22 <0.6.0;
contract Parent {
 uint256 internal sum;
function setValue() external {
uint256 a = 10;
uint256 b = 20;
sum = a + b;
}
}
contract child is Parent {
function getValue() external view returns (uint256) {
return sum;
}
}
contract caller {
child cc = new child();
function testInheritance() public returns (uint256) {
cc.setValue();
return cc.getValue();
}
function show_value() public view returns (uint256)
{return cc.getValue();
}
Steps
 Deploy all contracts
Click test Inheritance and then click on show_value to view value 

OR

Inheritance
Code:
pragma solidity ^0.5.0;
contract C {
//private state variable
uint private data;
//public state variable
uint public info;
//constructor
constructor() public {
info = 10;
}
//private function
function increment(uint a) private pure returns(uint) { return a + 1; }
//public function
function updateData(uint a) public { data = a; }
function getData() public view returns(uint) { return data; }
function compute(uint a, uint b) internal pure returns (uint) { return a + b; }
}
//Derived Contract
contract E is C {
uint private result;
C private c;
constructor() public {
c = new C();
}
function getComputedResult() public {
result = compute(3, 5);
}
function getResult() public view returns(uint) { return result; }
function getData() public view returns(uint) { return c.info(); }
}


3. Abstract Contract
pragma solidity ^0.5.17;
contract Calculator {
function getResult() external view returns (uint256);
}
contract Test is
Calculator {
constructor()
public {}
function getResult() external view returns (uint256) {
uint256 a = 1;
uint256 b = 2;
uint256 result
= a + b;return
result;
}
}
Steps
 Deploy test contract
 Click on getResult to get sum of a+b

4. Constructor
pragma solidity ^0.5.0;
// Creating a contract
contract
constructorExa
mple {string str;
constructor() public {
str = "GeeksForGeeks";
}
function getValue() public view returns (string memory) {
return str;
}
}

5. Interfaces
pragma solidity ^0.5.0;
interface Calculator {
function getResult() external view returns(uint);
}
contract Test is
Calculator {
constructor()
public {}
function getResult() external view
returns(uint){uint a = 1;
uint b = 2;
uint
result = a
+ b;return
result;
}
}

OR

Interfaces
Code:
pragma solidity ^0.5.0;
interface Calculator {
function getResult() external view returns(uint);
}
contract Test is Calculator {
constructor() public {}
function getResult() external view returns(uint){
uint a = 1;
uint b = 2;
uint result = a + b;
return result;
}
}

C) Aim : Libraries, Assembly, Events, Error handling.
1. Libraries
myLib.sol Code
pragma solidity >=0.7.0 <0.9.0; library
myMathLib {
 function sum(uint256 a, uint256 b) public pure returns (uint256) {
return a + b;
 }
 function exponent(uint256 a, uint256 b) public pure returns (uint256) {
return a**b;
 }
}
using_library.sol
pragma solidity >=0.7.0 <0.9.0;
import "contracts/myLib.sol";
contract UseLib {
 function getsum(uint256 x, uint256 y) public pure returns (uint256) {
return myMathLib.sum(x, y);
 }
 function getexponent(uint256 x, uint256 y) public pure returns (uint256) {
return myMathLib.exponent(x, y);
 }
}
Output:
Steps:
 Deploy using_library contract
 Input values to both getexponent and getsum functions as below
 Execute both functions

OR

Libraries
Code:
pragma solidity ^0.5.0;
library Sum {
function sumUsingInlineAssembly(uint[] memory _data) public pure returns (uint o_sum) {
for (uint i = 0; i < _data.length; ++i) {
assembly {
o_sum := add(o_sum, mload(add(add(_data, 0x20), mul(i, 0x20))))
}
}
}
}
contract Test {
uint[] data;
constructor() public {
data.push(1);
data.push(2);
data.push(3);
data.push(4);
data.push(5);
}
function sum() external view returns(uint){
return Sum.sumUsingInlineAssembly(data);
}
}

2. Assembly
pragma solidity >=0.4.16 <0.9.0;
contract InlineAssembly {
// Defining function
function add(uint256 a) public view returns (uint256 b) {
assembly {
let c := add(a, 16) mstore(0x80, c)
{
let d := add(sload(c), 12) b := d
}
b := add(b, c)
}
}
}

OR

Assembly
Code:
pragma solidity ^0.5.0;
library Sum {
function sumUsingInlineAssembly(uint[] memory _data) public pure returns (uint o_sum) {
for (uint i = 0; i < _data.length; ++i) {
assembly {
o_sum := add(o_sum, mload(add(add(_data, 0x20), mul(i, 0x20))))
}
}
}
}
contract Test {
uint[] data;
constructor() public {
data.push(1);
data.push(2);
data.push(3);
data.push(4);
data.push(5);
}
function sum() external view returns(uint){
return Sum.sumUsingInlineAssembly(data);
}
}

3. Events
pragma solidity ^0.5.0;
// Creating a contract contract eventExample {
// Declaring state variables uint256 public value = 0;
// Declaring an event
event Increment(address owner);
// Defining a function for logging event
function getValue(uint256 _a, uint256 _b) public { emit Increment(msg.sender);
value = _a + _b;
}
}

4. Error Handling
solidity ^0.5.17;
contract ErrorDemo {
function getSum(uint256 a, uint256 b) public pure returns (uint256) {
uint256 sum = a + b;
assert(sum<255);
return sum;
}
Output :
Steps:
 Provide some values and press on getSum
 Check terminal panel

OR

Error Handling
Code:
pragma solidity ^0.5.0;
contract Vendor {
address public seller;
modifier onlySeller() {
require(
msg.sender == seller,
"Only seller can call this."
);
_;
}
function sell(uint amount) public payable onlySeller {
if (amount > msg.value / 2 ether)
revert("Not enough Ether provided.");
// Perform the sell operation.
}
}

5 Write a program to demonstrate mining of Ether.
const Web3 = require('web3');
const web3 = new Web3(new Web3.providers.HttpProvider('http: /127.0.0.1:7545')); / Replace
with your Ganache HTTP provider
async function mine() {
const accounts = await web3.eth.getAccounts();
const coinbaseacc1 = accounts[0];
const coinbaseacc2 = accounts[1];
console.log(`Mining ether on Ganache with coinbase address:
${coinbaseacc1}`);
while (true) {
try {
await web3.eth.sendTransaction({
from: coinbaseacc1,
to: coinbaseacc2,
value: 50,
});
console.log(`Mined a new block!`);
} catch (err) {
console.error(err);
}
}
}
mine();

6 Demonstrate the running of the blockchain node.
Step 1-> Create a folder named ethermine and a JSON file named genesis.json
and write the following lines in it.
{
"config": {
"chainId": 3792,
"homesteadBlock": 0,
"eip150Block": 0,
"eip155Block": 0,
"eip158Block": 0
},
"difficulty": "2000",
"gasLimit": "2100000",
"alloc": {
"0x0b6C4c81f58B8d692A7B46AD1e16a1147c25299F": {
"balance": "9000000000000000000"
}
}
}
Step 2-> Run command geth account new –datadir
C:\Users\Achsah\Documents\MScIT\sem4\blockchain_practical\ethermine
testnet-blockchain
Step 3-> Run command geth account new --datadir
C:\Users\Achsah\Documents\MScIT\sem4\blockchain_practical\ethermine
Step 4-> Run command geth --identity "localB" --http --http.port "8280"--http.corsdomain "*"
--http.api "db,eth,net,web3" --datadir
"C:\Users\Achsah\Documents\MScIT\sem4\blockchain_practical\ethermine"
--port "30303" --nodiscover --networkid 5777 console. This command will enable geth
console.
Step 5-> Run the command
miner.setEtherbase('0xC050FE4d9bAc591d29538e2FD9cCA848B29489D0’) in the geth
console
Step 6-> Run the command miner.start() to start mining
Step 7-> Below screenshots are the mining processes running on your local machine
Step 8-> To stop the mining press Ctrl+D

7 Create your own blockchain and demonstrate its use.
Create a javascript folder with the following code in any folder of your choice.
JavaScript Code
const SHA256 = require("crypto-js/sha256");
class Block {
constructor(index, timestamp, data, previousHash = "") {
this.index = index;
this.timestamp = timestamp;
this.data = data;
this.previousHash = previousHash;
this.hash = this.calculateHash();
}
calculateHash() {
return SHA256(
this.index +
this.previousHash +
this.timestamp +
JSON.stringify(this.data)
).toString();
}
}
class Blockchain {
constructor() {
this.chain = [this.createGenesisBlock()];
}
createGenesisBlock() {
return new Block(0, "21/04/2023", "Genesis Block", "0");
}
getLatestBlock() {
return this.chain[this.chain.length - 1];
}
addBlock(newBlock) {
newBlock.previousHash = this.getLatestBlock().hash;
newBlock.hash = newBlock.calculateHash();
this.chain.push(newBlock);
}
isChainValid() {
for (let i = 1; i < this.chain.length; i +) {
const currentBlock = this.chain[i];
const previousBlock = this.chain[i - 1];
if (currentBlock.hash = currentBlock.calculateHash()) {
return false;
}
if (currentBlock.previousHash = previousBlock.hash) {
return false;
}
}
return true;
}
}
/Blockchain Implementation
let myCoin = new Blockchain();
myCoin.addBlock(new Block(1, "22/04/2023", { amount: 4 }));
myCoin.addBlock(new Block(2, "22/04/2023", { amount: 8 }));
//console.log('Is blockchain valid? ' + myCoin.isChainValid());
console.log(JSON.stringify(myCoin, null, 4));

Output :
Flow of execution
Step 1-> Make sure you have installed nodejs in your system

Step 2-> We need crypto –js node module to make our own blockchain. So install it as
following
Step 3-> Run the above code in command line using command: node main.js

OR

Code:
import hashlib
import time
class Block(object):
def __init__(self, index, proof_number, previous_hash, data, timestamp=None):
self.index = index
self.proof_number = proof_number
self.previous_hash = previous_hash
self.data = data
self.timestamp = timestamp or time.time()
@property
def compute_hash(self):
string_block = "{}{}{}{}{}".format(self.index, self.proof_number, self.previous_hash,
self.data, self.timestamp)
return hashlib.sha256(string_block.encode()).hexdigest()
def __repr__(self):
return "{} - {} - {} - {} - {}".format(self.index, self.proof_number, self.previous_hash,
self.data, self.timestamp)
class BlockChain(object):
def __init__(self):
self.chain = []
self.current_data = []
self.nodes = set()
self.build_genesis()
def build_genesis(self):
self.build_block(proof_number=0, previous_hash=0)
def build_block(self, proof_number, previous_hash):
block = Block(
index=len(self.chain),
proof_number=proof_number,
previous_hash=previous_hash,
data=self.current_data
)
self.current_data = []
self.chain.append(block)
return block
@staticmethod
def confirm_validity(block, previous_block):
if previous_block.index + 1 != block.index:
return False
elif previous_block.compute_hash != block.previous_hash:
return False
elif block.timestamp <= previous_block.timestamp:
return False
return True
def get_data(self, sender, receiver, amount):
self.current_data.append({
'sender': sender,
'receiver': receiver,
'amount': amount
})
return True
@staticmethod
def proof_of_work(last_proof):
pass
@property
def latest_block(self):
return self.chain[-1]
def chain_validity(self):
pass
def block_mining(self, details_miner):
self.get_data(
sender="0", #it implies that this node has created a new block
receiver=details_miner,
quantity=1, #creating a new block (or identifying the proof number) is awared with 1
)
last_block = self.latest_block
last_proof_number = last_block.proof_number
proof_number = self.proof_of_work(last_proof_number)
last_hash = last_block.compute_hash
block = self.build_block(proof_number, last_hash)
return vars(block)
def create_node(self, address):
self.nodes.add(address)
return True
@staticmethod
def get_block_object(block_data):
return Block(
block_data['index'],
block_data['proof_number'],
block_data['previous_hash'],
block_data['data'],
timestamp=block_data['timestamp']
)
blockchain = BlockChain()
print("GET READY MINING ABOUT TO START")
print(blockchain.chain)
last_block = blockchain.latest_block
last_proof_number = last_block.proof_number
proof_number = blockchain.proof_of_work(last_proof_number)
blockchain.get_data(
sender="0", #this means that this node has constructed another block
receiver="Sana",
amount=1, #building a new block (or figuring out the proof number) is awarded with 1
)
last_hash = last_block.compute_hash
block = blockchain.build_block(proof_number, last_hash)
print("WOW, MINING HAS BEEN SUCCESSFUL!")
print(blockchain.chain)

8 Aim Install hyperledger fabric and composer. Deploy and execute the application.
Create VM

1. Download VMware Player.
2. Download Ubuntu ISO
3. Install vmware player
4. Create VM of Ubuntu using vmware player
$ sudo dpkg-reconfigure locales // choose en_US.UTF-8 if in doubt
$ sudo apt-get update
$ sudo apt-get upgrade
Install pre-requists
$ sudo apt-get install curl git docker.io docker-compose golang nodejs npm
Type Y for yes
Install Docker
$ sudo usermod -a -G docker $USER
$ sudo systemctl start docker
$ sudo systemctl enable docker
$ sudo chmod 666 /var/run/docker.sock
Install Hyperledger Fabric
1. Check the latest version of fabric repository
2. Install Fabric
$ curl -sSL http://bit.ly/2ysbOFE | bash -s 1.4.0
3. Check if fabric is installed, you should see big "END" once done
$ cd fabric-samples/first-network
$ ./byfn.sh generate
$ ./byfn.sh up
4. Check if fabric docker is running smoothly
$ docker ps -a
5. Stop the network
$ ./byfn.sh down

Install Composer
1. Create new user, when asked about the full name, use something different than the
full name used of the main user, to avoid confusion next time you are logging on.
$ sudo adduser playground
2. Set permission for the new user
$ sudo usermod -aG sudo playground
3. Login as the new user
$ su – playground
4. Install the prerequisites by getting and running the script from github. It will ask for
the password of “playground” account to proceed.
$ curl -O https://hyperledger.github.io/composer/latest/prereqs-ubuntu.sh
$ chmod u+x prereqs-ubuntu.sh
$ ./prereqs-ubuntu.sh
5. Logout and login with the new user to get things activated properly
$ exit
$ su - playground
6. Install components needed for running Hyperledger Fabric
$ curl -sSL http://bit.ly/2ysbOFE | bash -s 1.4.0
7. Install components needed for running Hyperledger Composer
$ npm install -g composer-cli composer-rest-server generator-hyperledger-composer
yo composer-playground
8. Start Composer
$ composer-playground
9. Open your browser and check it:
http://localhost:8080
