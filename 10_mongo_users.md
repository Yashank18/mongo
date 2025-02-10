# MongoDB User Management, Roles, and Permissions

## Introduction to MongoDB Security

MongoDB provides robust security features to protect your data. User management and access control are crucial components of MongoDB security. In this lesson, we will explore how to create and manage users, assign roles and permissions, and secure your MongoDB instances.

## Setting Up MongoDB with Authentication

To enable authentication in MongoDB, you need to modify the MongoDB configuration file (`mongod.conf`) and restart the MongoDB service.

1. Open the `mongod.conf` file.
2. Add the following lines to enable authentication:

```yaml
security:
  authorization: enabled
```

3. Restart the MongoDB service.

## Creating Users in MongoDB

To create a user in MongoDB, use the `createUser` command. Here is an example of creating an admin user:

```javascript
use admin
db.createUser({
  user: "adminUser",
  pwd: "adminPassword",
  roles: [{ role: "userAdminAnyDatabase", db: "admin" }]
})
```

## Roles and Permissions

MongoDB provides several built-in roles, such as `read`, `readWrite`, `dbAdmin`, and `userAdmin`. You can also create custom roles to fit your specific needs.

### Built-in Roles

- `read`: Allows read access to the database.
- `readWrite`: Allows read and write access to the database.
- `dbAdmin`: Allows administrative access to the database.
- `userAdmin`: Allows management of users and roles.

### Custom Roles

To create a custom role, use the `createRole` command:

```javascript
use admin
db.createRole({
  role: "customRole",
  privileges: [
    { resource: { db: "exampleDB", collection: "" }, actions: ["find", "insert"] }
  ],
  roles: []
})
```

### Assigning Roles to Users

To assign a role to a user, use the `grantRolesToUser` command:

```javascript
use admin
db.grantRolesToUser("adminUser", [{ role: "customRole", db: "admin" }])
```

## Managing Users

### Viewing Existing Users

To view existing users, use the `show users` command:

```javascript
use admin
db.getUsers()
```

### Updating User Roles and Permissions

To update a user's roles and permissions, use the `updateUser` command:

```javascript
use admin
db.updateUser("adminUser", {
  roles: [{ role: "userAdminAnyDatabase", db: "admin" }, { role: "customRole", db: "admin" }]
})
```

### Deleting Users

To delete a user, use the `dropUser` command:

```javascript
use admin
db.dropUser("adminUser")
```

## Practical Examples

### Creating a Read-Only User

```javascript
use exampleDB
db.createUser({
  user: "readOnlyUser",
  pwd: "readOnlyPassword",
  roles: [{ role: "read", db: "exampleDB" }]
})
```

### Creating a User with Read/Write Permissions

```javascript
use exampleDB
db.createUser({
  user: "readWriteUser",
  pwd: "readWritePassword",
  roles: [{ role: "readWrite", db: "exampleDB" }]
})
```

### Creating a User with Admin Privileges

```javascript
use admin
db.createUser({
  user: "adminUser",
  pwd: "adminPassword",
  roles: [{ role: "userAdminAnyDatabase", db: "admin" }]
})
```

## Best Practices for User Management

1. **Least Privilege Principle**: Assign the minimum necessary permissions to users.
2. **Regular Audits**: Regularly review and audit user roles and permissions.
3. **Environment-Specific Users**: Use different users for development, staging, and production environments.

## Hands-On Exercises

### Exercise 1: Create a Read-Only User

Create a user with read-only access to a specific database.

### Exercise 2: Create a Custom Role

Create a custom role and assign it to a user.

### Exercise 3: Update a User's Role

Update a user's role and verify the changes.

## Q&A Session

Open floor for questions and discussions.