# MongoDB Indexes Overview

Indexes in MongoDB play a crucial role in optimizing query performance. By creating indexes, you can drastically reduce the number of documents that MongoDB scans when processing queries. This lesson covers the various types of indexes available in MongoDB, along with their key characteristics and use cases.

## 1. Single Field Index
- Description:

    A single field index is the most basic type of index, created on a single field in a collection. It helps speed up queries that match on that field.

- Use Cases:
    - Optimizing queries that search for a specific value or range of values in one field.

- Considerations:
    - Indexes incur storage overhead and can affect write performance, so they should be used judiciously.

## 2. Compound Index
- Description:
    A compound index is created on multiple fields within a collection. It can support queries that match on all the indexed fields or a prefix of them.

- Use Cases:

    - Queries that filter or sort on multiple fields.
    - Optimizing queries that use a combination of fields in the query predicate.

- Considerations
    - The order of fields in a compound index is significant. Queries can only efficiently use the index if they include a prefix of the indexed fields in the same order.

## 3. Multikey Index
- Description:

A multikey index is used to index fields that contain arrays. MongoDB automatically creates a multikey index when an indexed field contains an array.

- Use Cases:

    - Querying documents where the indexed field is an array.

- Considerations:

    - Each element in the array is indexed, which might increase index size.
    - There are limitations on creating compound multikey indexes if more than one field in the index contains an array.

## 4. Text Index

- Description:

Text indexes are used to support text search queries on string content. They index the content of string fields for full-text search.

- Use Cases:

    - Implementing search features for applications, such as searching for keywords in documents.

- Considerations:

    - Only one text index is allowed per collection.
    - Text indexes support stemming and stop words based on language settings.

## 5. Hashed Index

- Description:

Hashed indexes store a hash of the value of a field. They are primarily used for sharding, where the hashed value of the shard key determines data distribution.

- Use Cases:

    - Sharding: Distributing data evenly across a sharded cluster.
- Considerations:

    - Hashed indexes are not suitable for range queries because the hash function destroys ordering.
    - They offer good distribution of documents but are more limited in their query capabilities.

## 6. Geospatial Indexes
MongoDB supports several types of geospatial indexes to efficiently query location-based data.

### 6.1. 2d Index
- Description:
Supports legacy coordinate pairs for planar (flat) geometry.

- Use Cases:

    - Queries on legacy geospatial data with simple coordinate pairs.
- Considerations:

    - Best suited for legacy applications and simple 2D geometries.

### 6.2. 2dsphere Index

- Description:
Supports queries that calculate geometries on an earth-like sphere. This index is used for location-based queries that require spherical calculations.

- Use Cases:

    - Geo-queries using GeoJSON objects.
    - Applications that require accurate results for locations on a globe.

- Considerations:
    More versatile than 2d indexes and supports a wider range of geometries.

## 7. TTL (Time To Live) Index
- Description:
A TTL index automatically removes documents from a collection after a specified period. It is commonly used to manage data that only needs to be kept for a limited time.

- Use Cases:

    - Managing session data, cache data, or logs that expire after a certain time.

- Considerations:
    - The TTL value is defined in seconds, and MongoDB periodically checks for expired documents.

## 8. Sparse Index
- Description:
A sparse index only indexes documents that contain the indexed field. This can be useful when a field does not exist in every document.

- Use Cases:

    - Optimizing queries on fields that are not present in every document.
- Considerations:

    - Sparse indexes do not index documents that lack the indexed field, so queries expecting a full scan may miss some documents.

## 9. Partial Index
- Description:
A partial index indexes a subset of the documents in a collection, defined by a filter expression. This can reduce index size and improve performance.

- Use Cases:

    - When you want to index only documents that meet specific criteria.
- Considerations:

    - Ensure that queries use the same filter criteria to leverage the index.

## 10. Summary
In this lesson, we covered:

- Single Field Index: Indexing a single field for basic query optimization.
- Compound Index: Indexing multiple fields to support multi-field queries.
- Multikey Index: Indexing array values.
- Text Index: Full-text search support for string content.
- Hashed Index: Hashing field values, primarily for sharding.
- Geospatial Indexes:
    - 2d Index: For legacy, planar geometry.
    - 2dsphere Index: For spherical geometry queries.
- TTL Index: Automatically expiring documents.
- Sparse Index: Indexing only documents with the indexed field.
- Partial Index: Indexing a subset of documents based on a filter.

Understanding these various index types is crucial for optimizing query performance and effectively managing data in MongoDB. In the next lesson, we will provide practical examples for creating and using these indexes.

Happy indexing!