# MongoDB System Commands Lesson
In this lesson, we will explore a variety of system commands in MongoDB. These commands are essential for monitoring server status, gathering performance metrics, diagnosing issues, and managing system operations. Whether you're an experienced SQL/Oracle administrator or new to MongoDB, understanding these commands will help you maintain and troubleshoot your MongoDB environment.

### Below is a list of commonly used MongoDB system commands, along with a brief explanation and example for each.

## 1. Server and Database Status
### 1.1. db.serverStatus()
- Purpose:
Provides a comprehensive overview of the status of the MongoDB server, including metrics on memory, network, connections, operations, and more.

Example:

```javascript
 > db.serverStatus()
```

### 1.2. db.stats()
- Purpose:
Returns statistics about the current database, such as the number of collections, data size, storage size, and index information.

Example:
``` javascript
 > db.stats() 
```
### 1.3. db.getSiblingDB("admin").runCommand({ buildInfo: 1 })
- Purpose:
Retrieves detailed build information about the MongoDB server (version, modules, compiler, and flags).

Example:

``` javascript
 > db.getSiblingDB("admin").runCommand({ buildInfo: 1 }) 
```
## 2. Monitoring Current Operations
### 2.1. db.currentOp()
- Purpose:
Displays currently running operations on the MongoDB server. This is helpful for diagnosing performance issues or long-running queries.

Example:

``` javascript
 > db.currentOp() 
```
### 2.2. db.adminCommand({ connPoolStats: 1 })
- Purpose:
Returns statistics about the connection pool, including information on available, in-use, and created connections.

Example:

``` javascript
 > db.adminCommand({ connPoolStats: 1 }) 
```
## 3. Host and System Information
### 3.1. db.hostInfo()
- Purpose:
Provides information about the system (host) on which MongoDB is running, including OS details, CPU, memory, and disk usage.

Example:

``` javascript
 > db.hostInfo() 
```
### 3.2. db.getLog("startupWarnings")
- Purpose:
Retrieves startup warnings that were generated when MongoDB started. Useful for identifying potential configuration or compatibility issues.

Example:

``` javascript
 > db.getLog("startupWarnings") 
```
## 4. Logging and Diagnostics
### 4.1. db.adminCommand({ getLog: "global" })
- Purpose:
Retrieves the global log, which includes information on operations, warnings, and errors.

Example:

``` javascript
 > db.adminCommand({ getLog: "global" }) 
```
### 4.2. db.setLogLevel(verbosity)
- Purpose:
Sets the logging verbosity level for the current connection. Adjusting the verbosity can help diagnose issues by providing more detailed logs.

Example:

``` javascript
 > db.setLogLevel(2) 
```
## 5. Replica Set and Sharding Commands
### 5.1. db.isMaster() (or db.hello() in newer versions)
- Purpose:
Returns information about the role of the current node in a replica set. It indicates whether the node is primary, secondary, or an arbiter.

Example:

``` javascript
 > db.isMaster() 
```
### 5.2. rs.status()
- Purpose:
Provides the status of the replica set, including information on members, state, and replication lag.

Example:

``` javascript
 > rs.status() 
```
### 5.3. rs.conf()
- Purpose:
Displays the current configuration of the replica set.

Example:

``` javascript
 > rs.conf() 
```
### 5.4. db.adminCommand({ listDatabases: 1 })
- Purpose:
Lists all databases on the server. This command is often run from the admin database.

Example:

``` javascript
 > db.adminCommand({ listDatabases: 1 }) 
```
## 6. Shutdown and Maintenance
### 6.1. db.shutdownServer()
- Purpose:
Shuts down the MongoDB server. This command must be executed with appropriate privileges (typically from the admin database).

Example:

``` javascript
 > db.shutdownServer() 
```
### 6.2. db.killOp(opid)
- Purpose:
Terminates an in-progress operation by its operation ID (retrieved from db.currentOp()).

Example:

``` javascript
 > db.killOp(12345) 
```
## 7. Profiling and Performance
### 7.1. db.setProfilingLevel(level, [slowms])
- Purpose:
Sets the database profiling level to capture performance data. The level can be set to 0 (off), 1 (slow operations), or 2 (all operations). An optional slowms parameter defines the threshold in milliseconds.

Example:

``` javascript
 > db.setProfilingLevel(1, 100) 
```
### 7.2. db.system.profile.find().pretty()
- Purpose:
Queries the system profile collection to analyze the performance of database operations.

Example:

``` javascript

 > db.system.profile.find().pretty() 
```
## 8. Summary
Below is a consolidated list of system commands covered in this lesson:

```
Server and Database Status:
db.serverStatus()
db.stats()
db.getSiblingDB("admin").runCommand({ buildInfo: 1 })

Monitoring Current Operations:
db.currentOp()
db.adminCommand({ connPoolStats: 1 })

Host and System Information:
db.hostInfo()
db.getLog("startupWarnings")

Logging and Diagnostics:
db.adminCommand({ getLog: "global" })
db.setLogLevel(verbosity)

Replica Set and Sharding Commands:
db.isMaster() / db.hello()
rs.status()
rs.conf()
db.adminCommand({ listDatabases: 1 })

Shutdown and Maintenance:
db.shutdownServer()
db.killOp(opid)

Profiling and Performance:
db.setProfilingLevel(level, [slowms])
db.system.profile.find().pretty()
```
These system commands provide critical insights into the health, performance, and configuration of your MongoDB instance. As you work with MongoDB, these commands will help you diagnose issues, perform routine maintenance, and optimize performance.