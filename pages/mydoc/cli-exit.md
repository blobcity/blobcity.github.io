---
title: Exit
sidebar: mydoc_sidebar
permalink: cli-exit.html
folder: mydoc
---

## Exit Command

The exit command is a generic command on the BlobCity DB. The command is specific to the CLI interface and is used to exit from the CLI session. On hitting the exit command, the CLI connection opened on the DB will be terminated.
```
blobcity>exit
Closing console. Bye! 
Connection closed by foreign host
```

No data is lost by the exit command. All operations over CLI have no dependency on the connection being open. Any operation performed before close of the connection will be persisted.

{% include links.html %}
