# How to Configure and Deploy a MongoDB Instance
In this lesson, we will cover how to configure and deploy a MongoDB instance by modifying the configuration file. We will look at the key parameters (such as the database path, port, and log file location) and explain how to update them. In addition, we'll discuss setting proper file and directory permissions when changing these paths.

## Assumptions:

- MongoDB is currently running on its default port (27017).
- You have administrative (sudo) access to the server.
- You are familiar with basic Linux commands.

## 1. Understanding the MongoDB Configuration File

MongoDB uses a YAML-formatted configuration file (commonly named mongod.conf) to determine its runtime settings. The file typically includes settings such as:

- storage.dbPath:
The directory where MongoDB stores its data files.

- systemLog.path:
The file path where the MongoDB logs are written.

- net.port:
The port on which MongoDB listens for connections.

Here is a sample snippet from a typical mongod.conf file:

``` yaml
 # mongod.conf
Where and how to store data.
storage: dbPath: /var/lib/mongodb journal: enabled: true

where to write logging data.
systemLog: destination: file path: /var/log/mongodb/mongod.log logAppend: true

network interfaces
net: port: 27017 bindIp: 127.0.0.1
```

## 2. Changing the Database and Log Directories
Imagine you want to change the data directory from /var/lib/mongodb to /data/mongodb and the log file from /var/log/mongodb/mongod.log to /data/logs/mongod.log.

- Step 1: Stop the MongoDB Service
Before making changes, stop the MongoDB service to avoid any conflicts or data corruption.

    ```bash
    sudo systemctl stop mongod 
    ```
    Or, if you use an init script:

    ``` bash
    sudo service mongod stop 
    ```

- Step 2: Update the Configuration File
Open the configuration file (mongod.conf) in your favorite text editor. For example:

    ``` bash
    sudo nano /etc/mongod.conf
    ```

    Modify the following sections:

    ```yaml 
    storage: dbPath: /data/mongodb
    systemLog: destination: file path: /data/logs/mongod.log logAppend: true

    net: port: 27017 bindIp: 127.0.0.1
    ```

    Save and close the file.

- Step 3: Create New Directories
If the new directories do not already exist, create them:

``` bash
sudo mkdir -p /data/mongodb sudo mkdir -p /data/logs
```

- Step 4: Set Proper Permissions
MongoDB typically runs under the mongodb user and group. You need to ensure that the new directories have the correct ownership and permissions so that MongoDB can read from and write to them.

    ``` bash
    sudo chown -R mongodb:mongodb /data/mongodb sudo chown -R mongodb:mongodb /data/logs
    ```
    Additionally, you might want to set appropriate permissions (for example, 755) on these directories:
    ``` bash
    sudo chmod 755 /data/mongodb sudo chmod 755 /data/logs
    ```
## 3. Restarting MongoDB with New Configuration
After updating the configuration file and setting the proper permissions, restart the MongoDB service:

    ``` bash
    sudo systemctl start mongod
    ```
    Or if using an init script:

    ``` bash sudo service mongod start 
    ```
    Verify that MongoDB is running and listening on port 27017:

    ``` bash 
    netstat -plnt | grep 27017 
    ```
    Or by checking the service status:

    ``` bash
    sudo systemctl status mongod
    ```
    You can also check the log file at /data/logs/mongod.log to confirm that MongoDB started without errors.

## 4. Additional Considerations
Backup Configuration Files:
Before making changes, it’s a good idea to back up your existing configuration file:

``` bash
sudo cp /etc/mongod.conf /etc/mongod.conf.backup
```

Environment Variables:
If you prefer not to modify the default config file, MongoDB can also accept parameters via command-line arguments. However, using the config file is recommended for consistency and ease of management.

SELinux/AppArmor:
If your system has SELinux or AppArmor enabled, ensure that the new directories are permitted by the relevant policies.

Port Changes:
Although our example uses the default port (27017), you can also change the port if needed by modifying the net.port value in mongod.conf and updating any firewall rules accordingly.

## 5. Summary
In this lesson, you learned how to:

Modify the MongoDB configuration file to change settings such as dbPath, systemLog.path, and net.port.
Stop the MongoDB service safely before making configuration changes.
Create new directories for the database and logs.
Set appropriate permissions so that the MongoDB user can access the new directories.
Restart MongoDB and verify that it is running with the new settings.
These steps are critical when you need to customize your MongoDB deployment for different storage configurations, performance optimizations, or compliance with system policies.

Happy configuring and deploying your MongoDB instance!