---
title: Help
sidebar: mydoc_sidebar
permalink: load-data.html
folder: mydoc
---

## Help Command

The help command is not a generic command on the BlobCity DB. The command is specific to the CLI interface itself and is useful to get usage instructions for various command supported by the CLI. The help command can be used to get generic help instructions on using the CLI or for viewing the format of a specific command.

```
blobcity>help
List all commands with parameter structure create-ds <ds-name>
create-collection <collection-name>
...
```
Simply typing help in the CLI interface, the format specification for all commands is displayed. This acts as a very quick reference for you to lookup all available commands and get a high level understanding of the parameter format for each command. The `. . .` put is simply a placeholder to indicate that the complete list is very long and avoided here for sake of brevity.

In certain cases, when you are sure of the command you want to use, but want more information on usage of the command or the parameter format, you can specify the command code for that command as a parameter to the help command.
```
blobcity>help create-ds
Format: create-ds <ds-name>
Description: Creates a new datastore with the provided name
Parameters:
<ds-name> name of the datastore to create
```

{% include links.html %}