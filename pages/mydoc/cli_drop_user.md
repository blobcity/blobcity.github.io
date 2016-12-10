---
title: Drop User
sidebar: mydoc_sidebar
permalink: cli-drop-user.html
folder: mydoc
---

## Drop User

```
blobcity>drop-user {username}
```

Completely drops the specified user account. The username of the user to drop is specified by the `{username}` parameter. None of the existing permissions of the user have to be dropped for this operation to succeed. The connecting user needs to have the `manage-users` permission for the operation to succeed.

If dropping this specified user results in the system having no user with a particular role, that restricts permanent maintenance of the system, as a user with that role is required or another user cannot allot a user with that role, the `drop-user` operation will be restricted.

The connecting user can use this command to drop himself; but the system will not allow a user to be dropped if at the end of the operation the database remains with no user accounts.

This command is restricted to hosted cloud users of the database. They should use the management portal to manage their cloud user accounts.

Provides feedback indicating whether the user was dropped and if not dropped, provides the error reasons for debugging the problem.
{% include links.html %}
