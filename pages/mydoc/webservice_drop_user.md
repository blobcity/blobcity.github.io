---
title: Drop User
sidebar: mydoc_sidebar
permalink: webservice-drop-user.html
folder: mydoc
---

## Drop User

```json
{
  "username" : "root",
  "password" : "root",
  "q" : "drop-user",
  "p" : {
    "username" : "username1",
  }
}
```

Completely drops the user account. None of the existing permission of the user have to be dropped for this operation to succeed. The connecting user needs to have the `manage-users` permission of the operation to succeed.

If dropping this specified user results in the system having no user with a particular role, that restricts permanent maintenance of the system, as a user with that role is required or another user that can allot a user with that role is required, the `drop-user` operation will be restricted.

The connecting user can use this command to drop himself; but the system will not allow a user to be dropped if at the end of the operation the database remains with no user accounts.

This command is restricted to hosted cloud users of the database. They should user the management portal to manage their cloud user accounts.

**Response Structure**

```
{
"ack" : "1",
  "time" : 1000
}
```

Provides a simple acknowledgement indicating if the user was dropped. An `ack` value of `1` is a confirmation that by the end of this operation the specified user account is no longer present in the database. For any restrictions that apply, the system will return an `ack` value of `0` with an appropriate cause explaining the restriction.
{% include links.html %}
