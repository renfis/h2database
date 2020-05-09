# h2database
Docker image for [h2database](https://www.h2database.com/)

# Quickstart

These are just some simple examples how to create and use a H2 database. For comprehensive documentation
please read the docs on the [H2 homepage](https://h2database.com/html/main.html).

## Show all options

To display all available options, just execute:

    docker run --rm renfis/h2database

## Start temporary database

To just create a non-persistent database to play around, do the following:
```shell script
docker run --rm `# Delete the container after is is stopped` \
       -p 127.0.0.1:8092:8092 `# Bind port 8092 only to localhost` \
       renfis/h2database \
       -web `# Let server accept tcp connections (default port: 8092)` \
       -webAllowOthers `# Allow connections from outside the docker container` \
       -ifNotExists `# Allow creation of new databases`
```

Open http://localhost:8092 to connect to the database.

When the container is stopped, all data is deleted. 

## Create a new persistent database

Often you want to create a database which is not bound to the container lifecycle.

1. Create a folder on your host machine. The folder name is `data` in this example.
2. Start the container
   - with web interface enabled (`-web -webAllowOthers`)
   - with data folder mounted (`-v $(pwd)/data:/data`)
   - with base directory specified to be this folder (`-baseDir /data`)

```shell script
docker run --rm \
       -p 127.0.0.1:8092:8092 \
       -v $(pwd)/data:/data \
       renfis/h2database \
       -web \
       -webAllowOthers \
       -baseDir /data
```

Open http://localhost:8092 to connect to the database.

When the container is stopped, the data is persisted in the `data` folder and can be reused.

If you don't want to create the database using the web interface, you can also allow tcp connections. See next example. 

## Connect to an existing database

This example is similar to the above one, except that we 
- enable tcp connection
- do not allow creation of new databases 

```shell script
docker run --rm \
       -p 127.0.0.1:9092:9092 \
       -v $(pwd)/data:/data \
       renfis/h2database \
       -tcp \
       -tcpAllowOthers \
       -baseDir /data
```

More information how to start and connect to the server can be found in the [official documentation](https://h2database.com/html/tutorial.html#using_server).
