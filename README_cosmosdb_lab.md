# Getting started with Cosmos notebooks

In this notebook, we'll learn how to use Cosmos notebook features. We'll create a database and container, import some sample data in a container in Azure Cosmos DB and run some queries over it.

### step 1 - Create new database and container

To connect to the service, you can use our built-in instance of ```cosmos_client```. This is a ready to use instance of [CosmosClient](https://docs.microsoft.com/python/api/azure-cosmos/azure.cosmos.cosmos_client.cosmosclient?view=azure-python) from our Python SDK. It already has the context of this account baked in. We'll use ```cosmos_client``` to create a new database called **RetailDemo** and container called **WebsiteData**.

Our dataset will contain events that occurred on the website - e.g. a user viewing an item, adding it to their cart, or purchasing it. We will partition by CartId, which represents the individual cart of each user. This will give us an even distribution of throughput and storage in our container. Learn more about how to [choose a good partition key.](https://docs.microsoft.com/azure/cosmos-db/partition-data)

```python
import azure.cosmos
from azure.cosmos.partition_key import PartitionKey

database = cosmos_client.create_database_if_not_exists('RetailDemo')
print('Database RetailDemo created')

container = database.create_container_if_not_exists(id='WebsiteData', partition_key=PartitionKey(path='/CartID'))
print('Container WebsiteData created')
```

### step 2 - Set the default database and container context to the new resources

We can use the ```%database {database_id}``` and ```%container {container_id}``` syntax.

```
%database RetailDemo
```
```
%container WebsiteData
````

### Step 3 - Load in sample JSON data and insert into the container. 

We'll use the **%%upload** magic function to insert items into the container

```
%%upload --databaseName RetailDemo --containerName WebsiteData --url https://cosmosnotebooksdata.blob.core.windows.net/notebookdata/websiteData-small.json
```
A Special note:
The new database and container should show up under the **Data** section. Use the refresh icon after completing the previous cell. 

<img src="https://cosmosnotebooksdata.blob.core.windows.net/notebookdata/refreshData.png" alt="Refresh Data resource tree to see newly created resources" width="60%"/>


### Step 4 - Run a query using the built-in Azure Cosmos notebook magic

```Sql
SELECT c.Action, c.Price as ItemRevenue, c.Country, c.Item FROM c
```

execution result:

 ![exec_result](Image/img1.PNG?raw=true "exec_result")
 
 
 
### Step 5 - Run a query using the built-in Azure Cosmos notebook magic


