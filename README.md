# NTNU_Application
This is a repository made especially for submitting the solution of NTNU Ph.D Assignment

We would be discussing the solution to the Ethereum Task (My Perspective) :

1. We need to select the Test Net according to our choice. It could be either of Ropsten, Kovan or Rinkeby.
2. We connect it then by using Metamask. We can choose it easily over there.

### Address Calculation

Geth has a function named web3.eth.getBalance() (to find the balance of the contract)
(after the contract has been deployed)
Syntax - 

web3.eth.getBalance(address [, defaultBlock] [, callback]) 
```
gives us the address of that particular block
```
Hence, this gives us the balance assigned to that contract.

Moreover, we could also call address.balance or this.balance

```
address(this).balance.
```
##### Ether Balance can also be computed as follows -
The sender is sending some value
