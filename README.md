---
languages:
- python
page_type: sample
description: "This is a basic example of using Apache Spark on HDInsight to stream data from Kafka to Azure Cosmos DB."
products:
- azure
- azure-hdinsight
- azure-cosmos-db
---

# Use Apache Kafka with Apache Spark on hdinsight

This is a basic example of using Apache Spark on HDInsight to stream data from Kafka to Azure Cosmos DB. This example uses Spark Structured Streaming and the [Azure Cosmos DB Spark Connector](https://github.com/Azure/azure-cosmosdb-spark). 

This example requires Kafka and Spark on HDInsight 3.6 in the same Azure Virtual Network. It also requires an Azure Cosmos DB SQL API database.

__NOTE__: Apache Kafka and Spark are available as two different cluster types. HDInsight cluster types are tuned for the performance of a specific technology; in this case, Kafka and Spark. To use both together, you must create an Azure Virtual network and then create both a Kafka and Spark cluster on the virtual network. 

The `azuredeploy.json` template file in this repo creates Kafka and Spark clusters in HDInsight, inside an Azure Virtual Network. It also creates an Azure Cosmos DB account.

__IMPORTANT__: For a more detailed walkthrough of using this project, see the [Use Spark Structured Streaming with Kafka and Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/hdinsight/apache-kafka-spark-structured-streaming-cosmosdb) document.

## Deploy Azure resources

To create an environment that can be used to run this example, use the __Deploy to Azure__ button to deploy the following Azure resources:

* A virtual network

* Spark on HDInsight 3.6

* Kafka on HDInsight 3.6

* Azure Cosmos DB SQL API database

When the template loads, you must provide the following information:

* __Cosmos DB account name__: The name of the Cosmos DB account that is created.

* __Base cluster name__: This must be a unique alphanumeric value, and is used to generate the following resource names:

    * Virtual Network: __basename-network__
    * Spark on HDInsight: __spark-basename__

    * Kafka on HDInsight: __kafka-basename__

    * Azure Storage Account: __basenamestore__

* __Cluster login name__: This is the name used when logging in to Jupyter notebooks on the Spark cluster.

* __Cluster login password__: The password for the login account.

* __SSH user name__: The SSH user account for the cluster.

* __SSH password__: The SSH user password.

__NOTE__: SSH isn't used by this example, but you must still provide these values.

__NOTE__: This template creates an Azure Virtual Network with an IP address space of 10.0.0.0\16.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fhdinsight-spark-scala-kafka-cosmosdb%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

## Understand this example

This example uses a Scala application in a Jupyter notebook. The code in the notebook relies on the following pieces of data:

* __Kafka brokers__: The broker process runs on each workernode on the Kafka cluster. The list of brokers is required by the producer component, which writes data to Kafka.

* __Topic name__: The name of the topic that data is written to and read from. The default name used in the example is `tripdata`.

* __Cosmos DB endpoint__: The HTTPS endpoint used to connect to Cosmos DB.

* __Master key__: The key used to authenticate requests to the endpoint.

* __Database__: The name of the Cosmos DB SQL API database that data is written to.

* __Collection__: The document collection within the database.

* __PreferredRegions__: The preferred Azure regions to use when writing to the database.

__NOTE__: The notebooks contain information and links on how to obtain this information.

__WARNING__: HDInsight is charged hourly. To prevent unnecessary costs, delete the cluster once you are finished with this example.

## To run this example

To use the example Jupyter notebooks, you must upload them to the Jupyter Notebook server on the Spark cluster. Use the following steps to upload the notebooks:

1. In your web browser, use the following URL to connect to the Jupyter Notebook server on the Spark cluster. Replace __CLUSTERNAME__ with the name of your Spark cluster.

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    When prompted, enter the cluster login (admin) and password used when you created the cluster.

2. From the upper right side of the page, use the __Upload__ button to upload the `Stream-taxi-data-to-Kafka.ipynb` file. Select the file in the file browser dialog and select __Open__. 

3. Find the __Stream-taxi-data-to-Kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.

4. Once the file has uploaded, select the __Stream-taxi-data-to-kafka.ipynb__ entry to open the notebook. To load data into Kafka, follow the instructions in the notebook.

5. Repeat steps 1-3 to upload the `Stream-data-from-Kafka-to-Cosmos-DB.ipynb` document to Kafka. Once the file has uploaded, select the entry to open the notebook. Follow the instructions in the notebook to read the data from Kafka and store it into Cosmos DB.
