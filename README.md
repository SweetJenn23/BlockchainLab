  ![STSA Logo](https://github.com/SweetJenn23/BlockchainLab/blob/master/images/STSALogo.png)
# Workshop 3: Blockchain

## Architecture
 In this lab, we continue building on the existing architecture. In prior labs, you configured your Raspberry Pi with Sens Hat to talk to Watson IoT Foundation running on Bluemix. You grew your interaction by integrating NodeRed and the Watson Conversation service also both running on Bluemix. Your cloud environment will expand to a hybrid cloud by talking with a blockchain network. The Hyperledger V1 Fabric is running on a private server in a secured network. 

In this lab, NodeRed will communicate with the Hyperledger Fabric through APIs. NodeRed will also facilitate communication between the ledger and Weather.com.

![Lab Architecture](https://github.com/SweetJenn23/BlockchainLab/blob/master/images/BlockchainArchitecture/Slide1.png)

## Application Overview
The blockchain workshop is intended to give you a basic understanding of how a developer would interact with Hyperledger Fabric. In this workshop you will use a Browser based UI to modify chaincode, test your code and deploy your changes. You will also learn how tooling can take the code and generate API to allow for application integration through a REST-ful interface. 

This lab will be broken into two parts Ð creating chaincode and generating API and using NodeRed to test API integration.

### Terminology
With blockchain, many words are used interchangeably. This section is an attempt to decode them and show how they are related.

** Hyperledger Fabric: ** A particular implementation of blockchain technology. This implementation is built for business use. It is an open source project lead by the Linux Foundation. It is one project within the Hyperledger Project. For more information, visit the [Hyperledger Project page](http://www.hyperledger.org/).




