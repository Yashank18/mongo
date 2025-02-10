# Install MongoDB Enterprise Edition on Ubuntu

Supporting linux

- 24.04 LTS ("Noble")
- 22.04 LTS ("Jammy")
- 20.04 LTS ("Focal")


Check Linux version
```lsb_release```

## Steps
1. Import Public Key
    ```bash
    sudo apt-get install gnupg curl
    ```
    ```bash
    curl -fsSL https://pgp.mongodb.com/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
   ```
2. Create the list file
    - For 24
        ```bash
        echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.com/apt/ubuntu noble/mongodb-enterprise/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-enterprise-8.0.list
        ```
    - For 22
        ```bash
        echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.com/apt/ubuntu jammy/mongodb-enterprise/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-enterprise-8.0.list
        ```
3. Reload the package database
    ```bash
    sudo apt-get update
    ```
4. Install MongoDB Enterprise Server
    ```bash
    sudo apt-get install -y mongodb-enterprise
    ```

### Note:  
By default, a MongoDB instance stores:
- its data files in /var/lib/mongodb
- its log files in /var/log/mongodb
- MongoDB runs using the mongodb user account
- If you change the user that runs the MongoDB process, you must also modify the permission to the /var/lib/mongodb and /var/log/mongodb directories to give this user access to these directories.


5. Start MongoDB.
    ```bash
    sudo systemctl start mongod
    ```
6. Status
    ```bash
    sudo systemctl status mongod
    ```
7. Enable on reboot
    ```bash
    sudo systemctl enable mongod
    ```
8. Begin using MongoDB.
    ```bash
    mongosh
    ```


    [Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
ExecStart=/home/ubuntu/prometheus-3.1.0.linux-amd64/prometheus --config.file=/home/ubuntu/prometheus-3.1.0.linux-amd64/prometheus.yml
Restart=always

[Install]
WantedBy=default.target