# Druid Docker Image

## Run a simple Druid cluster

Build the docker image locally:

```
docker build .
```

This will spit out a final image md5 like `d7cb7f998281`. Tag this to
name "druid" with:

```docker tag d7cb7f998281 druid```

Now run with this command:

```docker run --rm -i -p 9889:9889 -p 3000:8082 -p 3001:8081 -p 8090:8090 -p 3888:3888 -p 2181:2181 -p 2888:2888 -p 8100:8100 druid```


Send a test datum into it with: `curl -H "Content-Type: application/json" -XPOST http://192.168.99.100:9889/v1/post/foo -d '{"timestamp":"2016-06-06T21:56:47Z", "dim1":"a", "dim2":"b", "dim3":"c", "count":1, "x":1}'`

(You will need to update the timestamp to reflect the current date and
time)

-------------------------------------

[Install Docker](docker-install.md)

Download and launch the docker image

```sh
docker pull druidio/example-cluster
docker run --rm -i -p 3000:8082 -p 3001:8081 -p 3090:8090 druidio/example-cluster
```

Wait a minute or so for Druid to start up and download the sample.

On OS X

- List datasources

```
curl http://$(docker-machine ip default):3000/druid/v2/datasources
```

- access the coordinator console

```
open http://$(docker-machine ip default):3001/
```

On Linux

- List datasources

```
curl http://localhost:3000/druid/v2/datasources
```

- access the coordinator console at http://localhost:3001/

## Build Druid Docker Image

To build the docker image yourself

```sh
git clone https://github.com/druid-io/docker-druid.git
docker build -t example-cluster docker-druid
```
