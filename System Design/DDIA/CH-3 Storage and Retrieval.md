
Database point of view

Discuss about storage engines optimized for **Transactional workloads** and for **analytics**

**log-structured storage engines**
**page-oriented storage engines**

for log oriented db_get(key) takes O(n) -- linear search
data structure used to improve search:  ***index***

general idea - keep some additional metadata on the side

overhead - slows down writes as we need to update index also 
that's why dbs don't index everything by default, manually add the indexes based on our query patterns


### Hash Indexes

key | byteoffset 

every key mapped to byte offset of data file - location of value


Append only logs - add new line for records even if duplicate records is present

How to handle running out of disk space ?
log into segments of certain size, then perform Compaction (throwing away duplicate keys and keeping only most recent update for each key).

Hash Index Limitations 
1. Hash table must fit in memory. (RAM) because it performs lot of random disk I/O
2. Range of queries are not efficient.


### SSTables and LSM-Trees

SSTables - Sorted String table

Tree based ds to store sorted by key data - red-black trees or AVL trees. Insert keys in any order and read them back in sorted order.

For compaction also as records are sorted we can use algorithm like mergesort.

in-memory balanced rb tree (sometimes called memtable)


LSM-tree 

Log Structured Merge-Tree 

**Sparse Index** store key and offset values for few of the records in sparse table to find the key by the range of offset between two key offset if exist.


LSM Tree algorithm will be slow when looking up keys that don't exist - need to search segment all way to the oldest 

To overcome this we use **Bloom Filters**

Bloom filter is memory-efficient data structure for approximating contents of set. It can tell if key exist in db.


LSM-Trees - Keeping cascade of SSTables that are merged in the background.


### B-Trees

The most widely used indexing structure

B-Trees break the databases into fixed size blocks or pages and read or write one page at a time.


Each page can be identified using an address or location, which allows one page to refer another - similar to pointer. Eventually we get down to page containing individual keys ( a leaf page).

leaf page - either contains value for each key inline or contains references to the pages containing values.

B-tree with n keys - Depth (Ologn)

Write Ahead Log (WAL) - To prevent database crashes during overwrite parent page and splitting child pages.

Concurrency required to prevent threads seeing trees in inconsistent state while updating. latches(lightweight-locks) used for concurrency.


