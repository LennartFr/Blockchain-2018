# Blockchain-2018-v1

## [Decentralized Energy with Hyperledger Composer](https://developer.ibm.com/code/patterns/decentralized-energy-hyperledger-composer/)


### [Get the Code](https://github.com/IBM/Decentralized-Energy-Composer?cm_sp=IBMCode-_-decentralized-energy-hyperledger-composer-_-Get-the-Code)

### Step 1: Design the app

### Step 2: App components

### Step 3: Composer: Model.cto file

~~~
/**
 * Decentalized energy network
 */
namespace org.decentralized.energy.network

participant Resident identified by residentID {
    o String residentID
    o String firstName
    o String lastName
    --> Coins coins
    --> Cash cash
    --> Energy energy
}

participant Bank identified by bankID {
    o String bankID
    o String name
    --> Coins coins
    --> Cash cash
}

participant UtilityCompany identified by utilityID {
    o String utilityID
    o String name
    --> Coins coins
    --> Energy energy
}


enum OwnerEntity {
  o Resident
  o Bank
  o UtilityCompany
}


asset Coins identified by coinsID {
    o String coinsID
    o Double value
    o String ownerID
    o OwnerEntity ownerEntity
    
}

asset Energy identified by energyID {
    o String energyID
    o String units
    o Double value
    o String ownerID
    o OwnerEntity ownerEntity
} 

asset Cash identified by cashID {
    o String cashID
    o String currency
    o Double value
    o String ownerID
    o OwnerEntity ownerEntity
} 


transaction EnergyToCoins {
    o Double energyRate
    o Double energyValue       
    --> Coins coinsInc
    --> Coins coinsDec
    --> Energy energyInc
    --> Energy energyDec
}

transaction CashToCoins {
    o Double cashRate       
    o Double cashValue    
    --> Coins coinsInc
    --> Coins coinsDec
    --> Cash cashInc
    --> Cash cashDec
}
~~~

### Step 4: Install Hyperledger Fabric: download fabric.sh

[Getting started with Hyperledger Fabric](https://medium.com/@gaurangtorvekar/getting-started-with-hyperledger-fabric-ba7efb55b75)

#### A Hyperledger Fabric with only one Peer is referred to as NOOPS and disables consensus. 
It performs no validation. It executes transactions as they arrive.
It is the default mode while the code is in pre-release version.

#### The other option for running the blockchain nodes is with the validating mechanism, which currently uses PBFT (Practical Byzantine Fault Tolerance) for concensus.
To do this, you’ll have to run at least 4 nodes at the same time.

~~~
docker pull hyperledger/fabric-peer:$ARCH-1.0.1 // Peer
docker pull hyperledger/fabric-ca:$ARCH-1.0.1   // Certificate Authority
docker pull hyperledger/fabric-ccenv:$ARCH-1.0.1 // Chaincode Environment
docker pull hyperledger/fabric-orderer:$ARCH-1.0.1 // Orderer
docker pull hyperledger/fabric-couchdb:$ARCH-1.0.1 // Couchdb
~~~

### Step 5: Generate the Business Network Archive
~~~
./startFabric.sh
./createComposerProfile.sh
cd ../
npm install
composer archive create -a dist/decentralized-energy-network.bna --sourceType dir --sourceName .
The composer archive create command has created a file called decentralized-energy-network.bna in the dist folder.
~~~

### Step 6: Deploy the Fabric

~~~
cd dist
composer network deploy -a decentralized-energy-network.bna -p hlfv1 -i PeerAdmin -s randomString -A admin -S
composer network ping -n decentralized-energy-network -p hlfv1 -i admin -s adminpw
~~~


### Chaincode
https://medium.com/@gaurangtorvekar/getting-started-with-hyperledger-fabric-ba7efb55b75
~~~
Start with the ‘chaincode’
Now there are two ways of deploying the chaincode — one through the Command Line, and other through the Node SDK.
In Hyperledger Fabric implementation, a ‘chaincode’ is the actual Smart Contract on the blockchain.
To run through the command line, and get a feel of the chain code, you can start using it directly from the containers you just started
Enter one of the containers by using this command
sudo docker exec -it pbft_vp0_1 bash
First, deploy the chaincode —
peer chaincode deploy -n mycc -p github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02 -c '{"Function":"init", "Args": ["a","100", "b", "200"]}'
Then, invoke the chaincode
peer chaincode invoke -n mycc -c '{"Function": "invoke", "Args": ["a", "b", "10"]}'
Then you can query the chaincode
peer chaincode query -n mycc -c '{"Function": "query", "Args": ["a"]}'

~~~



### Step 6: Add the GUI

### Step 7: Run the app
~~~
cd ../angular-app/
npm install
To start the application:

npm start
~~~



# Sources on Blockchain



[edX MOOC: Blockchain for Business - An Introduction to Hyperledger Technologies](https://www.edx.org/course/blockchain-business-introduction-linuxfoundationx-lfs171x)
