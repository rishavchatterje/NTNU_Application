# NTNU_PhD__Application_Task
This is a repository made especially for submitting the solution of NTNU Ph.D Assignment

We would be discussing the solution to the Ethereum Task (My Perspective) :

1. We need to select the Test Net according to our choice. It could be either of Ropsten, Kovan or Rinkeby.
2. We connect it then by using Metamask. We can choose it easily over there.

### Address Calculation

Geth has a function named web3.eth.getBalance() (to find the balance of the contract)
(after the contract has been deployed)
Syntax - 
```
web3.eth.getBalance(address [, defaultBlock] [, callback]) 
```
gives us the address of that particular block

Hence, this gives us the balance assigned to that contract.

Moreover, we could also call address.balance or this.balance

```
address(this).balance.
```
##### Ether Balance can also be computed as follows -
The sender and nonce are RLP encoded 
how many transactions the sender has sent is nonce. The address of the contract is basically the address of its sender.

This answers the second part of the question as well. Once we calculate the nonce, we would be able to figure out the number of transactions that are  being taking place.
```
nonce0= address(keccak256(0xd6, 0x94, address, 0x80))
nonce1= address(keccak256(0xd6, 0x94, address, 0x01))

```
This is a bit interesting; it means that these can be used to ‘hide’ money. From accountA, we can send ether to e.g. the nonce1-address. At this address, the ether will be unrecoverable, until we first make a transaction (increasing accountA nonce to 1) and then create a contract which lands on nonce1 and thus becomes the owner of the money; and can send it back again.

The contracts are, naturally, part of the same address space as the normal accounts; and the address of a contract is determined thus :
The sender and nonce are RLP encoded and then hashed with Keccak-256.
```
address = sha3(rlp_encode(creator_account, creator_account_nonce))[x:] 

```
###Snippets
I have tried writing one code in Java. We have to convert the address to a byte[], then encode, then Hash with Keccak-256 and we are ready with the output.
```
private String findcontractAddress(String address, long nonce){
    byte[] addressAsBytes = Numeric.hexStringToByteArray(address);

    byte[] foundAddressAsBytes =
            Hash.sha3(RlpEncoder.encode(
                    new RlpList(
                            RlpString.create(addressAsBytes),
                            RlpString.create((nonce)))));

    foundAddressAsBytes = Arrays.copyOfRange(foundAddressAsBytes,
            12, findAddressAsBytes.length);
    String foundAddressAsHex = Numeric.toHexString(foundAddressAsBytes);
    return foundAddressAsHex;
    
}
```
###Dependencies
We would need to have web3.js and rlp encoding as dependencies and these needs to be called in order to run the program.

The answer to the question will be - It's easy to calculate the first part since we can fetch the value by using various operators within a testnet, that which contract has the highest ether balance. But for the second part, we would need to find the nonce value for each of the transactions made by the sender. This would let us know  about the details of that particular tx.


