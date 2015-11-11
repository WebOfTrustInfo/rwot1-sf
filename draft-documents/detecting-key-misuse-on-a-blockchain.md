# Detecting Key Miuse on a Blockchain
#### *by Justin Newton*

## Summary

Within the Web of Trust, it is critical that someone authenticating the identity or other attributes associated with a private key is also keeping their own keys secure and under their control. If I am to trust Bob when he vouches for Jen’s key, I need to be certain that Bob’s key is under his control. Prior to the Web of Trust, loss of control of a private key impacted only the owner's security and the security of assets accessed through the token. Now, a small handful of misused keys can impact the security of the entire Web of Trust because they can create false identities, imitate other people, or create new identities from whole cloth. 

For this reason, it is critical that users know if their keys are compromised, so they can revoke and replace them.  (Revocation and replacement of keys will be left for another document.)

##  Problem
 
In any public-key cryptography system, there is a risk of a user losing control of his keys, and someone else gaining access to and using those keys without the owner's permission. This can lead to unauthorized access to systems as well as identity spoofing. In a Web of Trust environment there is an additional risk: a bad actor may use the lost keys to falsely validate the identity of others. This key misuse puts not only the original key owner, but the entire Web of Trust at risk.  

## Solution 

In PGP's classic Web of Trust system, misuse of keys is difficult to monitor because there is no centralized ledger or system that can track their use. Blockchain systems offer new opportunities for tracking transactions that involve a specific private key, using well understood and straightforward techniques. This could be implemented as a part of an existing service or as a stand alone Watcher Service available to users. 

This specification focuses on building a system that incorporates the Watcher Service into a standard Signing Service:

* The _Signing Service_ signs legitimate transactions and submits them to the blockchain. This is the job performed by _wallets_ in the blockchain ecosystem. 
* The _Watcher Service_ watches both transactions submitted to the blockchain by the signer and all other transactions occurring on the blockchain. It then compares these two lists to ensure that no transactions on the blockchain were signed by the user's private key without being submitted through the user's Signing Service.

![Solution Diagram](/event-documents/graphic-recording/07_Final%20Report%20Out_Rebrand%20WOT_2of2.jpg?raw=true)

## How It Works

In a traditional blockchain system the Signing Sevice ("wallet") simply signs transactions and submits them to the blockchain. In this system the Signing Service is responsible for two other things: 

1. When a new public/private key pair is created, the Signing Service submits a hash of the public key ("blockchain address") to the Watcher Service.
2. When the Signing Service submits a signed transaction to the blockchain, it also submits it to the Watcher Service.

The Watcher Service is where all of the action occurs:

1. It holds a list of all addresses associated with a user, provided by the Signing Service.
2. It holds a list of all transactions submitted through the Signing Service, also provided by the Signing Service.
3. It scans each new transaction on the blockchain to see if the list of inputs contains any of the user's addresses.
4. When a transaction with a watched address as an input is found, the Watcher Service checks if that transaction was also submitted to it by the Signer Service.
   * If it was, no problem.  
   * If it  was not, an alert is sent, notifying the user or system administrator that a private key may have been compromised.  
5. When a transaction is included in a block, that transaction is removed from the list held by the Watcher Service, as there should be no further submissions of that transaction to the blockchain.
