---
description: >-
  This guide will teach you how to install a mongoDB database on your Ubuntu
  22.04 Edge Server.
---

# How To Install mongoDB on Ubuntu 22.04

<figure><img src="../../../.gitbook/assets/mongoDB.png" alt=""><figcaption></figcaption></figure>

## Introduction <a href="#introduction" id="introduction"></a>

This guide will teach you how to install MongoDB on Ubuntu 22.04 Edge Server. MongoDB is a popular NoSQL database that is widely used in web development and big data applications. It is designed to handle unstructured data and offers high performance, scalability, and flexibility.

### Prerequisites

Before you start, you will need an Ubuntu 22.04 Edge Server with a non-**root** user with `sudo` privileges and a firewall enabled to block non-essential ports.

You can learn how to do this by following our base configuration tutorial for Ubuntu 22.04:

{% content-ref url="base-configuration-for-ubuntu-22.04.md" %}
[base-configuration-for-ubuntu-22.04.md](base-configuration-for-ubuntu-22.04.md)
{% endcontent-ref %}

Once you’re done setting this up, log in as your non-**root** user and proceed to step 1.

## Tutorial

### 1. Import the Public Key Used by the Package Management System

Import the MongoDB GPG key to ensure the authenticity of the package by running the following command:

```
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
```

The operation should respond with an `OK`.

### 2. Create a List File for MongoDB

Create a MongoDB source list file in the `/etc/apt/sources.list.d/` directory with this command:

```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

### 3. Reload Local Package Database

Issue the following command to reload the local package database:

```
sudo apt-get update
```

### 4. Install the MongoDB Packages

Install MongoDB by running:

```
sudo apt-get install -y mongodb-org
```

### 5. Start Your MongoDB Server

After the installation is complete, start the MongoDB service by running:

```
sudo systemctl start mongod
```

You can also enable MongoDB to start automatically at boot time by running:

```
sudo systemctl enable mongod
```

### Conclusion

That's it! You now have MongoDB installed on your Ubuntu 22.04 LTS Edge Server. Now that MongoDB is installed, you can start using it to store and retrieve data for your applications.
