
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

See the difference? 

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

## 1️⃣ Relational Database (RDBMS)

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

## Vertical Scaling vs Horizontal Scaling

## 🔹 Summary of This Tutorial

You have a service.

It becomes popular.

Millions of users start sending requests.

Now your system must:

* Handle high traffic
* Stay fast (low latency)
* Stay available (not crash)

To increase system capacity, we use **Scaling**.

There are two types:

1. Vertical Scaling (Scale Up)
2. Horizontal Scaling (Scale Out)

Each has advantages and limitations.

---

## What is Scaling?

Scaling = Increasing system capacity to handle more traffic and users.

If:

* 100 users → small server works
* 1 million users → need bigger system

---

## 1️⃣ Vertical Scaling (Scale Up)

Also called:

* Scaling Up

### What does it mean?

You increase power of the same server.

Example:

* Add more CPU
* Add more RAM
* Add more storage

---

### Visual Idea

Before:

```
[ Server ]
```

After:

```
[ Bigger Server with more CPU + RAM ]
```

---

### Example in Real Terms

Old server:

* 2 CPU cores
* 4GB RAM

Upgrade to:

* 16 CPU cores
* 64GB RAM

---

### Why It’s Simple?

Because:

* No architecture changes
* No load balancer
* No distributed system complexity

---

### Basic Simulation Example (Node.js)

If your app is slow due to CPU limits:

```bash
# Start Node with more memory
node --max-old-space-size=4096 app.js
```

Or upgrade cloud instance:

AWS:

```
t2.micro → t2.large
```

Simple upgrade.

---

### Limitations of Vertical Scaling

1. There is a hardware limit
   You cannot add unlimited RAM or CPU.

2. Single Point of Failure
   If server crashes → entire system goes down.

3. Expensive

4. Not suitable for massive applications

---

## 2️⃣ Horizontal Scaling (Scale Out)

Also called:

* Scaling Out

### What does it mean?

Instead of upgrading one server,
You add multiple servers.

---

### Visual Idea

Before:

```
[ Server ]
```

After:

```
        Load Balancer
              ↓
   Server1   Server2   Server3
```

Now traffic is distributed.

---

## Why Horizontal Scaling is Powerful

If:

* 1 server handles 1000 requests/sec
* 10 servers handle 10,000 requests/sec

It scales with growth.

---

## Basic Horizontal Scaling Example (Node Cluster)

Simulate multiple processes:

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
        res.send(`Handled by worker ${process.pid}`);
    });

    app.listen(3000);
}
```

This runs multiple worker processes (horizontal style on same machine).

---

## Why We Need Load Balancer

When multiple servers exist:

We need something to distribute traffic.

Example Concept:

```js
// pseudo example
function loadBalancer(request) {
    if (server1.isFree()) return server1;
    else return server2;
}
```

In real world:

* Nginx
* AWS ELB
* HAProxy

---

## When to Use Vertical Scaling?

Use when:

* Traffic is low to medium
* Startup stage
* Simplicity is important
* Budget limited
* System is small

---

## When to Use Horizontal Scaling?

Use when:

* Millions of users
* High traffic
* High availability required
* Cannot afford downtime
* Enterprise-level system

---

## Very Important: Single Point of Failure

In vertical scaling:

```
Only 1 server
```

If it crashes → full system down.

In horizontal scaling:

```
Multiple servers
```

If one crashes → others handle traffic.

That’s called **High Availability**.

---

## Real Interview Thinking

Interviewer asks:

“How would you scale your system?”

Good Answer Structure:

1. Start with vertical scaling for small traffic.
2. Move to horizontal scaling for large traffic.
3. Add load balancer.
4. Add database replication.
5. Add monitoring.

---

## Why Big Applications Use Horizontal Scaling?

Because:

* Unlimited scaling possible
* Fault tolerance
* No single server dependency
* Better reliability

Companies like:

* Google
* Amazon
* Netflix
* Instagram

Use horizontal scaling heavily.

---

## 📌 Important Interview Pointers

- Scaling = increasing capacity
- Vertical scaling = upgrade same machine
- Horizontal scaling = add more machines
- Vertical scaling has hardware limits
- Horizontal scaling removes single point of failure
- Load balancer required for horizontal scaling
- Large systems prefer horizontal scaling

---

## Comparison Summary

| Feature      | Vertical              | Horizontal       |
| ------------ | --------------------- | ---------------- |
| Method       | Increase server power | Add more servers |
| Complexity   | Simple                | Complex          |
| Limit        | Hardware limit        | Almost unlimited |
| Failure Risk | High                  | Low              |
| Used For     | Small systems         | Large systems    |

---

## 🧠 Final System Design Mindset

Small app → Vertical scaling
Growing app → Horizontal scaling
Large app → Distributed architecture

Scaling is not about “making server bigger”.
It is about designing system to grow safely.

---

## Load Balancer ⚖️

## 🔎 What This Tutorial Is Explaining (Summary)

The video explains:

1. ❌ Problem with users directly connecting to a single web server
2. ❌ Issues when server goes down or traffic increases
3. ✅ Solution: Use a Load Balancer
4. ✅ Add multiple web servers (Horizontal Scaling)
5. 🌐 Public IP vs Private IP concept
6. ⚠️ Still a problem: Single database is a SPOF (Single Point of Failure)
7. ➜ Need database scaling / replication (next logical step)

---

## 1️⃣ Problem: Users Directly Connected to Web Server

### Architecture:

```
Users → Web Server → Database
```

### Problems:

### 1. If server goes down

* All users lose service.
* Complete downtime.

### 🚦 2. If too many users connect at same time

* Server has limited CPU, RAM, connections.
* It may:

  * Respond slowly
  * Crash
  * Reject connections

This is called:

> **Single Point of Failure (SPOF)**

---

## 2️⃣ Solution: Load Balancer

Instead of:

```
Users → Server
```

We do:

```
Users → Load Balancer → Multiple Web Servers
```

## What Load Balancer Does

* Distributes incoming traffic
* Prevents overloading a single server
* Improves availability
* Automatically routes traffic to healthy servers

---

# 3️⃣ Load Balancer Architecture

```
Users → (Public IP) → Load Balancer
Load Balancer → (Private IPs) → Web Servers
```

## Important Concept: Public vs Private IP

### 🌍 Public IP

* Used by clients (browser/mobile app)
* Accessible from internet

### 🔒 Private IP

* Used inside internal network
* Not accessible from internet
* Used for:

  * Load balancer → servers
  * Server → database communication

---

## 4️⃣ Horizontal Scaling

Instead of increasing server size (vertical scaling), we:

Add more servers.

```
Server 1
Server 2
Server 3
```

Load balancer distributes traffic among them.

### Benefits:

* High availability
* Better performance
* Easy scaling when traffic increases

---

## 5️⃣ Health Checks

If one server goes down:

Load balancer detects it and stops sending traffic to it.

Example:

```
Server 1 ❌ (Down)
Server 2 ✅
Server 3 ✅
```

Traffic goes only to healthy servers.

---

## 6️⃣ But Still a Problem: Single Database

Even if we scale web servers:

```
Users
  ↓
Load Balancer
  ↓
Web Servers
  ↓
Single Database ❌
```

If database goes down:

* Entire system fails

This is another **Single Point of Failure**.

---

## Now Let’s Explain Important Concepts with Basic Code Examples

---

## 🧠 1. Basic Web Server (Node.js Example)

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send("Hello from Server 1");
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

This is a single server. If this crashes → service gone.

---

## 🧠 2. Multiple Servers (Simulating Horizontal Scaling)

Server 1:

```javascript
app.listen(3001);
```

Server 2:

```javascript
app.listen(3002);
```

Now we have 2 servers running.

---

## 🧠 3. Simple Load Balancing (Round Robin Example in Node.js)

Basic example using http-proxy:

```javascript
const http = require('http');
const httpProxy = require('http-proxy');

const proxy = httpProxy.createProxyServer();
const servers = ['http://localhost:3001', 'http://localhost:3002'];

let current = 0;

http.createServer((req, res) => {
    proxy.web(req, res, { target: servers[current] });
    current = (current + 1) % servers.length;
}).listen(8000);
```

Now:

```
Users → localhost:8000 → Distributed to 3001 & 3002
```

This is **Round Robin Load Balancing**.

---

## 🧠 4. Health Check Example

A load balancer periodically checks:

```javascript
GET /health
```

Server:

```javascript
app.get('/health', (req, res) => {
    res.status(200).send("OK");
});
```

If health check fails → remove server from pool.

---

# 🧠 5. Database as Single Point of Failure

Basic DB usage:

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydb');
```

If MongoDB crashes → all servers fail.

---

## 🧠 6. Database Replication Concept (High Level)

Instead of:

```
1 Database
```

We use:

```
Primary DB
Replica DB 1
Replica DB 2
```

Write → Primary
Read → Replicas

Example concept (MongoDB replica set):

```javascript
mongodb://host1,host2,host3/?replicaSet=myReplicaSet
```

Now if one DB fails → system continues.

---

## Final Architecture (Better Version)

```
Users
   ↓
Load Balancer (Public IP)
   ↓
Web Server 1 (Private IP)
Web Server 2 (Private IP)
Web Server 3 (Private IP)
   ↓
Primary DB
Replica DB
```

---

## 📌 Important Concepts List

* Single Point of Failure
* Horizontal Scaling
* Vertical Scaling
* Load Balancer
* Round Robin
* Health Checks
* Public IP
* Private IP
* High Availability
* Database Replication

---

## 🏗 Real World Example

When you open:

* Amazon
* Netflix
* Instagram

You are NEVER connecting to:

* A single server
* A single database

There are:

* Multiple load balancers
* Hundreds of servers
* Distributed databases

---

## Database Replication (07:29)

Niceee now we’re moving into proper production-level system design.

This part of the tutorial is about **Database Replication (Master–Slave architecture)** — how to prevent database failure from taking down your entire system.

Let’s break it cleanly and professionally.

---

# 🧾 Summary of This Tutorial

After solving:

✅ Traffic problem → using Load Balancer + multiple servers
Now solving:
❗ What if the **database goes down?**

Solution introduced:

> **Database Replication (Master–Slave Architecture)**

Main ideas covered:

1. Master DB handles **write operations**
2. Slave DB(s) handle **read operations**
3. Data from master is replicated to slaves
4. Improves:

   * Performance
   * Reliability
   * High Availability
5. Failover handling:

   * If slave fails → read from master
   * If master fails → promote a slave to master

---

## Problem: Single Database = Single Point of Failure

Even after adding:

```
Users → Load Balancer → Multiple Web Servers → Single DB ❌
```

If DB crashes:

* Entire system fails
* No data access
* No writes
* No reads

This is another **Single Point of Failure (SPOF)**.

---

# 💡 Solution: Database Replication

We create copies of the database.

## Architecture

```
              Web Servers
                    ↓
           ┌───────────────┐
           │   Master DB   │  ← Handles Writes
           └───────────────┘
                    ↓ (Replication)
        ┌───────────────────────┐
        │   Slave DB 1          │ ← Handles Reads
        │   Slave DB 2          │ ← Handles Reads
        └───────────────────────┘
```

---

# 📌 Important Concepts Explained

---

# 1️⃣ Master Database

The master database handles:

* INSERT
* UPDATE
* DELETE

All modifying queries.

Example (Node.js + MySQL):

```javascript
// Write connection (Master DB)
const masterDb = mysql.createConnection({
  host: 'master-db-host',
  user: 'root',
  password: 'password',
  database: 'app_db'
});

// Write operation
masterDb.query(
  "INSERT INTO users (name, email) VALUES (?, ?)",
  ["John", "john@example.com"]
);
```

Only master handles writes.

---

# 2️⃣ Slave Database (Read Replica)

Slave databases:

* Do NOT handle writes
* Only serve SELECT queries
* Continuously sync data from master

Example:

```javascript
// Read connection (Slave DB)
const slaveDb = mysql.createConnection({
  host: 'slave-db-host',
  user: 'root',
  password: 'password',
  database: 'app_db'
});

// Read operation
slaveDb.query(
  "SELECT * FROM users WHERE id = ?",
  [1],
  (err, result) => {
    console.log(result);
  }
);
```

---

# 3️⃣ Replication Process

Whenever something changes in master:

```
INSERT / UPDATE / DELETE
```

Master sends those changes to slaves.

This happens:

* Continuously
* Automatically
* In background

Example (MongoDB Replica Set connection string):

```javascript
mongoose.connect(
  "mongodb://db1,db2,db3/?replicaSet=myReplicaSet"
);
```

Mongo handles replication internally.

---

## 4️⃣ Why More Slaves Than Master?

In real applications:

👉 Read operations >> Write operations

Example:

* Instagram
* Amazon
* YouTube

Millions of:

* Profile views
* Product views
* Feed loads

But fewer:

* Profile updates
* Product edits

So we scale read capacity by adding more slaves.

---

## 🚀 Advantages of Database Replication

## ✅ 1. Better Performance

Reads distributed across slaves:

Instead of:

```
1 DB handling 10,000 reads/sec ❌
```

We get:

```
Slave1 → 3000 reads
Slave2 → 3000 reads
Slave3 → 4000 reads
```

Load divided → faster response time.

---

## ✅ 2. Reliability

If one slave crashes:

```
Slave1 ❌
Slave2 ✅
Slave3 ✅
```

System still works.

---

## ✅ 3. High Availability

If master fails:

We can:

👉 Promote a slave to become new master.

This is called:

> **Failover**

---

## 🔄 Failover Scenario

## Case 1: Slave goes down

Solution:

* Redirect reads to master temporarily
* Add a new slave

---

## Case 2: Master goes down

Steps:

1. Pick a slave
2. Promote it to master
3. Reconfigure replication
4. Add a new slave later

⚠️ In real production systems this is complex:

* Risk of data inconsistency
* Split brain issues
* Partial writes
* Recovery scripts needed

Tools that handle this:

* MongoDB Replica Set
* MySQL Group Replication
* AWS RDS Multi-AZ
* Kubernetes operators

---

## 🏗 Final Improved Architecture

```
Users
   ↓
Load Balancer (Public IP)
   ↓
Web Server 1
Web Server 2
Web Server 3
   ↓
Master DB (Write)
   ↓
Slave DB 1 (Read)
Slave DB 2 (Read)
Slave DB 3 (Read)
```

Now we solved:

✅ Traffic scaling
✅ Web server failures
✅ Database failure risk
✅ Read performance bottleneck

---

# 📊 Key Interview Concepts From This Topic

Make sure you remember these terms:

* Database Replication
* Master–Slave Architecture
* Read Replica
* Write Operations
* Read Operations
* Failover
* High Availability
* Data Consistency
* Replication Lag
* Single Point of Failure

---

## ⚠️ Important Real-World Problem: Replication Lag

Replication is not always instant.

If:

1. User updates profile (write to master)
2. Immediately reads profile
3. Read hits slave
4. Slave hasn’t updated yet

User sees old data.

Solution strategies:

* Read-after-write consistency (read from master)
* Sticky sessions
* Semi-synchronous replication

---

## 🎯 Big Picture

Before:

```
Single Server + Single DB = Fragile System
```

Now:

```
Load Balancer + Multiple Servers + Replicated DB = Production-ready architecture
```

---

## 👀 What Comes Next?

At the end, tutorial hints at:

> How to further improve response time?

Next logical topic:

* Caching (Redis, Memcached)
* CDN
* Query optimization
* Indexing

---

## Caching (7:12)

## 🧾 Summary of This Tutorial

So far we already fixed:

✅ Traffic problem → Load Balancer + Multiple Web Servers
✅ Database failure problem → Master–Slave Replication

Now question:

> Can we improve response time even more?

Answer: **YES — Using Cache**

Main ideas covered:

1. What is caching?
2. Why caching improves performance
3. Read-through caching pattern
4. When to use cache
5. Cache expiration policy
6. Cache consistency
7. Multiple cache servers (avoid SPOF)
8. Cache eviction policies (LRU, LFU, FIFO)

---

## 🚀 What is Cache?

Cache = Temporary high-speed storage.

It stores:

* Results of expensive database queries
* Frequently accessed data

Instead of hitting database every time, we serve data from cache.

---

## 🏗 Architecture with Cache

Before:

```
Web Server → Database
```

After:

```
Web Server → Cache → Database
```

Flow:

1. Check cache first
2. If found → return immediately
3. If not found → fetch from DB
4. Store in cache
5. Return response

---

## Why Cache is Important

Without cache:

* Every request hits database
* DB becomes overloaded
* Slower response time

With cache:

* Faster responses
* Less DB load
* Better scalability

---

## 📌 What Does Cache Store?

1. Results of expensive queries
2. Frequently accessed data

Example:

* User profile
* Product details
* Homepage feed
* Config settings

---

## 🧠 Read-Through Cache Pattern

This tutorial explains:

> Read-Through Caching

### Process:

1. Web server checks cache
2. If data exists → return
3. If not → read from DB
4. Store in cache
5. Return to user

---

## 💻 Basic Code Example (Node.js + Redis)

Install Redis client:

```bash
npm install redis
```

### Setup Redis

```javascript
const redis = require("redis");
const client = redis.createClient();

client.connect();
```

---

### Read-Through Cache Example

```javascript
async function getUser(userId) {
  const cacheKey = `user:${userId}`;

  // 1. Check cache
  let cachedUser = await client.get(cacheKey);

  if (cachedUser) {
    console.log("Cache hit");
    return JSON.parse(cachedUser);
  }

  console.log("Cache miss");

  // 2. Fetch from database
  const user = await database.getUserById(userId);

  // 3. Store in cache (with expiration)
  await client.set(cacheKey, JSON.stringify(user), {
    EX: 60 // expire in 60 seconds
  });

  return user;
}
```

---

## ⏳ TTL (Time To Live) / Expiration

Cache should not live forever.

Too short:

* Cache expires quickly
* DB still overloaded

Too long:

* Data becomes stale (outdated)

Example:

```javascript
await client.set("key", "value", {
  EX: 300  // expire after 5 minutes
});
```

---

## 🧠 When Should You Use Cache?

Use cache when:

✅ Data is read frequently
✅ Data changes rarely
✅ DB queries are expensive

Example:

* Product catalog
* Public profiles
* Blog posts

Avoid cache when:
❌ Data updates constantly
❌ Strong consistency required

---

## 🔄 Cache Consistency Problem

Problem:

1. Data updated in DB
2. Cache still has old value

User sees stale data.

Solution options:

1. Delete cache after DB update
2. Update cache after DB update
3. Short TTL

Example (Invalidate cache after update):

```javascript
async function updateUser(userId, newData) {
  await database.updateUser(userId, newData);

  // Delete cached value
  await client.del(`user:${userId}`);
}
```

---

## 🚨 Avoid Single Point of Failure (SPOF)

If you use only:

```
1 Cache Server
```

And it crashes → entire system slows down.

Solution:

Use multiple cache servers.

```
Web Servers
     ↓
  Cache Cluster
     ↓
 Database
```

Tools:

* Redis Cluster
* Memcached cluster

---

## 🗑 Cache Eviction Policies

When cache memory is full, we must remove old entries.

Common eviction policies:

---

## 1️⃣ LRU (Least Recently Used)

Remove data not used recently.

Most popular in real systems.

---

## 2️⃣ LFU (Least Frequently Used)

Remove data used least number of times.

---

## 3️⃣ FIFO (First In First Out)

Remove oldest inserted data.

---

Example Redis config:

```bash
maxmemory-policy allkeys-lru
```

---

## ⚡ Final Architecture Now

```
Users
   ↓
Load Balancer
   ↓
Multiple Web Servers
   ↓
Cache (Redis Cluster)
   ↓
Master DB (Write)
   ↓
Slave DBs (Read)
```

Now system is:

✅ Fast
✅ Scalable
✅ Fault tolerant
✅ High availability
✅ Optimized for reads

---

## 🎯 Key Interview Terms From This Topic

Make sure you remember:

* Caching
* Read-through cache
* Cache hit
* Cache miss
* TTL (Time to Live)
* Cache invalidation
* Eviction policy (LRU, LFU, FIFO)
* Cache consistency
* Cache cluster
* Single Point of Failure

---

## 🧠 Why Big Companies Use Cache

Instagram, Amazon, Netflix:

* Millions of reads per second
* Impossible to serve all from database
* Redis & Memcached heavily used

---

## 📊 Performance Comparison

Without cache:

```
Response time = DB query time (slow)
```

With cache:

```
Response time = Memory lookup time (very fast)
```

Memory access is thousands of times faster than disk.

---

## Big Picture Progression

1️⃣ Single server
2️⃣ Horizontal scaling
3️⃣ Load balancer
4️⃣ DB replication
5️⃣ Cache layer

Now you're building real production architecture knowledge 🚀

---

## CDN (Content Delivery Network) (07:56)

## 📌 1. What This Tutorial Covers

The video explains:

1. Static vs Dynamic content
2. What is CDN
3. How CDN works
4. CDN request flow
5. Cost considerations
6. Expiration time (TTL)
7. CDN fallback strategy
8. File invalidation & versioning
9. Final system architecture after adding CDN

---

## 📌 2. Static vs Dynamic Content

Understanding this is very important.

## 🔹 Static Content

Content that does NOT change frequently.

Examples:

* Images
* Videos
* CSS files
* JavaScript files
* Public documents
* Book cover images

These are ideal for CDN.

---

## 🔹 Dynamic Content

Content that changes based on user or request.

Examples:

* User dashboard
* Personalized feed
* Cart items
* Account balance
* Search results

These are usually served by web servers.

---

## 📌 3. What is CDN?

CDN = **Content Delivery Network**

It is a network of distributed servers across different geographic locations.

Its job:

> Store and deliver static content from the nearest server to the user.

---

## 📌 4. Why CDN is Important

Distance matters.

If your server is in the US:

* US user → Fast response
* India user → Slow response

CDN solves this by placing servers globally.

So:

* User gets content from nearest location
* Lower latency
* Faster load time
* Reduced load on web server

---

## 📌 5. How CDN Works (Step-by-Step Flow)

Let’s say a user requests an image:

### Step 1:

User → CDN

### Step 2:

If CDN has image → return immediately (CDN hit)

### Step 3:

If CDN does NOT have image:

* CDN requests it from Web Server
* Web Server sends image
* CDN stores it temporarily
* CDN sends it to user

Next time:

* Directly served from CDN

---

## 📌 6. Simple Architecture With CDN

```
User
   ↓
DNS
   ↓
Load Balancer
   ↓
Web Server
   ↓
Database
```

After adding CDN:

```
User
   ↓
CDN (Static Content)
   ↓
Load Balancer
   ↓
Web Server (Dynamic Content)
   ↓
Database
```

---

## 📌 7. Basic Example (Node.js Static File + CDN)

Suppose your app serves images.

### Normal Static Serving:

```javascript
const express = require("express");
const app = express();

app.use("/static", express.static("public"));

app.listen(3000, () => {
  console.log("Server running");
});
```

Now instead of:

```
https://myapp.com/static/logo.png
```

You configure CDN like:

```
https://cdn.myapp.com/logo.png
```

CDN will:

* Fetch from origin server
* Cache it
* Serve globally

---

## 📌 8. CDN Expiration (TTL)

Just like cache, CDN content should expire.

If TTL too short:

* CDN keeps fetching from server
* Server load increases

If TTL too long:

* Stale content problem

Example HTTP header:

```javascript
app.use((req, res, next) => {
  res.set("Cache-Control", "public, max-age=3600");
  next();
});
```

Meaning:

* Cache for 1 hour

---

## 📌 9. CDN Cost Consideration

CDN providers charge based on:

* Data transfer
* Requests count
* Geographic region

So:

❌ Do NOT store rarely used content
✅ Store frequently accessed static content

Examples of CDN providers:

* Cloudflare
* AWS CloudFront
* Akamai
* Fastly

---

## 📌 10. CDN Fallback Strategy

What if CDN goes down?

System must:

* Automatically fallback to origin server

Meaning:

```
If CDN fails → Web Server serves content directly
```

Always design fallback.

---

## 📌 11. File Invalidation

Problem:

You updated an image.

But CDN still has old version.

Solutions:

---

## 🔹 1. Manual Invalidation

Most CDN providers allow:

* Purge cache
* Invalidate specific file

Example:

```
Purge: /images/logo.png
```

---

## 🔹 2. File Versioning (Best Practice)

Instead of:

```
logo.png
```

Use:

```
logo_v2.png
```

OR

```
logo.png?v=2
```

Now CDN treats it as new file.

Example:

```html
<img src="https://cdn.myapp.com/logo.png?v=2" />
```

This forces CDN to fetch new version.

---

## 📌 12. Full Final Architecture After All Improvements

Now system becomes:

```
Users
   ↓
DNS
   ↓
CDN (Static)
   ↓
Load Balancer
   ↓
Multiple Web Servers (Dynamic)
   ↓
Cache (Redis)
   ↓
Master DB (Writes)
   ↓
Slave DBs (Reads)
```

---

## 📌 13. What We Improved Step-by-Step

| Layer            | Purpose                         |
| ---------------- | ------------------------------- |
| Load Balancer    | Traffic distribution            |
| Multiple Servers | Horizontal scaling              |
| DB Replication   | Read scaling                    |
| Cache            | Faster DB reads                 |
| CDN              | Faster static delivery globally |

---

## 📌 14. Interview Important Terms

Make sure you remember:

* Static content
* Dynamic content
* CDN
* Edge server
* Origin server
* Latency
* TTL
* CDN hit / miss
* Invalidation
* Versioning
* Fallback strategy
* Geo-distributed network

---

## 📌 15. Why Big Companies Use CDN

Netflix, Amazon, Instagram use CDN because:

* Millions of global users
* Need low latency worldwide
* Cannot serve static content from single data center

CDN reduces:

* Server load
* Bandwidth cost
* Latency

---

## 📌 16. Final Big Picture (System Design Growth)

1️⃣ Single server
2️⃣ Horizontal scaling
3️⃣ Load balancer
4️⃣ DB replication
5️⃣ Cache layer
6️⃣ CDN layer

Now you are designing production-level scalable systems 🚀

---
