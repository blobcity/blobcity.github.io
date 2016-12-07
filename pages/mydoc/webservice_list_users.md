---
title: List Users
sidebar: mydoc_sidebar
permalink: webservice-list-users.html
folder: mydoc
---

## List Users

```
{
  "username" : "root",
  "password" : "root",
  "q" : "list-users"
}
```

Lists all the users present in the database along with the system roles allotted to each user, and the groups the user belongs to. The user needs to have the `view-users` role assigned to be able to run the query. The operation is restricted on hosted cloud instances of the database.

This command will not allow for viewing of data level permissions that are allotted to users. For getting a detailed list of permissions associated with an user account the `list-permissions` query should be used.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000,
  "p" : {
    "users" : [
      {
        "u": "username1",
        "r": ["view-users", "manage-users"],
        "g": ["group1"]
      },
      {
        "u": "username2",
        "r": ["view-cluster", "manage-cluster"],
        "g": ["group1", "group2"]
      } 
    ]
  } 
}

If the user is permitted to run the operation, provides the list of users along with the system level roles allotted to each user, the groups names of the group to which each user belongs. The payload contains an element with the key `users` that is a JSONArray of JSONObjects. Each JSONObject within the array maps to one individual user account.

The element `u` maps to the username of the user. The element `r` is a JSONArray of String that maps to all the system level roles allotted to the user. The element `g` is also a JSONArray of String that maps to the groups to which the user belongs.

The command is guaranteed to return the list of all user accounts present in the database, along with all respective roles and groups irrespective of the permission the connecting user has.
{% include links.html %}
