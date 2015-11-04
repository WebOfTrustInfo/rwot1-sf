Summary

When using the Web of Trust as a way to authenticate the identity or other attributes associated with a private key, it is critical that the keys of the people doing the authentication remain secure and under their control.  If I am to trust Bob when he vouches for Jen’s key, I need to be certain that Bob’s key is under his control.  In the past loss of control of one’s private key impacted their own security and the security of assets they have access to through the token.  With the Web of Trust a handful of mis-used keys can impact the security of the entire Web of Trust.  A small number of compromised keys could create one or a series of false identities, either imitating other people, or creating new identities from whole cloth.  For this reason it is critical that users become aware if their keys are compromised so they can go about revoking and replacing them.  Revocation and replacement of keys will be left for another document.

Problem
 
In any public key/private key encryption system there is a risk of a user losing control of their keys and someone else gaining access to and using their keys without the owner’s permission.  This can lead to unauthorized access to systems as well as identity spoofing.  In a Web of Trust environment there is an additional risk, the risk of a bad actor using a key to falsely validate the identity of others.  This key mis-use puts not only the original key owner, but indeed the entire Web of Trust at risk.  

Solution 

In historical Web of Trust systems mis-use of keys is very difficult to track as there is no centralized ledger or system to go to to track use of keys.  In blockchain systems there is an opportunity to track transactions happening on the blockchain using your private key.  This is reasonably straightforward to achieve using well understood and straightforward techniques.  This could be implemented as a part of an existing service or as a stand alone “watcher service” available for users.  This specification will focus on building one system that includes the watcher service in the same platform as the one that is normally doing the signatures.  

This system is made up of two components.  The first component is the “Signing Servioce”.  The Signing Service is the process which actually is signing legitimate transactions and submitting them to the blockchain.  This is the job performed by “wallets” in the blockchain ecosystem. 

The second service is the Watcher Service.  The Watcher Service watches all transactions occurring on the blockchain as well as transactions submitted by the signer to the blockchain.  It then compares the transactions in order to ensure that no transactions have been submitted to the blockchain signed using the user’s private key without the transaction having been submitted by the signing service.  

How It Works

In a traditional blockchain system the Signing Service, or Wallet sign transactions and submit them to the blockchain.  In this system the Siggning Service is responsible for several other things.  First, any time a new public/private key pair are created the signing service submits a hash of the public key (otherwise known as a “blockchain address”) to the watcher service.  Second, any time the Signing Service submits a signed transaction to the blockchain, it also submits it to the Watcher Service.

The Watcher Service is where all of the action is.  The Watcher Service has a list of all addresses associated with a user, as submitted to it by the Signing Service.  It watches all new transactions that are submitted to the blockchain and scans the list of inputs to see if it contains any of the addresses it should be watching.  When a transaction is submitted with a watched address in the inputs, the Watcher Service checks to see if that transaction was also submitted to it by the signer service.  If it was, no problem.  Once that transaction has been included in a block it can be removed from the list of transactions submitted by the Signing Service as there should be no further submissions of that transaction to the blockchain.  If it  was not, an alert is sent, notifying the user or system administrator that a private key may have been compromised.  



