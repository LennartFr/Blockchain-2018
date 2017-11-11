# Blockchain-2018-v1

## [Decentralized Energy with Hyperledger Composer](https://developer.ibm.com/code/patterns/decentralized-energy-hyperledger-composer/)


### [Get the Code](https://github.com/IBM/Decentralized-Energy-Composer?cm_sp=IBMCode-_-decentralized-energy-hyperledger-composer-_-Get-the-Code)

### Step 1: Design the app

### Step 2: App components

### Step 3: Composer .BNA file

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










### Step 4: Install Hyperledger Fabric

### Step 5: Launch .bna file on Hyperledger Fabric

### Step 6: Add the GUI

### Step 7: Run the app




# Sources on Blockchain



[edX MOOC: Blockchain for Business - An Introduction to Hyperledger Technologies](https://www.edx.org/course/blockchain-business-introduction-linuxfoundationx-lfs171x)
