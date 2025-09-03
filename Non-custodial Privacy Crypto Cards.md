---
title: Non-custodial cards with Privacy

---

# Non-custodial Crypto Cards With Privacy 

**By [Rakan](https://x.com/r6ra4) and [Mohammed](https://x.com/m38mah)**

Cards are the default way to spend money held in a bank account. The wide network effects of card networks like Visa, Mastercard, and American Express and integrated into payment supply chains like apple pay, google pay means you can practically spend them anywhere in the world (thats not under sanctions).  

Crypto and stablecoins (eg.[USDC](), [EURe](), GBPe) are enabling a new paradigm of money that is programmable, composable and noncustodial. New cards backed by crypto and settled on blockchains is a revolutionary paradigm, completely challenging the idea that spending on the card needs to come from a bank, you can now spend on card money that is held in your crypto wallet. 

"Crypto cards" are not all the same. Ones issued by centralized exchanges allow for spending of crypto but are custodial. Also, crypto cards that require paying crypto into a wallet the issuer controls is effectively a prepaid card and is also custodial. We are interested in noncustodial cards that give the user full power over their funds. 

However, existing noncustodial crypto cards use public blockchains to settle, meaning transactions have very little privacy. This article explores crypto cards on private blockchains that offer the financial privacy and confidentiality that exists in traditional cards. 

keywords: stabelcoins, [openfi](https://medium.com/idos-publication/openfi-programmable-money-for-everyday-use-77d9353e13fb)

### How cards generally work

Traditional cards have a number of stakeholders involved:
- **Card network** (eg. Visa, Mastercard, Amex): Set the rules, connect issuers and acquirers, and handle message routing. 
- **Issuer** (eg. bank)  Issues the card to the user. They're responsible for approving transactions, ensuring funds or credit are available, and settling with the network.
- **Acquirer**: A financial institution or payments company that enables merchants to accept card payments. It receives authorization requests from the merchant, routes them through the card network to the correct issuer, and ultimately settles funds to the merchant after the transaction is approved.
- **Payment Processor** (e.g., Stripe, Adyen): Tech layer that connects the merchant to the acquirer and handles the transaction flow.
- **Merchant**: Entity selling goods and accepting the payment.
- **User**: The cardholder making the payment.

![image](https://hackmd.io/_uploads/BJ_v2zLhJl.png)

The card transaction lifecycle involves three steps:
1. **Authorization**: Real-time check with the issuer to approve or decline a transaction.
2. **Clearing**: Transaction data is sent through the network to calculate the final amount (e.g., applying currency conversion, fees).
3. **Settlement**: Funds are actually transferred between banks.

For the issuer these cards are different in how they manage risk and funding:

- **Debit**: Pulls directly from your bank account.
- **Credit**: Draws from a credit line, paid back later.
- **Prepaid**: Funds are preloaded, no credit or bank account needed.

For merchants, acquirers, and processors, these are mostly the same — all run through the same infrastructure with minor differences in interchange fees or risk models.


What is a Issuer Processor vs. BIN Sponsor? 

- Issuer Processor (e.g., Marqeta, Galileo): Handles the tech for issuing cards, managing balances, transaction auths, etc.
- BIN Sponsor: A licensed bank that lets fintechs issue cards using its regulatory approvals and BINs. Identified by the first 6 digits of a card.

Interchange fees, the cards business model. 
https://www.kulipa.xyz/post/what-is-the-interchange-fee-and-how-can-it-improve-revenue-for-crypto-wallets

### Offramping and Double-Spend: The Twin Problems of Noncustodial Crypto Cards
Because non-custodial cards hold funds in stablecoins on a public blockchain, and merchants operate on fiat basis, there are two main questions any noncustodial card must answer: 
1. **How to offramp stable to fiat** How does the merchant/acquiror eventually receive fiat. i.e. how does the offramping actually happen. 
2. **The Double Spend problem** How to solve the double spend problem. what if the user spends at the cashier but submits an onchain tx in the same block to withdraw funds? how do funds get locked to avoid this? 

For the **offramping**, specialized card issuers handle this for card users, this is made feasible because stable issuers like Circle or Monerium offramp for businesses at 1:1 and issuers just need to guarantee their access to stablecoins so they can use them at time of settlement. 

For the **double spend** problem there are four approaches:

1. **Approval based**: Simply spend the crypto on spot from a noncustodial wallet like metamask at time of tx, (the same way you would spend it when swapping on uniswap). It works by giving approval beforehand for a limit and then tapping the card initiates a transaction. 
2. **Custom Smart contract wallet**: User transfers crypto to a smart contract wallet with extra logic to handle the double spend. Particularly a time delay is introduced as is the case in [gnosis cards](https://help.gnosispay.com/en/articles/8464758-how-is-the-gnosis-card-self-custodial) with the time delay module. 
3. **Multisig based**: User transfers crypto to a wallet that has a cosigner requirement on withdrawals. This is the design of Argent card that is powered by Kulipa. In this design Argent approves the withdrawals and makes sure no withdrawals are cosigned that spends already authorized funds on the card.  
4. **Pool Based** user deposits into a pool. Also called universal funding in Immersve's frameworks. Tokens are pooled into a smart contract, maintaining accounts via internal mapping and paid out during settlement; resulting in a gas efficient process. 


### Exploring The Design Tradeoffs 

The factors we used to evaluate a card design are: 
- gas fees
- privacy 
- custody 


The approval based approach requires a fast and cheap blockchain to allow for a smooth flow but is as noncustodial as it gets because the user fully controls the funds and requires no one to withdraw. The issue of course is that each tx is a onchain tx and has the least privacy. 

The custom smart contract wallet with delay option allows the user good control over their funds, however the time delay option means every transaction on the card results in a transaction onchain as well. It also removes the blockchain as a dependency for the tx flow because settlement is no longer tied to blockchain times. 

The cosigner approach allows for aggregation of card transacions done by the user throughout the day where funds are only taken once at end of day, thereby lowering tx costs and offering some obfuscation if the user has many transactions throughout the day. It can be argued that if a user can only withdraw with permission of some entity x, then how noncustodial is it really?

The choice of blockchain where a card settles affects tx gas fees. For example Gnosis chain fees are less than 1 cent in comparison to a card that settles on polygon. 

add pools discussion

![image](https://hackmd.io/_uploads/Hy-d7S0Ryg.png)


### Summary of cards service providers 

To facilitate noncustodial cards some services emerged to facilitate, each differring slightly in how they answer questions above. Below is a summary of crypto focused noncustodial cards service providers. 

| Name | Issuer? | Cards | Website |
|------|---------|-------|---------|
| Monovate | Yes | gnosisPay, ledger, metamask  | https://www.monavate.com/ |
| Kulipa | No | Argent | https://www.kulipa.xyz/ |
| Immersve | Yes | Hana,pera | https://immersve.com/ |
| Baanx | No | metamask, ledger | https://baanx.com/ |

- Monovate is card issuer for Gnosis Pay crypto cards in Europe. 
- Baanx enables ledger, metamask cards 
- Kulipa is a middleware but is not issuer. Also works with Monovate. 
- Immersve has an impressive suite of APIs and products, and has built custom contracts for a non-EVM, Algorand.

There are many other crypto card issuers with a noncustodial focus, and are therefore not mentioned in the table above. 

### The privacy issue in noncustodial crypto cards 

Because noncustodial crypto cards spend crypto that is held onchain, and the settlement also happens onchain, transactions are public in most of the designs above. Each wallet's (whether EOA or smart contract) has a unique onchain address whose txs are visible. 

Moreover, spending on a noncustodial crypto card in the real world results in an observable footprint that is ample material for cross referencing. For example, a CCTV observing a user transacting with a card, can now link their wallet to a face. Whereas traditional card doesnt reveal any information to the observer. 

This [article](https://tzedonn.substack.com/p/22-crypto-cards-will-get-you-robbed) is a good overview on privacy issues in crypto cards, we recommend reading it. 

Some obvious privacy related scenarios: 

- **Visibility at time of sale**: if a merchant (or person behind you in queue) is able to observe a card that initiates an onchain tx on spot then they are able to deduce information on spending habits and attach this data to a person. This is an [example](https://x.com/ganainmtech/status/1880252520096018589) of how visibility looks like.  
- **Onchain analysis**: Because smart contracts of issuers or service providers are usually public, onchain analysis of wallet interactions might result in leaking information about users. This could be as trivial as checking ENS names to observing their defi interactions.  
- **Funding wallet observability**: If a wallet of a user is known by someone they will be able to check the funding wallet and perhaps observe the networth. Where good opsec (eg. funding from railgun or privacy pools or even a cex) solves this issue, it's a big ask for simple crypto users on ux side.

The natural human tendency for confidentiality in financial dealings makes us believe the design space for crypto cards still in exploration phase, and confidential crypto card designs that mimics traditional cards are yet to be explored. 

An interesting approach is to leverage private smart contract blockchain like Aztec, Aleo, or Miden as settlement layers. 

### Aztec based Cards 

- Do we need a native stablecoin on Aztec?
- can we already bake in the needed modules in the wallet contract? 
- Smart Contracts Architecture

It is not trivial to say crypto cards settled on a private blockchain solves all privacy issues. For example Aztec might have block times of few mins,

- Gas fees (could they be sponsored?)
- L2 considerations
- Block times 

A time delay on withdrawals would work well.
instant tx will not work well. So this leaves us with second best choice: a time delayed smart contract. 

What about AML? 
Since every issued card is KYC verified, we do not foresee any compliance issues. However any thoughts on this are welcome. 

https://www.pcisecuritystandards.org/standards/
