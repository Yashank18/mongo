## 1. WiredTiger Engine Files
### WiredTiger
- Purpose:
This file is the main metadata file for the WiredTiger engine. It stores configuration settings and metadata essential for WiredTiger to manage the data store.

### WiredTiger.wt
- Purpose:
The primary data file that contains a large part of the database's actual data managed by the WiredTiger storage engine.

### WiredTiger.lock
- Purpose:
A lock file to ensure that only one instance of the MongoDB server (mongod) is accessing the data directory. This prevents corruption from simultaneous writes.

### WiredTiger.turtle
- Purpose:
A small metadata file used by WiredTiger to store essential, frequently accessed configuration and state information. Despite its small size, it plays a critical role in engine startup.

### WiredTigerHS.wt
- Purpose:
The History Store file. WiredTiger uses multiversion concurrency control (MVCC) to handle concurrent operations, and the history store maintains previous versions of data pages for supporting point-in-time reads and transactions.


## 2. MongoDB Data Files
### _mdb_catalog.wt
- Purpose:
This file stores the metadata catalog for MongoDB. It keeps track of all collections and indexes defined in the database, acting as a central registry for the data stored.
- Collection Files
Files like the following represent individual collections:

    collection-0-15344230373835763432.wt collection-2-15344230373835763432.wt collection-4-15344230373835763432.wt 
    - Explanation:
        - The prefix collection indicates that the file stores data for a MongoDB collection.
        - The number immediately following (e.g., 0, 2, 4) is an internal collection identifier. These IDs are sequentially assigned as collections are created.
        - The long numeric string (e.g., 15344230373835763432) is a unique identifier (often derived from timestamps or a unique counter) ensuring that file names do not conflict across restarts and migrations.
- Index Files
Similarly, index files follow a naming pattern:
    index-1-15344230373835763432.wt index-3-15344230373835763432.wt index-5-15344230373835763432.wt index-6-15344230373835763432.wt
    - Explanation:
        - The prefix index designates that the file holds index data for a collection.
        - The number after index- (e.g., 1, 3, 5, 6) is the internal index identifier. These numbers are part of a counter that often aligns with the collection's creation order and how many indexes exist on a collection.
        - The same long numeric identifier seen in collection files ensures that the index file is uniquely associated with the corresponding collection.
### sizeStorer.wt
- Purpose:
This file maintains statistics about the size of collections and indexes. This helps MongoDB optimize queries and storage allocation by keeping track of data size information without scanning entire files each time.

### storage.bson
- Purpose:
A BSON file that stores storage metadata. This file contains additional configuration and state information about the storage engine and its data layout.