# Simple explanation for Singleton Pattern

## 🔍 When to Use Singleton?

- When only one instance should ever exist(e.g, Database Connection, Logger, Config Manager, Thread Pool Manager).
- When global shared access is needed.
- When managing resources carefully matters.

## **Situation:** You're Creating a Database Connection Manager.

You need a connect your application to a Database.
Simple - You Write: **DatabaseConnection conn = new DatabaseConnection();**

**🚨 The Problem Start**
- Different parts of your app start creating their own separate connections.
- You realize each connection is expensive(memory, network sockets, auth).
- **Worse:** two object might not even know they've working with different connections - leading to weird bugs like dirty ready, locks, race conditions.

Now you’re stuck debugging issues that feel random but are actually because you have multiple instances of something that should have been only one.

**❗ What's Really Wrong?**
- Multiple instances of something that should be shared.

- Wasted resources (memory, DB connections).

- Inconsistent behavior across modules.

- Testing & debugging get harder.

**🛠️ How Singleton Pattern Fixes This**

**Singleton says:** "There should be exactly ONE object of this class — ever. And everyone should share it."



**Here’s what the Singleton Pattern does:**

- Creates the instance only once.

- Reuses the same instance throughout the application.

- Provides a controlled, centralized access point.

**✅ Benefits**
- One DB connection = less resource usage.

- Everyone shares the same configuration.

- Behavior is predictable and consistent.


``` 
class DatabaseConnection {
  // Step 1: Private static instance variable
  private static instance: DatabaseConnection;

  // Step 2: Private constructor
  private constructor() {
    console.log('Connected to the Database.');
  }

  // Step 3: Public method to access the single instance
  public static getInstance(): DatabaseConnection {
    if (!DatabaseConnection.instance) {
      DatabaseConnection.instance = new DatabaseConnection();
    }
    return DatabaseConnection.instance;
  }

  // Example method
  public query(sql: string): void {
    console.log(`Executing query: ${sql}`);
  }
}

const db1 = DatabaseConnection.getInstance();
const db2 = DatabaseConnection.getInstance();

db1.query('SELECT * FROM products');

console.log(db1 === db2); // true – same instance

```
