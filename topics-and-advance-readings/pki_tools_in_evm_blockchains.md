# PKI Tools in EVM-based Blockchains

By Christian Lundkvist [@ChrisLundkvist](https://twitter.com/chrislundkvist) \<christian.lundkvist@consensys.net\>

## Introduction

A blockchain can provide a good foundation for a PKI since it acts as a distributed well-publicized ledger whose integrity can be validated through the proof-of-work mechanism. A blockchain with a fully featured virtual machine such as [Ethereum][] (with its Ethereum VM or EVM) or the recent Bitcoin sidechain project [Rootstock][] (also EVM-based) provides a rich scripting language with which to build tools that can be used in a PKI.

A blockchain with such a virtual machine allows the user to send transactions creating blockchain-native programs, sometimes called "smart contracts" or simply "contracts". These programs have an associated address and expose API functions which can be called by sending a transaction to the address with a data message containing the signature of the function along with its parameters. The programs are run by miners and they have associated storage and/or funds (Ether in the case of the Ethereum blockchain) which is updated upon contract execution.


## Key Revocation

To show how such blockchain-native programs can be used in a PKI context we will demonstrate a simple program for defining a Key Revocation List. This program is written in the language [Solidity][] which compiles down to EVM bytecode. Similarly to the terminology used in Bitcoin we denote hashes of public keys _addresses_ and we can use these addresses to query our Key Revocation List.

```
contract KeyRevocationList {
  mapping (address => bool) public isKeyRevoked;

  function revokeKey() {
    isKeyRevoked[msg.sender] = true;
  }
}
```

In the above program we see that the hash table `isKeyRevoked` stores the revocation information for the stored addresses. The construct `msg.sender` denotes the address sending the transaction that calls the function, i.e. the transaction is signed by the private key belonging to the address `msg.sender`. The function `revokeKey()` therefore allows the revocation of a key that the user controls.

In order for someone to check if a key is revoked they would call the exposed getter function for the `isKeyRevoked` mapping of the `KeyRevocationList` program (the keyword `public` will automatically expose such a getter function). We assume that our Key Revocation List has a well-publicized address on the blockchain. Using e.g. the [Javascript API][jsapi] this would look something like

```
var revList = KeyRevocationList.at(wellKnownAddress);
revList.isKeyRevoked(addressOfQuestionableKey, function(err, isRevoked) {
  if (isRevoked) {
    console.log("Key is revoked. Abort!");
  }
  else {
    console.log("Key is not revoked. Continue!");
  }
});
```

## Key Expiry

We can also easily introduce key expiry by adding a few items to our `KeyRevocationList`:

```
contract KeyRevocationList {

  mapping (address => bool) public isKeyRevoked;
  mapping (address => uint) public keyExpiry;
	
  function revokeKey() {
    isKeyRevoked[msg.sender] = true;
  }

  function addKeyExpiry(uint secondsUntilExpiry) {
    // Only allow setting an expiry if it hasn't been set already
    if (keyExpiry[msg.sender] == 0) {
      keyExpiry[msg.sender] = block.timestamp + secondsUntilExpiry;
    }
  }

  function isKeyValid(address addrOfKey) constant returns(bool) {
    if ( !isKeyRevoked[addrOfKey] && 
         (keyExpiry[addrOfKey] == 0 || keyExpiry[addrOfKey] > block.timestamp)
       ) {
      return true;
    }
    else {
      return false;
    }
  }
}
```

In the above extension we note the construct `block.timestamp` that will return the block timestamp (expressed in unix time) at the time of function execution. We've also introduced a convenience function `isKeyValid()` that will return `false` if the key has been revoked or is expired.


## On-blockchain access control

Blockchain-native programs are often used for fiduciary control of funds, for instance as escrow accounts or on-chain wallets with enhanced functionality. For these programs access control is very important. Access control in smart contracts is mainly done through checking the `msg.sender` construct:

```
if (msg.sender == addrWithAccess) {
  // Do stuff
} else {
  // No access
}
```

With a Key Revocation List we can also easily check if the key is valid before allowing access:

```
KeyRevocationList krl = KeyRevocationList.at(wellKnownAddress);
var isKeyValid = krl.isKeyValid(msg.sender);
if (msg.sender == addrWithAccess && isKeyValid) {
  // Do stuff
} else if (!isKeyValid){
  // Oops, key is revoked or expired!
  // Use recovery/backup key, multisig procedure 
  // or similar to restore access.
} else {
  // No acccess
}
```

[ethereum]: https://www.ethereum.org
[rootstock]: http://www.rootstock.io
[solidity]: https://github.com/ethereum/wiki/wiki/Solidity-Tutorial
[jsapi]: https://github.com/ethereum/wiki/wiki/JavaScript-API
