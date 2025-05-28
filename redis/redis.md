Redis (REmote DIctionary Server) is an **in-memory key-value store** used as a database, cache, and message broker.
It is extremely fast due to its in-memory nature and supports a variety of data structures

##  Core Concepts
### 1. **Key-Value Store**

- Like a `Map<String, Object>` in Java.
- Example:
    ```shell
    SET name "rey"
    GET name           # returns "rey"
    ```
### 2. **Data Structures**
Redis supports:
- **String** – basic value.
- **List** – ordered list of strings.
- **Set** – unordered unique elements.
- **Hash** – like a map/dictionary.
- **Sorted Set (ZSet)** – set with score-based ordering.
- **Bitmaps, HyperLogLogs, Streams** – for advanced use cases.

---

## Persistence Options
1. **RDB (Redis Database Backup)** – saves snapshots periodically.
2. **AOF (Append Only File)** – logs every write operation.

---
## Common Use Cases
- Caching (e.g., frequently accessed DB queries)
- Session storage
- Leaderboards (using ZSets)
- Pub/Sub messaging
- Rate limiting
---
## Redis vs Other DBs

| Feature         | Redis           | MongoDB / SQL        |
| --------------- | --------------- | -------------------- |
| Storage         | In-memory       | Disk-based           |
| Speed           | Very high       | Slower comparatively |
| Use Case        | Cache, Realtime | Persistent data      |
| Data Durability | Optional        | Guaranteed           |
