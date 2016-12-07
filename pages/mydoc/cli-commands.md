---
title: Commands 
sidebar: mydoc_sidebar
permalink: cli-commands.html
folder: mydoc
---

## Command Format

All CLI requests start with a command code. The command code instructs the database of the operation the user wishes to perform as part of that request. Each support operation has a unique command code. An example command is shown below.

```
blobcity>create-ds datastore1
```

In the above command `create-ds` is the command code and `datastore1` is the command parameter. All commands need to always start with a valid command code. `datastore1` is a parameter supplied to the create-ds command, and the parameter formats varying from command to command. This particular command creates a new datastore with the specified name of datastore1.

The `blobcity>` shown at the beginning of the command is actually not typed by the user. This is displayed by default by the CLI interface, to indicate to the user that the user is
successfully logged into the CLI and the CLI is ready to accept a new command.

{% include links.html %}
