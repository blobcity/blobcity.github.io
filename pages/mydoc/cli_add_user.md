---
title: Add User
sidebar: mydoc_sidebar
permalink: cli-add-user.html
folder: mydoc
---

## Add User

```
blobcity>add-user {username} {password}
```

Creates the specified user account in the database, if the username is not already allotted to another user. The username is specified by the `{username}` parameter and the password that the user will use to login is specified by the `{password}` parameter. The username needs to comply with the username specification standard to not include any special characters. Only alphanumeric values with ‘-‘ and ‘_’ characters is allowed.

The user created by this command has no permissions by default. The user will be able to login to the database, but will not be able to access any data or perform any database management operations unless the user is allotted the necessary permissions or added to a group that has the necessary permissions.

This command is restricted on hosted cloud instances of the product. Cloud users need to use the management portal to create new user accounts.

The command will provide feedback indicating whether the user account was created, and if not created will response with the reason for non creation that can be used to debug the problem.
{% include links.html %}
