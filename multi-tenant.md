# Multi-Tenant Architecture

## Overall

![Database Tenants](https://i.postimg.cc/VLjVRn21/multi-tenant.jpg)

## 1. single database, single schema

![Database Tenants](https://i.postimg.cc/Y9kLBcbh/singal-db-singal-schema.png)

## 2. single database, multiple schemas

![Database Tenants](https://i.postimg.cc/0NS7q0vH/singal-db-multi-schemas.png)

## 3. multiple databases

![Database Tenants](https://i.postimg.cc/nrp42j6S/singal-databases.png)

### 2. Multi-Tenant Database with Multiple Schemas

This guide covers the basics of creating and managing multiple schemas in a single database to support multi-tenant architecture.

#### Steps to Implement Multi-Tenancy

1. **Create the Database**

   ```sql
   CREATE DATABASE multi_tenant_db;

   ```

2. **Connect to the Database**

   ```sql
    \c multi_tenant_db;

   ```

3. **Create Schemas for Tenants**

   ```sql
    CREATE SCHEMA tenant1;
    CREATE SCHEMA tenant2;

   ```

4. **Create Tenant-Specific Tables**

   ```sql
    CREATE TABLE tenant1.users (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100),
     email VARCHAR(100) UNIQUE
   );

   CREATE TABLE tenant2.users (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100),
     email VARCHAR(100) UNIQUE
   );
   ```

5. **Insert Data**

   ```sql
   INSERT INTO tenant1.users (name, email) VALUES ('Alice', 'alice@example.com');
   INSERT INTO tenant2.users (name, email) VALUES ('Bob', 'bob@example.com');

   ```

6. **Query Data**

   ```sql
   SELECT * FROM tenant1.users;
   -- Result: Alice's data

   SELECT * FROM tenant2.users;
   -- Result: Bob's data

   ```

7. **Optional: Set Schema Search Path**

   ```sql
   SET search_path TO tenant1;
   SELECT * FROM users;
   -- Result: Alice's data

   SET search_path TO tenant2;
   SELECT * FROM users;
   -- Result: Bob's data

   ```

8. **Managing Access Control**

   ```sql
     CREATE ROLE tenant1_role;
   GRANT USAGE ON SCHEMA tenant1 TO tenant1_role;
   GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES 			   IN SCHEMA tenant1 TO tenant1_role;

   CREATE ROLE tenant2_role;
   GRANT USAGE ON SCHEMA tenant2 TO tenant2_role;
   GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA tenant2 TO tenant2_role;
   ```

   **Reference:**

Original article available at: [Multi-Tenant Data Architecture](https://web.archive.org/web/20170530080303/https://msdn.microsoft.com/en-us/library/aa479086.aspx)
