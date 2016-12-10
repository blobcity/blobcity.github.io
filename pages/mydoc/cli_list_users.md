---
title: List Users
sidebar: mydoc_sidebar
permalink: cli-list-users.html
folder: mydoc
---

## List Users

```
blobcity>list-users
```

Lists all the users present in the database along with the system roles allotted to each user, and the groups the user belongs to. The user needs to have the `view-users` role assigned to be able to run the query. The operation is restricted on hosted cloud instances of the database.

This command will not allow for viewing of data level permissions that are allotted to users. For getting a detailed list of permissions associated with an user account the `list-permissions` query should be used.

The command is guaranteed to return the list of all user accounts present in the database, along with all respective roles and groups irrespective of any other permissions the logged in user has.
{% include links.html %}
