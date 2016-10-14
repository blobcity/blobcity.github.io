---
title: Telnet / CLI Interface
sidebar: mydoc_sidebar
permalink: telnet-cli-interface.html
folder: mydoc
---

## Over the network CLI based management

Whether On-Cloud or On-Premise, the BlobCity Database can be fully used her an over the network command line interface (CLI). The CLI uses a long running TCP pipe that can be opened with the database for sending in CLI type commands. It is important to note that while we call this capability a CLI capability, it is not a traditional CLI capability. It is CLI type syntax over a long running TCP connection. The CLI support is very exhaustive and extends to every action that can be taken on the database.

## Cloud Connection Endpoint
To connect to any cloud instance of BlobCity, the CLI connection can be opened using telnet in the manner shown below.

```
telnet {data-centre-id}.db.blobcity.com 10113
```

The telnet command is available by default in Mac and Linux distributions and can be fired from the terminal / Xterm window. On a Windows operating system the telnet can be achieved via PuTTY. The PuTTY client is free and offers telnet and ssh capability over windows operating systems.

The `{data-centre-id}` is the id of the data centre on which you are running your BlobCity instance. The id usually comprises of the major data centre provider code followed by the region code of the data centre. For connecting to AWS instance on US East (N. Virginia) the code would be `aws-us-east-1` and the endpoint would be `aws-us- east-1.db.blobcity.com`. The number `10113` is the port number on which the TCP based CLI service is running and needs to be specified. This is the default port for cloud and on-premise installations, and can be customised to a different suitable value for on- premise installations.

The complete list of upto date data centre codes can be found from the API details section on your cloud portal account. They are also mentioned in Appendix 3 for quick reference, but you should note that the list is ever changing, and the Appendix 3 may be outdated, by the time you are reading this.

## On-Premise Connection Endpoint
The BlobCity CLI for on-premise installations can be accessed by default at

`telnet localhost 10113`
OR

`telnet <ip> 10113`

If you are attempting to connect from a terminal window from the same machine as which the database is running `localhost` will work, or if you are connecting to an instance over the network and appropriate IP address needs to be specified in place of `<ip>`. The CLI is started over port `10113` by default and can be changed through the configuration file. You should ensure that the chosen port is not blocked by a firewall for the connection to succeed.

The rest of the chapter focuses on the request and response formats for the various supported operations over CLI.

{% include links.html %}
