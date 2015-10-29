# Key revocation of lost and stolen keys

By Martin Koeppelmann - martin.koeppelmann@consensys.net

## Introduction

If we usually speak about key revocation we have compromised keys in mind. Compromised means that an unauthorized third party has or even just might have access to a key. For professional entities it is a reasonable assumption that this is worst that can happen. However, a web of trust solutions that aims for broader use of average users has to deal with two even more problematic scenarios: lost and stolen keys. In both cases does the original owner do not have any longer access, while in the second case the key is additionally compromised.

## Decentralized key reset

In centralized architectures the central authority usually gives the user the option to reset a lost key (password). In a WoT network we can leverage the trusted nodes and give them the right to reset a key. A certain fraction or a threshold of the trusted nodes could be required. In the case of a lost key a dispute period should give the owner the chance to stop the revocation process by signing a specific message with the key. In the case of a stolen keys the rules about the numbers of trustees needs to be very strict because even the original key owner must not be allowed to stop the process.


## EVM based contract example

The advantages of an blockchain as PKI has been discussed [here][Todd]. Christian Lundkvist has given an introduction to PKI on EVM based blockchains [here][lundkvist]. This simple example is an extension of the introduced example by an implementation of the lost key resetting request. In this implementation every trustee has the right to report a key as stolen and request to replace the key by a new one. This request will trigger a dispute period of one week. During this period the request can be cancelled by the original key owner. After the period the old key is revoked and replaced with the requested one.

```
contract KeyRevocationList {

  mapping (address => bool) public isKeyRevoked;
  mapping (address => mapping (address => bool)) public trustees;
  mapping (address => LostKeyRequest) public LostKeyRequests;
  
  //one week request period
  uint constant RQEEST_PERIOD = 7 * 24 * 60 * 60;
  
  struct LostKeyRequest{
      address newKey;
      uint timeOfRequest;
  }

  function revokeKey() {
     // simlpe key revocation
    isKeyRevoked[msg.sender] = true;
  }

  function RequestLostKeyReset(address LostKey, address NewKey) {
      //requester needs to be trustee of the LostKey
      if (trustees[LostKey][msg.sender]){
         LostKeyRequests[LostKey].newKey = NewKey;
         LostKeyRequests[LostKey].timeOfRequest = now;
     }
  }
     
  function CancelResetRequest() {
    //the key owner can cancel a request
    delete LostKeyRequests[msg.sender];
  }
  
  function FinalizeRequest(address LostKey){
      if (LostKeyRequest[LostKey].timeOfRequest > 0 && 
          LostKeyRequest[LostKey].timeOfRequest + RQEEST_PERIOD > now){
              isKeyRevoked[LostKey] = true;
              //somehow set newKey
          }
  }
}
```

[todd]: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/blockchain-opportunities.txt
[lundkvist]: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/pki_tools_in_evm_blockchains.md
