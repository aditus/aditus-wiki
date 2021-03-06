# Aditus Wiki

---

## Roles within the Aditus Ecosystem
There are 4 distinct roles within the ecosystem:

#### Users:
This includes anyone that interacts with the Aditus API, smart invitations, tokens, mobile applications and resources. They function as the key interacting participants that the merchant will be targeting and where Aditus is providing a service for.

#### Merchants:
Retailers that is leveraging Aditus to better target users in a cost efficient and targeted manner while having a unique opportunity to target the crypto affluent. They will be creating smart invitations to serve a range of purpose to market and sell their products.

#### Aditus:
We are positioned as the platform maintainer to keep the Aditus ecosystem functional. At the current point in time, features of the Aditus platform, requires to a certain extent, a final arbiter to provide users and merchants the indicated service. As the ethereum protocols evolve, we aim to decentralise modules of the system to encourage a “fee / market” economy within the Aditus ecosystem.

#### Liquidity providers:
To cater for convertability to merchants and users in terms of payment method, we require a significant amount of liquidity to reduce the spread and price volatility when commercial transactions happen. Therefore we will be partnering with multiple liquidity providers ( centralised / decentralised ) to maintain a stable exchange rate.

---

## Modular Architecture
As the ethereum ecosystem is still in its initial stages of development, we feel the need to cater for extendability and upgradability of the Aditus platform. Therefore our approach is to modularised each business facing functionality with their own microservice API.

Our concerns stems from the following areas:

#### Protocol level enhancements
Technology like sharding, Swarm, Zksnarks, Plasma, lightning network, Shnorr signatures, cross atomic swaps would help different operational automation functionality when it comes into effect. Hence, we would need to cater for different trade-offs during implementation with certain trade-offs ( full decentralisation / partial centralisation ) within some of our modules. 

#### Ecosystem service providers
Decentralised applications like 0x, kyber network, omisego, polkadot, filecoin would be able to streamline our operations for areas where it might be handled by third party providers. We envision this to work best on areas where market making, token convertibility, liquidity and cross-chain interoperability comes into play by leverging the network effect of existing ecosystem.

---

## Smart Invitation
Since Aditus’s core audience will not be technology savvy, we want to abstracts away the concept of ether, gas price or gas limit that is essential to each ethereum transaction. 

There are 3 platform areas with regards to smart invitation: 
1. Aditus Merchant Console
2. Smart Invitation ( aka Smart Contract )
3. the Aditus Mobile Application

#### Merchant Console to Smart Invitation Interaction
1. Merchant would access the merchant console to set up their smart invitation
2. They would select their preferred smart invitation template
3. Enter in the predefined parameters needed for the users to complete the smart invitation
4. ADT token rewards to be distributed will be defined.
5. The final cost incurred by the merchant will be calculated at this point.
6. Merchant can choose to make the payment with SGD, USD, ADT, BTC, ETH
7. Upon completion of payment, the smart invitation will be created and the smart invitation address will then be stored in the Aditus “Smart Invitation Repository” Database.
8. The selected amount of ADT tokens for distribution will also then be sent to the smart invitation [ The Aditus wallet address will default with approval to transferFrom the smart invitation. This is avoid unnecessary logical complexity within the smart invitation’s code to deal with token transfers. ]
9. The generated smart invitation is ready to be interacted and available for personalised matching on the Aditus mobile application

#### Mobile Application to Smart Invitation Interaction
1. Private key of user’s account is held within the mobile application
2. The application interface will sign the message with user’s private key to be broadcasted onto the blockchain and send that to the Aditus API. [ This ‘transaction’ is done off-chain ]
3. The Aditus API will decrypt the signed message to ensure the transaction is properly formatted. [ This acts as a gateway to prevent DDoS and the unnecessary wastage of ether that Aditus is providing for all its customers ]
4. Upon validation of the transaction, the API will ‘repackage’ the raw transaction and broadcast the new transaction on-chain
5. Ether will be used from the contract address broadcasting the transaction which eliminates the need for users to understand ethereum while providing a seamless user experience

#### Smart Invitation to User Interaction
1. The smart invitation will validate the transaction formating and will throw any transaction that does not conform. [ Transactions sent from Aditus API would not have any issues but this is catered for users that might be integrating with the smart contract. This helps in further extendability of Aditus’s offering by allowing merchants to interact with generated smart contracts on their own product platform ]
2. Upon confirmation based on the smart invitation template type, the predefined allocation number of ADT token updated on the smart invitation’s contract storage. [ Tokens are not transferred to the user’s ethereum address yet. ]
3. To have a more efficient execution flow and prevent gas wastage, smart invitations addresses will be monitored for transactions and be queried by the Aditus API instead of being broadcasted by the smart invitation. [ Thus eliminating the need to send ether to smart invitations ]
4. Once a successful transaction is detected, the Aditus API will initiate the transfer of tokens to the indicated user address.
5. Upon completion or end of the smart invitation campaign, the smart invitation will be killed on the ethereum blockchain to better keep track of active campaigns.

#### Ether Payment Repository
1. Ether will be topped up periodically as it is being used up as gas for smart invitation
2. More complex functionalities can be added for operational automation purposes in the future [ e.g. security, rehydration, multisignature approval use case ]
* Contract paying for gas issue to be resolved with this EIP:
https://github.com/ethereum/EIPs/blob/bd136e662fca4154787b44cded8d2a29b993be66/EIPS/abstraction.md#rationale

---

## Smart Invitation Templates
By allowing merchant to have access based on different needs when targeting users, smart invitation templates makes it easy to do on-the-fly marketing with real rewards while still being able to leverage our core proposition of targeted marketing and immutable auditability of transaction behaviour in the ecosystem.

#### Physical On-site Invitation 
This smart invitation template consist of merchant who wants to invite consumers to participate in specific onsite events through the Aditus platform. By setting up geofencing and merchant defined access code, it'll bridge the gap between merchant and users by incentivising user to participate with ADT tokens as rewards.

#### Data Sharing Invitation
This smart invitation template consist of merchant who wants consumers who are interested to participate in their marketing campaigns. This creates the right incentive for the merchant ( to get users who are interested in their products & services ) and the users ( to redeem ADT token rewards for sharing their data ). 

#### Merchant Cashback Invitation
This smart invitation template consist of cashback that merchant may want to rewards users to encourage spending. For the users, it is as simple as receiving ADT tokens back on to their ETH address upon transaction confirmation.

#### Custom Invitation 
This smart invitation template onsist of a permutation of the other various available templates. By allowing the merchant to pick and choose conditional items within the smart invitation, it allows merchant to create targeted marketing opportunities.

---

## Smart Invitation Matching
1. Merchants create their personalised Smart Invitation through the Aditus Merchant Console
2. Smart Invitation Templates will have customisable selections for different needs
3. Upon confirmation, the invitation will be broadcasted on the Ethereum blockchain
4. The contract address of the Smart Invitation would then be stored within the Aditus database
5. During initiation of the Aditus Mobile Application, the contract address of all active Smart Invitations would be retrieved
6. Smart Invitation parameters will be queried from the ethereum blockchain to be match with user's local copy of perference data
7. Only filtered Smart Invitation that are relevant will be shown to users

---

## Decentralised Identity & Secure Wallet
To allow sufficient privacy for our catered audience while preserving a seamless user experience (for the non-tech savvy), we employ an identity architecture that abstracts the complexity behind our mobile interface. 

---

## Specifications

#### Message Format
Each order is a data packet containing order parameters and an associated signature. Order parameters are concatenated and hashed to 32 bytes via the Keccak SHA3 function. The order originator signs the order hash with their private key to produce an ECDSA signature.


#### Signature Authentication
The Aditus smart contract (program?) is able to authenticate the order originator’s signature using the ecrecover function, which takes a hash and a signature of the hash as arguments and returns the public key that produced the signature. If the public key returned by ecrecover is equal to the originator’s address, the signature is authentic.

Address publicKey = ecrecover( hash, signature( hash ) );
If ( publicKey != originator ) throw;

---

## Aditus Multisignature structure
Having a good multisignature structure is important for security and ensure the project can and will do everything as planned.

The following multisignature will hold reserves for different use cases:
1. The Aditus Foundation Multisig
2. Merchant Incentive Multisig
3. Strategic Partners & Token holders Incentive Multisig

All address listed uses the standard multisignature contract provided by Parity.
