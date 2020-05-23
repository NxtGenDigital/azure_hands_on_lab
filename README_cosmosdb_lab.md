# Getting started with Cosmos notebooks

In this notebook, we'll learn how to use Cosmos notebook features. We'll create a database and container, import some sample data in a container in Azure Cosmos DB and run some queries over it.

# Getting started with Cosmos notebooks

In this notebook, we'll learn how to use Cosmos notebook features. We'll create a database and container, import some sample data in a container in Azure Cosmos DB and run some queries over it.

```
import azure.cosmos
from azure.cosmos.partition_key import PartitionKey

database = cosmos_client.create_database_if_not_exists('RetailDemo')
print('Database RetailDemo created')

container = database.create_container_if_not_exists(id='WebsiteData', partition_key=PartitionKey(path='/CartID'))
print('Container WebsiteData created')
```

#### Set the default database and container context to the new resources

We can use the ```%database {database_id}``` and ```%container {container_id}``` syntax.
