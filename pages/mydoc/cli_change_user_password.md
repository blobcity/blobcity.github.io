---
title: Change User Password
sidebar: mydoc_sidebar
permalink: cli-change-user-password.html
folder: mydoc
---

## Load Code

```
blobcity>change-user-password {username} {password}
```

Sets the password of the specified user to the specified password. The username is specified by the `{username}` parameter and the new password to set is specified by the `{password}` parameter. A valid old password of the user is not required to set a new password for the user, but the connecting user needs to have the `manage-user` role to set the password for another user. If the user who’s password is to be set is same as the connecting user, then no role or permission is required for the operation to succeed.
{% include links.html %}
