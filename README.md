
# System Design Concepts

## Overview

## What is System Design?

System Design is the process of **planning and structuring a software system** so that it:

* Works correctly
* Handles many users
* Scales when traffic increases
* Stays reliable
* Is easy to maintain

Think of it like this:

If coding is **building a room**,
System design is **planning the entire building** — where the doors go, how electricity flows, where plumbing runs, how many floors it can support.

---

## In simple words

System Design answers questions like:

* How will users interact with the system?
* Where will the data be stored?
* How will different services communicate?
* What happens if 1 million users come at the same time?
* What happens if one server crashes?

It’s about **big-picture architecture**.

---

## Real World Example

Imagine you're building **Instagram**.

System design decisions include:

* Where are photos stored? (Cloud storage like S3)
* How do we serve millions of feeds quickly?
* How do we handle notifications?
* How do we scale when traffic spikes?
* How do we cache frequently accessed data?

You’re not writing functions here — you're designing the structure of the entire system.

---

## Main Components of System Design

Here are common building blocks:

* **Frontend** – What users see
* **Backend** – Business logic
* **Database** – Data storage
* **Cache** – Faster access (Redis)
* **Load Balancer** – Distributes traffic
* **CDN** – Faster content delivery
* **Message Queues** – Async processing
* **Microservices** – Breaking system into smaller services

---

## Use Cases of System Design

### 1️⃣ Building Scalable Applications

If you’re building:

* E-commerce website
* Social media app
* Banking system
* Ride sharing app

You need system design to make sure it handles:

* High traffic
* Data consistency
* Reliability

---

### 2️⃣ Designing APIs for Large Systems

When creating:

* REST APIs
* Microservices architecture
* Backend for mobile apps

You must design:

* How services communicate
* How failures are handled
* How scaling works

---

### 3️⃣ Performance Optimization

When your app becomes slow:

System design helps you:

* Add caching
* Use database indexing
* Introduce load balancing
* Add sharding
* Use CDNs

---

### 4️⃣ Handling Large Data

For:

* Analytics systems
* Logging systems
* Streaming platforms (like Netflix)

You design:

* Distributed databases
* Data pipelines
* Batch vs real-time processing

---

## Why It’s Important for us (especially as a dev)

System design will help us:

* Move from mid-level to senior
* Think beyond writing APIs
* Design systems that handle real-world scale
* Understand cloud architecture (AWS etc.)

It’s literally the bridge between “developer” and “architect”.

---

## Small Example (Practical Thinking)

Let’s say your API is slow.

Without system design thinking:

> “Maybe optimize code.”

With system design thinking:

* Should I add Redis cache?
* Is DB indexed?
* Should I split service?
* Do I need read replicas?
* Is N+1 query happening?
* Should I use CDN?

See the difference? 🔥

---

## In One Line

System Design is about designing software systems that are scalable, reliable, and efficient — not just writing code.

---

## Single Server Setup

## 🔹 PART 1 — Summary of the Tutorial

## 1️⃣ Start with a Simple System (Single User + Single Server)

* One user (Laptop / Mobile)
* One Web Server
* User types a domain (example.com)
* DNS converts domain → IP address
* Request goes to Web Server
* Server sends response back
* User sees webpage/app response

Very basic flow:

```
User → DNS → Server → Response → User
```

---

## 2️⃣ What is Domain Name?

* Domain name = Human readable name
* Example: google.com
* Servers understand only IP addresses
* Example IP: 142.250.182.14

We type:

```
www.google.com
```

But internally it becomes:

```
142.250.182.14
```

---

## 3️⃣ What is DNS?

DNS = Domain Name System
It converts domain name → IP address.

It is usually a third-party service.

Example in Node.js:

```js
const dns = require('dns');

dns.lookup('google.com', (err, address) => {
    console.log(address);
});
```

Output:

```
142.250.182.14
```

---

## 4️⃣ What is Traffic?

Traffic = Number of requests coming to your server.

Example:

* 1 user → 1 request
* 1000 users → 1000 requests

Restaurant example:

* 1 table → 1 customer → easy
* 1 table → 100 customers → problem

Same with servers.

---

## 5️⃣ Where Does Traffic Come From?

Traffic comes from:

* Web Applications (Browser)
* Mobile Applications

---

## 6️⃣ How Web Applications Work

Frontend:

* HTML
* CSS
* JavaScript

Backend:

* Node.js
* Java
* Python
* Django
* Express etc.

Example Simple Express Server:

```js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hello Single User!');
});

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

Open in browser:

```
http://localhost:3000
```

---

## 7️⃣ How Mobile Apps Talk to Server

Mobile apps use:

* HTTP / HTTPS protocol
* Send requests
* Receive response in JSON format

Example API response:

```json
{
  "id": 1,
  "name": "Armaan",
  "age": 25
}
```

---

## 8️⃣ What is JSON?

JSON = JavaScript Object Notation
Used to send structured data.

Example:

```js
const user = {
    id: 1,
    name: "Armaan",
    age: 25
};

console.log(JSON.stringify(user));
```

---

## 9️⃣ Problem with Single Server

If traffic increases:

* Server slows down
* Crashes
* Cannot handle requests

One server is NOT enough for:

* Millions of users
* Billion-dollar systems

---

## 🔹 Concept 1: Client–Server Architecture

Client = User device
Server = Machine that processes request

Example:

```js
// Client side fetch request
fetch('http://localhost:3000')
  .then(res => res.text())
  .then(data => console.log(data));
```

Server:

```js
app.get('/', (req, res) => {
    res.send('Hello Client');
});
```

Flow:

```
Client → Request → Server → Response → Client
```

---

## 🔹 Concept 2: HTTP Protocol

HTTP = How client & server talk.

Basic Example:

```
GET /users HTTP/1.1
Host: example.com
```

Server Response:

```
HTTP/1.1 200 OK
Content-Type: application/json
```

Express Example:

```js
app.get('/users', (req, res) => {
    res.json([{ name: "Armaan" }]);
});
```

---

## 🔹 Concept 3: IP Address

Two types:

* IPv4 → 192.168.0.1
* IPv6 → 2001:db8::1

Example server running on IP:

```
http://192.168.1.10:3000
```

---

## 🔹 Concept 4: Web vs Mobile Traffic

Both send HTTP requests.

Example from Mobile (React Native):

```js
fetch('https://api.example.com/users')
```

Same backend handles both.

---

## 🔹 Concept 5: Scaling Problem

If 10 users:

* Single server works fine.

If 1 million users:

* Server crashes
* High CPU usage
* Memory full

---

## What Comes Next (Scaling Preview)

To scale system, we need:

* Load Balancer
* Multiple Servers
* Database
* Caching
* CDN
* Auto Scaling

---

### 📌 Important Pointers (Interview Ready Notes)

- Domain name is human readable
- DNS converts domain → IP
- Server understands only IP
- Client sends HTTP request
- Server returns HTTP response
- Data usually sent in JSON
- Traffic = number of requests
- Single server = limited capacity
- More users → need scaling

---

## 🧠 Basic flow of application on web

1. User types domain
2. DNS resolves to IP
3. Request goes to server
4. Server processes logic
5. Server sends response
6. Client renders result

---

## Database & Multiple Servers

Initially:

* We had **1 user + 1 server**
* That works only for small traffic
* Not suitable for millions of users

Now:

* We improved architecture
* We separated:

  * Application Server (handles traffic)
  * Database Server (stores data)
* Now both can scale independently

Next topics mentioned:

* How to choose the right database
* What is scaling?
* Types of scaling:

  * Vertical Scaling
  * Horizontal Scaling

---

## Important Concepts Explained Clearly

## 1️⃣ Why Single Server is Not Enough?

Earlier architecture:

```
User → Server (handles traffic + logic + database)
```

Problems:

* CPU overload
* Memory overload
* Database queries slow everything
* One failure = whole system down

This is called a **monolithic single-server bottleneck**.

---

## 2️⃣ Separating Application Server and Database Server

New Architecture:

```
User
   ↓
Application Server
   ↓
Database Server
```

Now:

* App server handles:

  * Requests
  * Business logic
  * API responses

* Database server handles:

  * Data storage
  * Queries
  * Transactions

This is called **Separation of Concerns**.

---

## 3️⃣ Why Separation Helps?

Because now:

✔ We can scale app server separately
✔ We can scale database separately
✔ App server crash ≠ database crash
✔ Better performance

This is the first step toward scalable architecture.

---

## 🔹 Basic Example (Node + Database)

### Application Server (Node.js + Express)

```js
const express = require('express');
const app = express();
const mysql = require('mysql2');

const db = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: 'password',
    database: 'users_db'
});

app.get('/users', (req, res) => {
    db.query('SELECT * FROM users', (err, results) => {
        if (err) throw err;
        res.json(results);
    });
});

app.listen(3000, () => {
    console.log('App server running on port 3000');
});
```

Here:

* Node server handles request
* MySQL handles data
* Both are separate services

---

## 4️⃣ Independent Scaling (Very Important Interview Point)

Because they are separate:

If traffic increases:

* Add more Application Servers

If database becomes slow:

* Upgrade database machine
* Add replicas

This is the core idea.

---

## 5️⃣ What is Scaling?

Scaling = Increasing system capacity to handle more traffic.

Two main types:

---

## 6️⃣ Vertical Scaling (Scale Up)

You increase power of the same machine.

Example:

* Add more RAM
* Add more CPU
* Upgrade to better server

Diagram:

```
Old Server → Bigger Server
```

Example:

```
8GB RAM → 32GB RAM
```

Advantages:

* Simple
* Easy to implement

Disadvantages:

* Has limit
* Expensive
* Single point of failure still exists

---

## 7️⃣ Horizontal Scaling (Scale Out)

You add more machines instead of upgrading one.

Diagram:

```
        Load Balancer
            ↓
   Server1   Server2   Server3
```

This is how big companies scale.

Advantages:

* No single bottleneck
* High availability
* Can handle millions of users

Disadvantages:

* More complex
* Requires load balancer

---

## 🔹 Basic Load Balancer Example (Conceptual)

Using Node Cluster (Simple Simulation)

```js
const cluster = require('cluster');
const os = require('os');
const express = require('express');

if (cluster.isMaster) {
    const cpuCount = os.cpus().length;

    for (let i = 0; i < cpuCount; i++) {
        cluster.fork();
    }
} else {
    const app = express();

    app.get('/', (req, res) => {
        res.send('Handled by worker ' + process.pid);
    });

    app.listen(3000);
}
```

This simulates horizontal scaling on same machine.

---

## 8️⃣ Choosing the Right Database (Interview Gold)

Different databases serve different needs.

## SQL Databases

* MySQL
* PostgreSQL

Use when:

* Structured data
* Relationships important
* ACID compliance needed

Example:

* Banking system
* E-commerce orders

---

## NoSQL Databases

* MongoDB
* Redis
* Cassandra

Use when:

* Huge scale
* Flexible schema
* Fast reads/writes

Example:

* Social media
* Real-time apps

---

## Interview Question:

"Which database will you choose and why?"

Your answer should depend on:

* Type of data
* Read-heavy or write-heavy?
* Consistency requirement?
* Scalability need?

---

## Updated Architecture Diagram

Final improved version from tutorial:

```
User
   ↓
Application Server
   ↓
Database Server
```

Next step (future improvement):

```
Users
   ↓
Load Balancer
   ↓
Multiple App Servers
   ↓
Database Cluster
```

---

## 📌 Important Interview Pointers

- Single server is not scalable
- Separate app server and database
- Independent scaling is key
- Vertical scaling = bigger machine
- Horizontal scaling = more machines
- Database choice depends on use case
- Always design for failure

---

## 🧠 If Interviewer Asks:

"How will you scale a single server system?"

You say:

1. Separate database from application server
2. Add load balancer
3. Add multiple application servers
4. Scale database (replication/sharding)

That’s strong system design thinking.

---

## Which Database to use ?

## 🔹 Summary of This Tutorial

Previously:

* We separated Application Server and Database Server.

Now:

* We must choose which type of database to use.

There are two main types:

1. Relational Database (SQL / RDBMS)
2. Non-Relational Database (NoSQL)

Key discussion points:

* What is RDBMS?
* What is NoSQL?
* Differences
* When to use which?
* Interview perspective

---

## 🔥 1️⃣ Relational Database (RDBMS)

Also called:

* SQL Database
* Relational Database Management System

Examples:

* MySQL
* PostgreSQL
* Oracle
* SQL Server

---

## ✅ How Relational Database Works

* Data stored in tables
* Tables contain rows and columns
* Fixed schema
* Supports JOIN operations
* Uses SQL language

Example Table:

### Users Table

| id | name   | age |
| -- | ------ | --- |
| 1  | Armaan | 25  |

### Orders Table

| id | user_id | product |
| -- | ------- | ------- |
| 1  | 1       | Laptop  |

---

## 🔹 JOIN Operation (Very Important)

You can combine tables:

```sql
SELECT users.name, orders.product
FROM users
JOIN orders ON users.id = orders.user_id;
```

This is powerful for relational data.

---

## 🔹 Basic SQL Example

Create table:

```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  name VARCHAR(100),
  age INT
);
```

Insert:

```sql
INSERT INTO users VALUES (1, 'Armaan', 25);
```

Query:

```sql
SELECT * FROM users;
```

---

## 🔹 When to Use Relational Database?

Use RDBMS when:

- Data is structured
- Relationships are important
- Strong consistency required
- ACID properties needed
- Financial / transactional systems

Example:

* Banking
* E-commerce orders
* Payment systems

---

## 2️⃣ Non-Relational Database (NoSQL)

NoSQL = Not Only SQL

Examples:

* MongoDB (Document-based)
* Redis (Key-value)
* Cassandra (Column-based)
* Neo4j (Graph-based)

---

## 🔹 Types of NoSQL Databases

1. Key-Value Store (Redis)
2. Document Store (MongoDB)
3. Column Store (Cassandra)
4. Graph Database (Neo4j)

---

## Document Database Example (MongoDB)

Data stored as JSON-like documents.

Example:

```json
{
  "name": "Armaan",
  "age": 25,
  "orders": [
    { "product": "Laptop", "price": 80000 }
  ]
}
```

No fixed schema required.

---

## 🔹 MongoDB Example (Node.js)

Insert document:

```js
const { MongoClient } = require('mongodb');

const client = new MongoClient('mongodb://localhost:27017');

async function run() {
    await client.connect();
    const db = client.db('testDB');
    const users = db.collection('users');

    await users.insertOne({
        name: "Armaan",
        age: 25
    });

    console.log("User inserted");
}

run();
```

---

## Major Differences: SQL vs NoSQL

| Feature      | SQL                 | NoSQL                   |
| ------------ | ------------------- | ----------------------- |
| Schema       | Fixed               | Flexible                |
| Structure    | Tables              | JSON / Key-value        |
| JOIN Support | Yes                 | Usually No              |
| Scaling      | Harder horizontally | Easier horizontally     |
| Best For     | Structured data     | Large unstructured data |

---

## When Should You Use NoSQL?

Use NoSQL when:

- Data is unstructured
- You don’t want fixed schema
- High scalability needed
- Very large data
- Low latency requirement
- Rapid development

Example:

* Social media
* Real-time chat
* Large analytics systems
* Big data applications

---

## Why Big Systems Prefer NoSQL?

Because:

* Flexible schema
* Easier horizontal scaling
* Handles massive data
* Good performance at scale

Example:
Instagram, Facebook, Netflix use NoSQL in parts of their systems.

---

## Important Interview Question

Interviewer asks:

"Which database will you choose and why?"

Correct approach:

You do NOT say randomly.

You analyze:

1. What type of data?
2. Is it structured?
3. Are relationships important?
4. Is strict consistency needed?
5. How much scale?
6. Read-heavy or write-heavy?

Then answer accordingly.

---

## Example Interview Answer

If designing:

## 🏦 Banking App

“I will use PostgreSQL because strong consistency, ACID transactions and relationships are important.”

---

## 📱 Social Media App

“I will use MongoDB or Cassandra because schema flexibility and horizontal scalability are important.”

---

## Real-World Example from Tutorial

Large e-commerce platform:

Each customer document may contain:

* Name
* Address
* Order history
* Payment info

If millions of users → huge data → NoSQL preferred for scalability.

---

## ACID (Important for SQL)

Relational databases support:

* Atomicity
* Consistency
* Isolation
* Durability

Example (Transaction):

```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

This ensures safe money transfer.

---

## Big Picture Architecture

If building large system:

```
Users
   ↓
Load Balancer
   ↓
Application Servers
   ↓
Database (SQL or NoSQL)
```

Database choice depends on use case.

---

## 📌 Important Interview Pointers

- RDBMS = structured + relations
- NoSQL = flexible + scalable
- SQL supports JOIN
- NoSQL often avoids JOIN
- SQL good for transactions
- NoSQL good for massive unstructured data
- Always choose database based on use case

---

## 🧠 Final Mindset Shift

Good engineer asks:

Not:
“Which database is best?”

But:
“Which database fits this problem?”

That’s system design thinking.

---
