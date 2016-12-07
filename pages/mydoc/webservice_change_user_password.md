---
title: Change User Password
sidebar: mydoc_sidebar
permalink: webservice-change-user-password.html
folder: mydoc
---

## Change User Password

```
{
  "username" : "root",
  "password" : "root",
  "q" : "change-user-password",
  "p" : {
    "username" : "username1",
    "new-password" : "password2"
  }
}
```

Sets the password of the specified user to the specified password. A valid old password of the user is not required to set a new password for the user, but the connecting user needs to have the `manage-user` role to set the password for another user. If the user who’s password is to be set is same as the connecting user, then no role or permission is required for the operation to succeed.

**Response Structure**

```
{
  "ack" : "1",
  "time" : 1000
}
```

Provides a simple acknowledgement confirming a change of password. If this response is an `ack` value of `1`, it ensures the password change and the old password will no longer work.
{% include links.html %}
