# Defi Threat Modeling
This repo comprises of material related to threat modelling of DEFI and other Blockchain related Ecosystem.

## Approach 
In this threat analysis, the focus is primarily on dissecting the functional aspects of various web3 components, including NFT marketplaces, DAOs, Bridges, Dex. Recognizing that each component possesses a set of common functionalities, the analysis meticulously explores the potential security vulnerabilities and threats associated with these functionalities. The approach adopts a systematic examination of each functionality in its operational context to unveil risks. The culmination of this analysis presents a comprehensive understanding of the threat landscape within the web3 ecosystem, based on its constituent functionalities.


## DAOs (Decentralized Autonomous Organizations)
| Proposal Maker      | Voter          | Voting Power       | Smart Contracts             | Oracle             | Treasury          |
| ------------------- | -------------- | ------------------ | --------------------------- | ------------------ | ----------------- | 
| <details><summary>Malicious Proposals</summary>*DAOs beauty is that anyone can submit a proposal. Generally the verification of the proposal lies with the voters and the community. If a Malicious proposal is submiited and not examined and verfied correctly it can have a devastating effects. The classic example to Malicos Proposal Attack is of Tornado Cash in which attacker submitted a malious proposal and gained control over the DAO. Source:https://twitter.com/samczsun/status/1660012956632104960*</details> | <details><summary>Double Voting</summary>*Double Voting refers to the term where an attacker can double vote on a same proposal and affect the outcome of the proposal. This can arise due to the logic flaw in the code of voting code.It is recommended checking the following scenarios:<br><br>vote → transfer → vote again;<br>vote → delegate → vote again;<br>mangle a vote() arguments to add extra voting power;<br>check for reentrancy.*</details>  | <details><summary>Flash Loans Attack</summary>*A Flash Loan Attack is a type of exploit , where an attacker takes advantage of the flash loan feature to manipulate market/protocol conditions. In this type of attack, a malicious actor borrows a large amount of cryptocurrency through a flash loan, uses it to manipulate the market prices of assets, and then repays the loan within the same transaction block. In case of DAOs attacker can use flash loan to gain high amount of voting power and execute proposal in the same block.<br>Example:<br>https://bean.money/blog/beanstalk-governance-exploit<br>https://medium.com/@nvy_0x/the-beanstalk-bean-exploit-b038f4d324ea*</details> | Coding Practice Issues                 | <details><summary>Price Manipulation</summary>*Oracle Price Manipulation refers to an attack where a malicious actor manipulates the data provided by an oracle to exploit a smart contract or DAO. Many DeFi applications and DAOs rely on this data for critical functions, manipulating an oracle can have severe consequences, including the wrongful distribution of funds or the misrepresentation of asset values.<br>An attacker can manipulate oracle to gain tokens at a low price and get high voting power. An attacker can leverage this to vote on proposal in the DAO*</details> | <details><summary>Key Compromise</summary>*A Private Keys Compromise attack in the context of DAOs occurs when an unauthorized entity gains access to the private keys of participants, especially those who hold significant amounts of governance tokens or who have elevated permissions within the DAO. Private keys are crucial for signing transactions and controlling assets on a blockchain. When private keys are compromised, the attacker essentially gains full control over the associated wallet and can manipulate the DAO by making unauthorized transactions, voting on proposals, or even siphoning funds from the DAO.Keys compromise is considered as END GAME!*</details>    | 
| <details><summary>Voter Bribing</summary>*Voter Bribing in DAOs refers to a malicious practice where an entity offers incentives, to members of a Decentralized Autonomous Organization (DAO) in exchange for their voting power or specific voting actions. The intent behind this is usually to manipulate the decision-making process of the DAO to achieve outcomes favorable to the attacker, which may not necessarily be in the best interests of the DAO or its broader community. The likelyhood of this attack depends upon the value to be extracted from the sucessfull exploitation. It should be +ve after the incentives offered to the voters.*</details>       | <details><summary>51% Attack</summary>*In terms of DAO 51% Attack refers to the term in which an attacker gains more the 2/3 of the voting power and affects the outcome of the proposal. An attacker pocessing 51% of the voting power can unilateraly pass the proposal. Flash Loan attacks can be considered a type of 51% Attack.<br>Aragon DAO faced the similar attack but averted it https://blog.aragon.org/aragon-repurposes-dao-to-ensure-treasury-serves-its-mission/*</details>     |                    | <details><summary>Business Logic Issues</summary>*Business Logic Issues in the context of DAOs refer to vulnerabilities that arise due to flaws in the underlying smart contracts' code or design. Unlike other attacks that exploit the blockchain network, this type of attack takes advantage of unintended consequences of how the smart contract is programmed. It can lead to unauthorized actions, such as the manipulation of votes, fund theft, or unintended distribution of tokens.<br>Example:<br>Yam Finance suffered an issue in it rebase() method due to which after every rebase() $500k worth of yCRV will be added to the YAM treasury. If rebase happens as per the issue ,no further governance actions will possible as so many YAM will be held in the reserve that it will be impossible for any proposals.<br>https://medium.com/yam-finance/save-yam-245598d81cec*</details>       |                    | <details><summary>Governance Exploit</summary>*A Governance Takeover attack in the context of DAOs occurs when an entity gains control over a significant portion of the governance tokens, allowing them to unilaterally dictate the decisions and proposals within the DAO. By obtaining a majority or a critical mass of governance tokens, the attacker essentially takes over the governance process, and can then make decisions that benefit themselves at the expense of other participants, such as diverting funds, changing protocols, or making other malicious alterations to the DAO’s operations. Governance Takeover can also be carried out by passing of a malicious proposal proposed by attacker.<br>Example:<br>Takeover of Tornado Cash is a classic example.<br>https://decrypt.co/140932/tornado-cash-governance-attacker-offers-dao-new-lifeline-expensive-lesson*</details> |
| <details><summary>Sybil Attack</summary>*A Sybil Attack in the context of DAOs is when an attacker creates multiple fake identities, or controls a large number of accounts, in order to exert disproportionate influence over the decision-making process. By flooding the network with these identities, the attacker seeks to manipulate voting or consensus mechanisms in the DAO to their advantage, often at the expense of other participants and the overall health of the system.<br>Example of Sybil Attack can be SteemIt vs Justin Sun , where Sun gained control of the steemit network.Justin Sun, the founder of TRON, acquired Steemit Inc., which was one of the major organizations in the Steem ecosystem. With this acquisition, he also obtained a large quantity of pre-mined STEEM tokens, known as the "Steemit stake," which were originally meant for development and not to be used for governance.<br>Sun used these tokens in conjunction with major exchanges (Binance, Huobi, and Poloniex) to vote in new witnesses, effectively taking over the governance of the Steem blockchain. Many in the community viewed this as a hostile takeover, as it centralized control over a network that was intended to be decentralized.<br>In response, a large portion of the community decided to execute a hard fork to create a new blockchain, Hive, which was essentially a copy of the Steem blockchain but without the Steemit stake. This allowed them to continue with a more decentralized governance model.*</details>        |  |                    | Proxy Upgrade Attacks             |                    |                   | 
|                     |                |                    | Replay Attacks              |                    |                   | 
|                     |                |                    | Missing proposal validation |                    |                   | 
|                     |                |                    | <details><summary>Double Execution</summary>*In terms of DAO , Double Execution refers to a Smart Contract issue in which an attacker can execute a reentrancy in the execute/vote method of the DAO in the same Block.<br>A theoretical example can be a DAO with voting functionality and in the voting() or execution() there exist a reentrancy and an attacker can abuse it to cause double voting which will eventually affect the output of the proposal.*</details>            |                    |                   |
|                     |                |                    | <details><summary>Access Control Issue</summary>*Access control issues refer to a type of security vulnerability that occurs when inadequate controls or restrictions exist on who can access and modify certain resources or data within a system. In terms of DAO an attacker can leverage a misconfigured access control to execute higer leverage methods which can have implication depending upon the methods.<br>Example:<b1>DaoMaker was exploited for ~$4m. They left the `init` function unprotected. The attacker re-initialized the contract with malicious data and then called `emergencyExit` to get away with the funds.<br>https://twitter.com/Mudit__Gupta/status/1434059922774237185*</details>|||
|                     |                |                    | <details><summary>Profanity Wallet</summary>*A vulnerability in Profanity Wallets were identified by 1inch via which it was possible to crack the Private keys of Wallets generated via Profanity Generator.<br>Example:<br>Two projects were hacked via profanity issue<br>FriesDao:https://twitter.com/friesdao/status/1585712229067915264<br>Wintermute: https://twitter.com/EvgenyGaevoy/status/1572329148411936770<br>Although Wintermute is not a DAO but the threat is applicable across all type of Blockchain Apps deployed using profanity wallets*</details>|||
