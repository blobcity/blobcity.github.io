---
title: Accessing Database over CLI
sidebar: mydoc_sidebar
permalink: accessing-database-over-cli.html
folder: mydoc
---

## Accessing Database over CLI

The Command Line Interface (CLI) is the easiest and most developer friendly mechanism to perform operations on BlobCity DB. The CLI is permitted over the network and hence is actually a TCP stream. This means you do not have to be on the local terminal of the machine on which the database is running to use the CLI of the database.

The default connection to CLI is over port 10113. From a linux terminal the following command will get you connected to the CLI.

```
telnet localhost 10113
```

OR

```
telnet <ip> 10113
```

The `<ip>` allows for connecting to a remote database instance. You will be required to enter a valid username and password that you wish to use to connect to the database. On connection a greeting message will be displayed, and the console will be ready to accept further commands. Sample console shown below.

```
telnet localhost 10113
Trying ::1...
Connected to localhost.
Escape character is '^]'.
username>root
password>root
You are now inside the BlobCity DB console
Type 'help' for assistance and 'exit' to quit
blobcity>
```

All on-premise / dedicated instance of BlobCity ship with a default user named `root`. The password of the root user is also `root`. The root user has full administrative rights on the database. It is highly recommended that you change the password of the `root` user, or create new users and delete the `root` user as soon as your instance is setup.
{% include links.html %}
