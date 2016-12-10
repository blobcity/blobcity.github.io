---
title: Load Code
sidebar: mydoc_sidebar
permalink: cli-load-code.html
folder: mydoc
---

## Load Code

```
blobcity>load-code {ds}
```

This command is used to load all types of stored procedures within a specified datastore. The name of the datastore is specified by the `{ds}` parameter. The compiled stored produce classes should be placed inside the `deploy-db-hot` folder of the corresponding datastore before the command is executed. The `db-code.mf` manifest file must also be located inside the `deploy-db-hot` folder, and should be of the correct format without any syntax errors for the operation to succeed.

The command will confirm to the user whether the code was successfully loaded or whether any error occurred in loading the code. The error if any occurred will be reported to the user to the best possible extent to allow for debugging of the problem.

If any code is already loaded for the datastore, this command will replace all previously loaded code with the new code. Loading code for one datastore, does not affect or reload code for any other datastore.
{% include links.html %}
