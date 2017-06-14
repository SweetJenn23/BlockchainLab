  ![STSA Logo](https://github.com/SweetJenn23/BlockchainLab/blob/master/images/STSALogo.png)
# Workshop 3: Blockchain

## Architecture
 In this lab, we continue building on the existing architecture. In prior labs, you configured your Raspberry Pi with Sens Hat to talk to Watson IoT Foundation running on Bluemix. You grew your interaction by integrating NodeRed and the Watson Conversation service also both running on Bluemix. Your cloud environment will expand to a hybrid cloud by talking with a blockchain network. The Hyperledger V1 Fabric is running on a private server in a secured network. 

In this lab, NodeRed will communicate with the Hyperledger Fabric through APIs. NodeRed will also facilitate communication between the ledger and [Weather.com](https://twcservice.mybluemix.net/rest-api/).

![Lab Architecture](https://github.com/SweetJenn23/BlockchainLab/blob/master/images/BlockchainArchitecture/Slide1.png)

## Application Overview
The blockchain workshop is intended to give you a basic understanding of how a developer would interact with Hyperledger Fabric. In this workshop you will use a Browser based UI to modify chaincode, test your code and deploy your changes. You will also learn how tooling can take the code and generate API to allow for application integration through a REST-ful interface. 

This lab will be broken into two parts: creating chaincode and generating API and using NodeRed to test API integration.

### Terminology
With blockchain, many words are used interchangeably. This section is an attempt to decode them and show how they are related.

**ledger:** an account book of final entry where business transactions are recorded. A ledger is typically associated with accounts. In this case, the concept remains the same but for business in general, not just finance.

**blockchain:** a decentralized, distributed ledger that records transactions between participants in a network. 

**block:** An ordered set of transactions that is cryptographically linked to the preceding block(s) on a channel.

**chain:** The chain of the ledger is a transaction log structured as hash-linked blocks of transactions. Peers receive blocks of transactions from the ordering service, mark the block?s transactions as valid or invalid based on endorsement policies and concurrency violations, and append the block to the hash chain on the peer?s file system.

**Hyperledger Fabric:** A particular implementation of blockchain technology. This implementation is built for business use. It is an open source project lead by the Linux Foundation. It is one project within the Hyperledger Project. For more information, visit the [Hyperledger Project page](http://www.hyperledger.org/).

**_Note:_** You will see blockchain, ledger, Hyperledger (referring to the fabric) and fabric used interchangeably. They are all referring to the concept of blockchain.

**Hyperledger Composer:** (Composer) an open development toolset and framework to make creating blockchain applications easier. The tooling can be used through a Command Line Interface (CLI) or through a web UI called Composer Playground. Each interface allows for developers to define the network in terms of participants, asset(s) and transactions.  Composer also includes the ability to run a rest server that uses Swagger to generate callable APIs to interact with chaincode. For more information: [Hyperledger Composer page](https://hyperledger.github.io/composer/introduction/introduction.html).

**asset:** something of value to participants in the network. They may be tangible or intangible goods, services or property.

**smart contract:** (contract) your terms for doing business in a blockchain network. Really, this is the conditions that a transaction can occur in. It may include checking for other specific information to allow the transaction to occur. In Composer terms, this is the logic that makes your transaction work.

**business network artifact:** When using Composer, the defined network of participants, assets and transactions can be exported to a file type known as business network artifact (.bna). 

**chaincode:** code written for blockchain. Typically this an application written in Go or NodeSDK. It now can also mean the same thing as your .bna. When you create your network and supporting logic in Composer, the entire package becomes your chaincode. 

**_Note:_** You may see chaincode, smart contract and transaction (in relation to Composer) used interchangably. They can refer to the same thing conceptually. In reality, chaincode == the business network artifact from Composer, transaction defines what is in a transaction (e.g. data, assets) and a smart contract is really the logic that is written to make a transaction actually happen in Composer.

