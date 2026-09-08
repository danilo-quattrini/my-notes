---
created: 2026-03-10T12:06:00
tags:
  - baby
topics:
  - "[[Front-end]]"
  - "[[Programming]]"
author: Danilo Quattrini
---
# Redis and Laravel - A Complete Developer Guide

---

## Table of Contents

1. [What is Redis?](#1-what-is-redis)
2. [Traditional Database vs Redis](#2-traditional-database-vs-redis)
3. [Using Redis in Laravel](#3-using-redis-in-laravel)
4. [Real-Life Use Cases](#4-real-life-use-cases)
5. [Best Practices and Common Pitfalls](#5-best-practices-and-common-pitfalls)
6. [Quick Reference](#6-quick-reference)

---

## 1. What is Redis?

Redis, which stands for *Remote Dictionary Server*, is an open-source, in-memory data structure store. Unlike a traditional relational database that reads and writes data to disk, **Redis keeps everything in RAM**. This makes it exceptionally fast, typically responding in under a millisecond.

Redis was created by Salvatore Sanfilippo in 2009. It is now maintained by Redis Ltd and is one of the most popular databases in the world, used by companies like Twitter, GitHub, Airbnb, and Stack Overflow.

### 1.1 Core Concepts

**Key-Value Store:** Every piece of data is stored under a unique key. There are no tables, no rows, no schemas. You set a key, you get a value back. This simplicity is what makes Redis so fast and predictable.

**In-Memory:** Data lives in RAM, not on disk. Reading from RAM is orders of magnitude faster than reading from a spinning disk or even an SSD. This is the fundamental reason Redis can respond in microseconds where a traditional database takes milliseconds.

**Data Structures:** Redis is not just a simple key-value cache. It natively supports multiple data structures including strings, hashes, lists, sets, sorted sets, bitmaps, and streams. Each structure has its own set of atomic commands, which means Redis can do in one operation what would require multiple queries in SQL.

**Optional Persistence:** By default, Redis is in-memory only, but you can configure it to persist data to disk using RDB snapshots (point-in-time dumps at intervals) or AOF (Append-Only File, which logs every write command). This lets you recover data after a restart if needed.

**Single-Threaded Command Processing:** Redis processes commands one at a time in a single thread. This design avoids the complexity of locks and race conditions that plague multi-threaded systems. Each command is atomic by nature.

### 1.2 What Redis is NOT

Redis is not a replacement for your primary database. It does not support complex SQL queries, joins, or full relational integrity. You cannot run a SELECT with a WHERE clause across multiple fields the way you can in MySQL or PostgreSQL.

Think of Redis as a high-speed layer that sits alongside your database, not instead of it. Your relational database remains the source of truth for persistent application data. Redis handles the fast, ephemeral, or frequently-accessed layer on top.

### 1.3 Supported Data Types

```
String      Simple scalar values. Can be text, integers, or binary data up to 512 MB.
Hash        A map of field-value pairs. Ideal for representing objects like a user profile.
List        An ordered collection of strings, implemented as a linked list.
Set         An unordered collection of unique strings.
Sorted Set  Like a set but each member has a floating-point score used for ordering.
Bitmap      A string treated as an array of bits. Useful for tracking boolean states at scale.
Stream      An append-only log data structure, similar to a lightweight Kafka topic.
```

---

## 2. Traditional Database vs Redis

Understanding the difference between a relational database like MySQL or PostgreSQL and Redis is essential to using both effectively. They are complementary technologies, not competing ones.

|Criteria|Traditional Database (MySQL)|Redis|
|---|---|---|
|Storage Type|Persistent disk (HDD/SSD)|In-memory (RAM)|
|Read Speed|~1-10ms (disk I/O)|~0.1ms (sub-millisecond)|
|Data Persistence|Full persistence by default|Optional (RDB / AOF)|
|Data Structure|Tables, rows, columns|Strings, hashes, lists, sets, sorted sets|
|Primary Use Case|Persistent application data|Cache, sessions, queues, pub/sub|
|Scaling Model|Vertical scaling, read replicas|Horizontal clustering native|
|Query Language|SQL|Redis commands (GET, SET, HGET, etc.)|
|Transactions|Full ACID compliance|Optimistic (WATCH / MULTI / EXEC)|
|Laravel Driver|mysql / pgsql / sqlite|redis (predis or phpredis)|

### 2.1 When to Use Each

Use your relational database when you need to store users, products, orders, or any data that must survive indefinitely and remain consistent. Use it when you need complex queries with joins, filters, and aggregations. Use it when data integrity rules like foreign keys and cascading deletes are important.

Use Redis when you need to cache the result of expensive database queries to avoid repeating them. Use it for session storage where fast read and write access per request matters. Use it for rate limiting, job queues, background processing, real-time leaderboards, pub/sub messaging, and live counters. Any data that is either short-lived or needs to be accessed with very low latency is a good candidate for Redis.

### 2.2 Connection Model Comparison

MySQL and PostgreSQL connect via TCP to a database server. The server authenticates the connection, then processes queries against data stored on disk. Each connection has overhead in terms of memory and CPU on the server, which is why connection pooling tools like PgBouncer exist. Query execution involves parsing SQL, planning an execution strategy, and then performing disk reads.

Redis also connects via TCP, using port 6379 by default. However, once connected, all commands operate against data already in RAM. There is no query planner, no disk seek, and no schema validation. The server reads the command, finds the key in its in-memory hash table, and returns the result immediately. This makes individual Redis connections lighter and responses faster than any disk-based database can achieve.

# Reference
---

