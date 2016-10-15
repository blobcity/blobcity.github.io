---
title: Authentication
sidebar: mydoc_sidebar
permalink: cli-authentication.html
folder: mydoc
---

## Authentication

On opening a successful TCP connection to the CLI service, entering valid authentication credentials is mandatory. The system will immediately prompt you to enter a username and corresponding password that you want to use to connect to the CLI. An example login with the `root` user account is shown below.

```bash
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

The system will proceed further and display a welcome greeting followed by blobcity> to indicate that the login was successful and the system is now ready to take your CLI command. It is important to note that all users accounts created on a BlobCity cluster can login to CLI using valid credentials, but not all users may be able to perform all operations on the CLI.

All operations performed on the CLI are checked against the logged-in user to ensure that the user has the necessary permission to perform such an operation. The configured roles and permissions are fully applied over all CLI operations to ensure that no user gets access to data that is restricted to the user, or is able to perform any operation for which the user does not have permissions.

The root user by default has full permissions on the database. For the remainder of this chapter we will assume that all commands are fired by the root user with full permission. For the sake of brevity, we will not show the login process for the beginning of each operation and assume that the user is already successfully authenticated into the CLI and the CLI is ready for taking commands.

{% include links.html %}
