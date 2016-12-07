---
title: Starting an Instance
sidebar: mydoc_sidebar
permalink: starting-an-instance.html
folder: mydoc
---

## Starting an Instance

The easiest way to start BlobCity on any operating system is using the Docker container. The BlobCity DB is hosted on Docker at https://hub.docker.com/r/blobcity/db/

You need to have docker installed and the docker daemon running on your computer for the following commands to work.

To start Docker as a daemon, or in background mode, use the following command.

```
docker run -d -p 10111:10111 -p 10113:10113 blobcity/db
```

This will pull the latest distribution of BlobCity DB from the public Docker registry and start the same on your computer. The command forwards two ports from your host machine to the docker container. The port 10111 is used by the adapter and other REST web services, while the port 10113 is used for CLI / Telnet connectivity for database management.

The database can be started in a non-daemon or foreground mode by replacing the `-d` flag with a `-i` flag. The following command will start the database in the current thread, and allow you to view the DB logs and diagnose any database related issues and errors.

```
docker run -i -p 10111:10111 -p 10113:10113 blobcity/db
```

The data stored in the database gets stored within the container itself. This can be a problem as changing the container or rerunning the container may cause a dataloss. Also the default file system allotted by Docker to your container is not recommended for production grade performance.

In order to map an external storage system to Docker, using the following command to map a host directory to a container directory. All data stored by BlobCity DB inside the container is stored at location /data. When an external folder is mounted on the same container location, all data gets saved onto the external folder, and the file system performance achieved by the container is that of the external folder.

A sample command mapping an host directory to the Docker container directory is provided below.

```
docker run -d -p 10111:10111 -p 10113:10113 -v /host-dir:/data blobcity/db
```

Here `host-dir` can be the absolute or relative path on your system where you would want the database’s data to be saved.

If you are using any large tables that will be stored on disk and no in-memory, then it is advisable to have the `host-dir` on an xfs formatted volume. If your primary storage is in-memory, any format volume is expected to work well.
￼
More information on Docker, micro services architecture and how to use Docker can be found at: http://docker.com

{% include links.html %}
