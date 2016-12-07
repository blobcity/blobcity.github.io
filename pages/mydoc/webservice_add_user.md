---
title: Add User
sidebar: mydoc_sidebar
permalink: webservice-add-user.html
folder: mydoc
---

## Add User

```json
{
  "username" : "root",
  "password" : "root",
  "q" : "add-user",
  "p" : {
    "username" : "username1",
    "password" : "password1"
  }
}
```

Creates the specified user account in the database, with the username is not already allotted to another user. The username needs to comply with the username specification standard to not include any special characters. Only alphanumeric values with ‘-‘ and ‘_’ characters is allowed.

The user created by this command has no permissions by default. The user will be able to login to the database, but will not be able to access any data or performance any database management operations unless the user is allotted the necessary permissions or added to a group that has the necessary permissions.

This command is restricted on hosted cloud instance of the product. Cloud users need to use the management portal to create new user accounts.

**Response Structure**

```
{
"ack" : "1",
  "time" : 1000
}
```

Provides a simple acknowledgement confirming creation of the new user account.
{% include links.html %}
