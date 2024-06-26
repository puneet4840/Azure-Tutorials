# Azure Storage

### What is Azure Storage?

Azure Storage is a cloud storage solution provided by azure.

### Types of Azure Storage

4 types of Azure storage:

1 - Blob Storage.

2 - File Share.

3 - Queue.

4 - Table.

**Blob Storage**

Blob (Binary Large Objects) is a storage solution to store large amount of unstructured data. It stores the data like videos, text files, images, hard drives, code(python, java,etc), any type of data we can store in blob storage.

**File Share**

It is a cloud based file storage solution. It stores data in the form of organized file structure as of our pc. It can share the file share using SMB (Server Message Block) protocal at anywhere in the world.

**Tables**

It is a storage service used to store structured No SQL data. Imagine data organized in rows and columns, like a spreadsheet and excel.

**Queues**

Queue is to store and retrieve the messages. Queue message is up to 64 kb in size. Queues are generally used to store lists of messages to be processed asynchronously.

### Storage Access Tier

Three types of access tiers:

1 - Hot.

2 - Cool.

3 - Archive.

**Hot Tier**

It is used when data is access more frequently that you need to use quickly. it is costly.

**Cool Tier**

Is is used when data is accessed less frequently.

**Archive Tier**

Is is used when data is rarely accessed.

### Storage Replication

Storage replication is to make multiple copies of your data in the same region, different region for high availability and durability.

**Locally Redundant Storage (LRS)**

It makes 3 copies of data in the 3 storage boxes the same data center.

**Zone Redundant Storage (ZRS)**

It makes 3 copies of data in multiple data centers in the same region.

**Geo Redundant Storage (GRS)**

It creates 3 copies of data in the primary geo location and other 3 copies in the secondary location.
