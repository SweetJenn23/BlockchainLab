  ![STSA Logo](images/STSALogo.png)
# Workshop 3: Blockchain

## Architecture
In this lab, we continue building on the existing architecture. In prior labs, you configured your Raspberry Pi with Sens HAT to talk to Watson IoT Foundation running on Bluemix. You grew your interaction by integrating NodeRed and the Watson Conversation service also both running on Bluemix. Your cloud environment will expand to a hybrid cloud by talking with a blockchain network. The Hyperledger V1 Fabric is running on a private server in a secured network. 

In this lab, NodeRed will communicate with the Hyperledger Fabric through APIs. NodeRed will also facilitate communication between the ledger and [Weather.com](https://twcservice.mybluemix.net/rest-api/).

![Lab Architecture](images/BlockchainArchitecture/Slide1.png)

## Application Overview
The blockchain workshop is intended to give you a basic understanding of how a developer would interact with Hyperledger Fabric. In this workshop you will use a Browser based UI to modify chaincode, test your code and deploy your changes. You will also learn how tooling can take the code and generate API to allow for application integration through a REST-ful interface. 

This lab will be broken into two parts: creating chaincode and generating API and using NodeRed to test API integration.

### Terminology
With blockchain, many words are used interchangeably. This section is an attempt to decode them and show how they are related.

**ledger:** an account book of final entry where business transactions are recorded. A ledger is typically associated with accounts. In this case, the concept remains the same but for business in general, not just finance.

**blockchain:** a decentralized, distributed ledger that records transactions between participants in a network. 

**block:** An ordered set of transactions that is cryptographically linked to the preceding block(s) on a channel.

**chain:** The chain of the ledger is a transaction log structured as hash-linked blocks of transactions. Peers receive blocks of transactions from the ordering service, mark the block's transactions as valid or invalid based on endorsement policies and concurrency violations, and append the block to the hash chain on the peer's file system.

**Hyperledger Fabric:** A particular implementation of blockchain technology. This implementation is built for business use. It is an open source project lead by the Linux Foundation. It is one project within Hyperledger Project. For more information, visit the [Hyperledger Project page](http://www.hyperledger.org/).

**_Note:_** You will see blockchain, ledger, Hyperledger (referring to the fabric) and fabric used interchangeably. They are all referring to the concept of blockchain.

**Hyperledger Composer:** (Composer) an open development toolset and framework to make creating blockchain applications easier. The tooling can be used through a Command Line Interface (CLI) or through a web UI called Composer Playground. Each interface allows for developers to define the network in terms of participants, asset(s) and transactions.  Composer also includes the ability to run a rest server that uses Swagger to generate callable APIs to interact with chaincode. For more information: [Hyperledger Composer page](https://hyperledger.github.io/composer/introduction/introduction.html).

**asset:** something of value to participants in the network. They may be tangible or intangible goods, services or property.

**smart contract:** (contract) your terms for doing business in a blockchain network. Really, this is the conditions that a transaction can occur in. It may include checking for other specific information to allow the transaction to occur. In Composer terms, this is the logic that makes your transaction work.

**business network artifact:** When using Composer, the defined network of participants, assets and transactions can be exported to a packaging of files known as a business network artifact (.bna). 

**chaincode:** code written for blockchain. Typically this is an application written in Go or NodeSDK. It now can also mean the same thing as your .bna. When you create your network and supporting logic in Composer, the entire package becomes your chaincode. 

**_Note:_** You may see chaincode, smart contract and transaction (in relation to Composer) used interchangably. They can refer to the same thing conceptually. In reality, chaincode == the business network artifact from Composer, transaction defines what is in a transaction (e.g. data, assets) and a smart contract is really the logic that is written to make a transaction actually happen in Composer.

## Project Repositories
**_TBD_

## Workshop Setup
To run this workshop you will need the following:
1. Webbrowser (tested with Firefox and Chrome)


## Workshop Instructions
### Scenario Overview
Your Raspberry Pi Sens HAT detects the temperature in the room or the temperature you create around it. In a real world scenario, this could be a temperature gauge in your house or in an office building. In this lab, we have a logical thermostat that only exists programatically in blockchain. This could be connected to a real thermostat like Nest via API. To keep family members, housemates, friends or children from excessively running air conditioning or heat, they must first find out if they have permission to adjust the thermostat by running a transaction defined in a smart contract running on Hyperledger Fabric. We will also add in the ability to consult current conditions via API from Weather.com to optimally set the thermostat.

### Part 1 - Working with Chaincode
In this section of the lab you will be working with Hyperledger Composer to create chaincode that could run on a blockchain network. We will create our code in the the Composer Playground, a browser based UI. The code has already been started and is stored in GitHub.

#### Defining your blockchain network
1. Open the GitHub [repository for this lab](https://github.com/SweetJenn23/BlockchainLab).
   ![GitHub Repository](images/Part1_Step1.png)






2. Select **stsa-temp-part1.bna**.
   ![Select stsa-temp-part1.bna](images/Part1_Step2.png)






3. Click **Download**.
   ![Select Download](images/Part1_Step3.png)






4. In a browser, go to the Composer Playground running on Bluemix. [https://composer-playground.mybluemix.net/editor](https://composer-playground.mybluemix.net/editor)

   * <u>Note:</u> You will need to view the browser in Full Screen (fully expanded) mode to be able to access everything and prevent issues with inability to scroll on certain screens.

   ![Open Composer Playground in a browser](images/Part1_Step4.png)

   ​

   * Explore Composer Playground.

     * Click **About** *(README.md)*: This is a text file designed to tell you about the code you are going to work with.

       ​

     * Select **Model File** *(models/org.acme.sample.cto)*: This is where you create your *model* `participants`, `assets` and `transactions`.

     ![Model File Samples](images/Part1_Step4ModelFile.png)

     ​

     * Select **Script File** *(lib/sample.js)*: This is where you write JavaScript to give functionality (logic) to your model. All of this together creates your chaincode.

       ![Script File example](images/Part1_Step4ScriptFile.png)

       ​

     * Select **Access Control** *(permissions.acl)*: This allows you to control what permissions participants in the network have.

       ![ACL example](images/Part1_Step4ACLFile.png)

       ​

     * **Note:** All of these files together become part of your **.bna** (business network archive) once you deploy them. Business Network Archive is a file type created by Hyperledger Composer. You may also hear this refered to as business network definition.

       ​

     * Select **Add File**: This would allow you to add another file to the web UI. Click **Cancel**

       ![Add File example](images/Part1_Step4AddFile.png)

       ​

     * At the top of the page, select **Test**.

       ![Select Test](images/Part1_Step4Test.png)

       ​

     * <u>Note:</u> Under the Test tab, you will be able to interact with your code after you've selected **Deploy** on the Define tab. As shown below, you see that you can create a participant based on specifications from your model file. We won't explore through more of these right now because we will be working with them closely later in the lab.

       ![Example of Testing code](images/Part1_Step4SampleParticipant.png)

       ​

     * At the top of the page, select **Admin**.

       ![Select Admin](images/Part1_Step4Admin.png)

       ​

     * <u>Note:</u> The credentials that Composer Playground is using to access blockchain are stored here. From here you can also issue new credentials if you have authority.

       ![Admin Sample](images/Part1_Step4AdminSample.png)

       ​

     * <u>Note:</u> The Composer Playground running on Bluemix is not currently connected to a blockchain environment. That's okay! The browser will simulate how things would work if connected to blockchain. In a Composer Playground connected to a blockchain, there will be a **globe** icon instead of **Get local version**. In that tab, you can create a connection profile with issued credentials to access specific blockchain networks where you would deploy your business network definition and interact with it.

       ![Connection example](images/Part1_Step4Globe.png)

     ​





5. Click back to the **Define** tab and scroll down on the left side of the Composer Playground to select **Import/Replace**.
   ![Select Import/Replace](images/Part1_Step5.png)





6. Click the **browse** link.
   ![Click browse](images/Part1_Step6.png)





7. Navigate to where you downloaded the **stsa-temp-part1.bna** file, select the file and click **Open**.
   ![Select stsa-temp-part1.bna](images/Part1_Step7.png)





8. From the _Import/Replace dialog window_, verify that your file shows it contains 1 asset, 0 participants and 3 transactions. Click **Deploy**.
   ![Deploy bna file.](images/Part1_Step8.png)





9. On the warning box, _Current definition will be replaced_, accept the warning by clicking **Replace & Import**.
   * <u>Note for Hyperledger Composer V0.7 - 0.9</u>: When you deploy your business network to Hyperledger Fabric, the business network name is used as the chaincode ID. If the business network name is changed then a new chaincode ID will be issued and used on deploy. All existing data in blockchain will be lost due to the change. 
     ![Click Replace & Import](images/Part1_Step9.png)




10. You should now see the README and project named for stsa-temperature-part1. **Read through the README.**![stsa-temperature-part1](images/Part1_Step10.png)











11. Clilck on **Model File**.

![Click Model File](images/Part1_Step11.png)













12. Click in the **editor** on the right to begin writing your models. 

    * <u>NOTE:</u> **DO** **NOT** modify the namespace during the lab.

      ![Click in the editor](images/Part1_Step12.png)













13. On a new line, give your asset `Team` the following attributes.

    * ​<u>Explanation: </u> In this lab, the asset type is "Team". The attribute name of the Team asset for transactions is "asset". You could actually change the attribute name to be something else such as :star: "DallasCowboys" :star: when you create your own code. In that case it would look something like:

      ```
      DallasCowboys Team identified by teamID{

        o String teamID

        o String teamName

        o Double sensorTemp

        o Double thermostatTemp

        o String recommendation

      }
      ```

    * Note: a small "o" is used as a bullet in the model.

    * `o String teamID` — this will be the value that is assigned to your team. (already there!)

    * `o String teamName`— this could be anything! Come up with something clever!

    * `o Double sensorTemp` — temperature from the Raspberry Pi will be stored here.

    * `o Double thermostatTemp`— you will create a temperature for the thermostat.

    * `o String recommendation`— this will be populated based on the `CompareWeather` transaction.

      ![Team model](images/Part1_Step13.png)











14. Now create your first transaction model for `SetSensorTemp`. Enter the following attributes:

    * `o String transactionId` — This is given value by the fabric. We will never populate this field.

    * `--> Team asset` — The transaction will need to put data into the `Team` asset. This passes a reference to the asset so we can work with the asset in the logic for the transaction.

    * `o Double newSensorValue` — This is the variable that will be set by the temperature passed into the transaction from the Raspberry Pi Sens Hat.

      ![Create SetSensorTemp model](images/Part1_Step14.png)











15. Build your `ChangeThermostatTemp` transaction model. Add the following:

    * `o String transactionId` — This is given value by the fabric. We will never populate this field.
    * `--> Team asset` — The transaction will need to put data into the `Team` asset. This passes a reference to the asset so we can work with the asset in the logic for the transaction.
    * `o Double newThermostatValue` — This allows for a new, proposed value to be sent into the transaction. In the logic tab, we will use this value to compare to what the sensor says and decide if the thermostat value should be adjusted.

    ![Create ChangeThermostatTemp model](images/Part1_Step15.png)













16. Enter the following values to build your `CompareWeather` transaction model:

    * `o String transactionId` — This is given value by the fabric. We will never populate this field.

    * `--> Team asset` — The transaction will need to put data into the `Team` asset. This passes a reference to the asset so we can work with the asset in the logic for the transaction.

    * `o Double outsideTemp` — Looking at the [Weather.com API](https://twcservice.eu-gb.mybluemix.net/rest-api/#!/Current_Conditions/v1locobscurrent) for Current Conditions, you can see all of the possible data that the call could return. 

      ![Weater.com API temps](images/Part1_Step16Temps.png)

      Based on the data, it was decided to take the actual outside temperature and the feels like temperature to give a recommendation on thermostat settings. This variable stores the value passed into it via NodeRed from Weather.com for the outside temperature.  The model on the API page shows up whether the data is returned in Celsius or Fahrenheit and its variable type. For this lab, we are working with Celsius as this is the measure of temperature that the Raspberry Pi Sens Hat uses.

    * `o Double feelsLike`— the variable to store the feels_like value from Weather.com.

    ![create CompareWeather model](images/Part1_Step16.png)













17. Click on the **Script File** tab.

    ![Click Script File](images/Part1_Step17.png)













18. Review the code in the editor. ******Verify that your variable names match the variable names here.****  Capitalization does matter! If names don't match, you'll have errors. 

    * Any guesses what the code is doing for each transaction?

    ![Review code](images/Part1_Step18.png)













19. Click **Deploy**.
    * <u>Note:</u> When connected to an actual blockchain this would create a new contract on the ledger. If you ever modify the project name for any reason, this will create a new contract. The project name is currently used as the chaincode ID for Composer V0.7.3. The project name is viewable and editable on the **About** page.

![Click Deploy](images/Part1_Step19.png)













20. You should see a *Deploy Successful* message appear in the upper right corner of the browser.

    ![Deploy Successful message](images/Part1_Step20.png)













21. Click on the **Test** tab at the top to try out your code.

![Click Test](images/Part1_Step21.png)











22. Notice that in this particular case because we have no participants, the **Test** tab has opened to the **Asset** menu on the left. You must have an asset to be able to run any of the transactions.

    * Click **Create New Asset**.

    ![Click Create New Asset](images/Part1_Step22.png)











23. Create an example asset to test your code by filling in the following information:

* `"teamID": "teamID:**xxx**"` where ** **xxx** ** is the team number given to you at STSA.
* `"teamName":""` — this could be any name you'd like. Be clever! :bowtie:
* `"sensorTemp": **0**` — Set ** **0** ** to any value. When you work with NodeRed, temperatures will be in Celsius, but for this it doesn't matter. Just be consistent either way with Fahrenheit or Celsius.
* `"thermostatTemp": **0** `— Set ** **0** ** to any value. This is initializing your thermostat so pick a value you want to work with.
* `"recommendation": "" `— Leave this as is.
* **Make a note somewhere** of the values you used for `sensorTemp` and `thermostatTemp`.

![Create asset](images/Part1_Step23.png)











24. Click **Create New**.

![Click Create New](images/Part1_Step24.png)













25. Once your **Team** asset is created it should show in the registry as shown below.

    ![Asset registry](images/Part1_Step25.png)











26. You're ready to run your first transaction. Click on **Submit Transaction**.

    ![Click Submit Transaction](images/Part1_Step26.png)











27. The **Submit Transaction** dialog will open a new window. 

    a.  Make sure that the **Transaction Type** is set to `SetSensorTemp`.

    b.  Modify the JSON data.

    * `"asset": "resource:org.acme.sample.Team#teamID:xxx"`  — enter your team's identifier in 		place of the value where **xxx** is in the sample JSON data.


    * `"newSensorValue": 0` — enter a value your sensor could have.

    c.  Click **Submit**.

![Submit SetSensorTemp](images/Part1_Step27.png)










28. If you submitted the transaction with your correct team ID, then you should have a transaction showing in your registry with the data you entered in the prior step. Congratulations! You've now completed a transaction. :thumbsup:

![Transaction Registry](images/Part1_Step28.png)











29. Verify that `SetSensorTemp` updated the `sensorTemp`value in your asset. Click **Team**.

    ![Click Team](images/Part1_Step29.png)









30. Check the `sensorTemp` value. Does it have the new value from the `SetSensorTemp` transaction?

![Check sensorTemp value](images/Part1_Step30.png)













31. Let's do another transaction. Select **Submit Transaction**.

![Select Submit Transaction](images/Part1_Step21.png)











32. This time let's run, `ChangeThermostatTemp`. 


1. In the **Transaction Type** drop down, select `ChangeThermostatTemp`.

   ![Select ChangeThermostatTemp](images/Part1_Step32_1.png)

2. Edit the sample JSON for the transaction.

   * `"asset": "resource:org.acme.sample.Team#teamID:xxx"`— change **xxx** to your team ID value.
   * `"newThermostatValue": 68` — Replace **68** with a value to which you would like to see if you can adjust the thermostat.

3. Click **Submit**.

![Submit ChangeThermostatTemp](images/Part1_Step32.png)







* If you select a temperature for the thermostat that is not within 3 degrees of the `sensorTemp` value, then you will get an error message like the one below. If you get this message, enter another value and click submit.

  ![ChangeThermostatTemp Error Message](images/Part1_Step32_errormsg.png)

* If you do have permission to adjust the thermostat, you will be returned back to the transaction registry where you can see the data you just submitted.

![Successful Transaction](images/Part1_Step32_success.png)

* If for some reason you forget to modify your teamID value or update it to the wrong value, you will see an error like the one shown below. Check your value for teamID and try again.

![Asset does not exist error message](images/Part1_Step33AssetError.png)











33. Verify that the last transaction updated your asset. Click **Team**.

![Click Team](images/Part1_Step33.png)













34. Verify that the `thermostatTemp` attribute for your Team has been updated to the value you gave successsfully in the `ChangeThermostatTemp` transaction.

* <u>Note:</u> Look back at step 25 and see that the `thermostatTemp` value was 71 before.

![Verify thermostatTemp value](images/Part1_Step34.png)











35. Time to work with the `CompareWeather` transaction. Click **Submit Transaction**.

![Click Submit Transaction](images/Part1_Step35.png)













36. Select **CompareWeather** from the *Transaction Type* drop down.

![Select CompareWeather](images/Part1_Step36.png)













37. Complete the **CompareWeather** transaction.

    a. Fill in the following fields in the JSON for **CompareWeather**:

    * `"asset": "resource:org.acme.sample.Team#teamID:xxx"`— Replace **xxx** with your team ID.
    * `"outsideTemp": 0`— Enter a value for an outside temperature.
    * `"feelsLike": 0` — Enter a value for what temperature it could feel like outside.

    b. Click **Submit**.

    ![Complete CompareWeather](images/Part1_Step37.png)









38. Verify that your transaction is showing in the Transaction Registry.

![Transaction Registry](images/Part1_Step38.png)





39. Click on **Team**. 

![Click Team](images/Part1_Step39.png)









40. Verify there is now a message in the `recommendation`variable in your Team asset and that the `thermostatValue` has been updated to the recommended value.
    * <u>Note:</u> This application was developed for temperatures in Celsius. The CompareWeather transaction and recommendation result are based on Celsius. If you use Fahrenheit, you'll see results like below.

![Team asset recommendationv value](images/Part1_Step40.png)











41. Continue testing your code for all scenarios to understand what your contract(s) can do. The hints to the remaining scenarios are as follows: (Yes, you'll have to look at the Script File under the Define Tab to figure out the criteria.)

    1. ChangeThemostatTemp:
       - [ ] A successful transaction where the `thermostatValue` is updated in the Team asset.
       - [ ] An error message in the *Submit Transaction* window advising you do not have permission to adjust the thermostat.
    2. CompareWeather:
       -[ ] A transaction based on `outsideTemp` values where it is really hot.
       -[ ] A transaction based on `outsideTemp` values where it is quite nice.
       -[ ] A transaction based on `outsideTemp` values where it is cold.
       -[ ] A transaction based on `feelsLike` values where it hot.
       -[ ] A transaction based on `feelsLike` values where it is quite nice.
       -[ ] A transaction based on `feelsLike` values where it is cold.

    * <u>Note:</u> You should verify that your asset values have been updated appropriately after each transaction like you did in prior steps.







### End of Part 1







