## ** Work in Progress **
# Postgre SQL Database as a Fabric Certificate Wallet 

Security on the Hyperledger Fabric is enforced with digital signatures. All requests made to the fabric must be signed by users with appropriate enrolment certificates. Once user is enrolled, Node js application persist certificate in wallet for future usages.

Fabric Node SDKs provide default file system wallet for storing fabric certificate. File system wallet stores user certificate in folders. This approach does not provide required security and flexibility to maintain certificate like generation of new certificate for enrolled users (if any modification to blockchain network) or unregistering user from blockchain. File system wallet also impact scalability as production projects grow.

Fabric Node SDK provides a way to store certificates in Couch DB but not in Postgres. There is not direct provision to store enrolment certificates to Postgres database. Postgres database support SQL and NoSQL data storing and has strong community support. Postgres database provides more flexibility compared to Couch db. Also, PostgreSQL provides cost effective alternative. This pattern demonstrates how to use Postgre SQL db as Certificate Wallet using Nodejs SDK.

At the end of this code pattern, users will understand - how to use postgre sql db as a fabric certificate wallet using node js SDK.

# Flow

# Pre-requisites

* [IBM Cloud Account](https://cloud.ibm.com)
* [Git Client](https://git-scm.com/downloads) - needed for clone commands.
* [Node js](https://nodejs.org/en/download/) - 8.9 or greator

# Steps

Follow these steps to setup and run this code pattern. The steps are described in detail below.
1. [Get the code](#1-get-the-code)
2. [Create IBM Cloud Services](#2-create-ibm-cloud-services)
3. Set up the Hyperledger Fabric Network
4. [Set up Postgre SQL DB](#4-set-up-postgresql-db)
5. Update connection profile and credentials
6. Run the application


## 1. Get the code

- Clone the repo using the below command.
   ```
   git clone https://github.com/IBM/fabric-postgres-wallet.git
   ```

## 2. Create IBM Cloud Services

**Create IBM Kubernetes Service Instance**

Create a Kubernetes cluster with [Kubernetes Service](https://cloud.ibm.com/containers-kubernetes/catalog/cluster) using IBM Cloud Dashboard.

  ![Kubernetes Service](images/create_kubernetes_service.png)

  > Note: It can take up to 15-20 minutes for the cluster to be set up and provisioned.  

**Create IBM Blockchain Platform Service Instance**

Create [IBM Blockchain Platform Service](https://cloud.ibm.com/catalog/services/blockchain-platform) instance using IBM Cloud Dashboard.

![Blockchain Platform](images/create_IBP_service.png)

## 3. Setup

In this step, we will setup the Hyperledger Fabric network using IBM Blockchain Platform. 


The network should consist of two organizations with single peer each and an orderer service for carrying out all the transactions. For detailed steps, please refer to the [quick start guide](https://developer.ibm.com/tutorials/quick-start-guide-for-ibm-blockchain-platform/) for IBM Blockchain Platform.

## 4. Set up PostgreSQL DB
There are two approaches to set up PostgreSQL DB instance -
* **IBM PostgreSQL service** - IBM cloud provide PostgreSQL as service, type postgreSQL in catlog search box and create PostgreSQL instance. once service is created, navigate to left menu and create service credentials.
* **PostgreSQL as container**- PostgreSQL can also be deployed as container. pull postgreSQL docker image from docker hub.
```
docker pull postgres:[tag_you_want]
```
 start container with appropriate username, password and db name - for example
```
docker run --rm   --name pg-docker -e POSTGRES_PASSWORD=docker -e POSTGRES_USER=postgres -e POSTGRES_DB=walletdb -d -p 5432:5432 -v /postgreSQL-docker/volume:/var/lib/postgresql/data  postgres
```

## 5. Update connection profile and credentials
after setting up fabric network and postgreSQL DB mentioned in step 3 and 4, Please replace ```server/config/connection-profile.json```  and ```server/config/local-postgres-config.json``` with your fabric network connection profile and postgreSQL credentials(in case of IBM cloud postgreSQL service). current postgresconfig contains postgreSQL credentials for dockurized postgreSQL.

## 6. Run the application
to run application, first install npm dependencies with cmd ``` npm install```. after installing all dependencies successfully, run app with following cmd ```npm start```. server will start running, visit [localhost:3000](http://localhost:3000/) for api swagger. 


## Learn More

* [Quick start guide for IBM Blockchain Platform](https://developer.ibm.com/tutorials/quick-start-guide-for-ibm-blockchain-platform/)


<!-- keep this -->
## License

This code pattern is licensed under the Apache Software License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1 (DCO)](https://developercertificate.org/) and the [Apache Software License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache Software License (ASL) FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)

