---
layout: post
title:  "SQL vs NoSQL"
categories: [ DB , SQL, NoSQL ]
author: Souren
image: assets/images/nosql-vs-sql-overview-1.png
---


---

### **What Defines a Database (DB)?**
A database is defined by its **underlying database engine**, which manages:
- **Data storage**
- **Retrieval**
- **Querying**

**SQL databases** account for approximately **5% of all databases**, with **NoSQL** and other paradigms dominating the rest.

---

### **Myths About NoSQL**
1. **"NoSQL exists because SQL doesn't scale."**
   - **Misleading!** **SQL databases** can scale through **sharding** (partitioning data across nodes).
   - **NoSQL** is often **sharded by default**, creating the perception of inherent scalability.
   - **Constraint**: Scaling **SQL** with **ACID compliance** is more complex than **NoSQL**’s relaxed models.

2. **"SQL databases always use B+ trees."**
   - **Not true!** While **MyISAM** and **InnoDB** (MySQL engines) use **B+ trees** for **O(log n) lookup performance**, you can implement **custom storage engines** with different structures.
   - **Data storage** is flexible, not limited to **B+ trees**.

---

### **SQL vs. NoSQL: Structural Differences**
#### **SQL Databases**
- **Structure**: **Rigid, tabular format** with **predefined schemas**.
- **Storage Engine**: Often uses **B+ trees** (e.g., **InnoDB**, **MyISAM**) for efficient indexing.
- **Guarantees**: **Strong consistency** via **ACID compliance** (Atomicity, Consistency, Isolation, Durability).

#### **NoSQL Databases**
- **Structure**: **Flexible, no standardized schema**. Types include:
  - **NewSQL**: SQL structure with NoSQL scalability.
  - **In-Memory**: RAM-based for speed (e.g., **Redis**).
  - **Key-Value**: Simple pairs (e.g., **DynamoDB**).
  - **Columnar**: Column-based queries (e.g., **Cassandra**).
  - **Document**: Semi-structured data (e.g., **MongoDB** with **WiredTiger** engine).
  - **Hybrid**: Combines multiple paradigms.
- **Guarantees**: Varies—some prioritize **availability** over **consistency** (**CAP theorem**).
- **Engines**: **NoSQL** and **SQL** can share the **same storage engine**. Differences stem from **guarantees** (e.g., distributed, in-memory, centralized, embedded).

---

### **Database Architecture: Abstracted Layers**
A database system uses **modular, plug-and-play layers**:
1. **Physical Layer**: Manages **storage** on disk/devices (e.g., **allocating space**, **reading/writing**).
2. **Storage Engine Layer**: Handles **data structures**, **indexing**, and **retrieval** (e.g., **B+ trees**, **hash tables**).
3. **Query Layer**: **Parses** and **executes queries**, translating commands for the storage engine.
4. **Application Layer**: Provides the **user/application interface** (e.g., **query language**, **API**).

**Key Point**: Layers are **abstracted**, so changes in one (e.g., upgrading the **storage engine**) don’t affect others. **Performance** depends heavily on the **storage layer**.

---

### **Data Storage in B+ Trees**
In **relational databases**:
- A **B+ tree node** contains **one or more rows** of **fixed-width data**, ensuring predictable storage.
- **Multiple rows** can reside in a single node, optimizing **space** and **retrieval**.

In **NoSQL** (e.g., **MongoDB**’s document store):
- **JSON data** appears simple at the **application layer** but is stored in **complex, optimized formats** by the **storage engine** (e.g., **WiredTiger**).

---

### **Indexing in SQL and NoSQL**
**Indexing** improves **read performance** (lookups):
- **Sparse Index**: Stores **indexed values** with **offsets**, reducing **index size**.
- **Dense Index**: Indexes **all values**, increasing size but enabling **faster lookups**.

---

### **Why No Joins in NoSQL?**
**Joins** are computationally expensive in **NoSQL** due to its **distributed nature**:
- **Joins** occur on the **compute layer**, not the **storage engine**.
- In **sharded databases**, data is spread across **multiple nodes**. Joining requires gathering data on a **single machine**, incurring **network overhead**.
- **Alternatives**: **Approximate joins** or **partial joins**.
- **Geo-sharding**: Distributes data across **geographic regions** for **performance** and **availability**, but complicates joins.

---

### **Scaling Reads and Writes**
#### **Master-Slave Architecture**
- **Purpose**: Scales **read operations**.
- **Mechanism**: **Writes** occur on the **master node**, which **replicates** data to **slave nodes** via a **replication log**. **Slaves** handle **reads**.
- **Advantage**: **Reads** are more common, improving **performance**.

#### **Multi-Master Architecture**
- **Purpose**: Scales **reads** and **writes** across **multiple masters**.
- **Challenges**:
  - **Conflict Resolution**: Handling concurrent writes (e.g., **First Write Wins**, **Last Write Wins**, **Concatenation**, or **rejecting conflicts**).
  - **ID Management**: Ensuring **unique IDs** across masters.

---

### **Joins in Distributed Databases**
In **sharded** or **distributed systems**:
- **Data** from multiple nodes is collected on a **single machine** for the **join**.
- The **result** is computed and **redistributed**.
- **Use Case**: Suitable for **analytics** (batch processing), but **not ideal** for **real-time applications** due to **high latency** and **cost**.

---

### **SQL vs. NoSQL: When to Use**
- **SQL Databases**:
  - **Strengths**: **ACID compliance** ensures **strong consistency**, ideal for **transactional systems**.
  - **Best for**: Data under **5TB**, where **sharding** isn’t needed.
  - **Trade-off**: Scaling **distributed SQL** with **ACID** is **slower** due to **distributed transactions**.

- **NoSQL Databases**:
  - **Strengths**: **Flexible schemas**, **built-in sharding**, and **high scalability**.
  - **Best for**: **Large, distributed datasets** needing **high availability** or **eventual consistency**.
  - **Trade-off**: **Weaker consistency** in some cases.

---

### **Key Takeaways**
- **Everything is a trade-off**: **SQL** prioritizes **consistency**; **NoSQL** emphasizes **scalability**.
- The **storage engine** is **critical** to **performance** for both **SQL** and **NoSQL**.
- Understand the **architecture** (**layers**, **indexing**, **sharding**) to choose the **right database** for your **use case**.

---

**Souren**

{% include adsense.html %}
