# EMAsphere
We forked this repository because the ActiveMQ image it generates is of good quality, and there is no official Apache ActiveMQ image available on Docker Hub.

All the scripts related to its push toward our ECRs are located in https://github.com/EMAsphere/emasphere/tree/develop/admin/containerization/ActiveMQ .

This base image is then used to built a customized version of the ActiveMQ broker, with the same _activemq.xml_ configuration file as the one used on the AWS service, AmazonMQ.

The only modification of this forked repository, compared to its "parent", is this section of the `README.md` file.

---

## Dockerfile to build a ActiveMQ container image.

Based on openjdk:8-jre-alpine, as lightweight as possible. 

Published on the Docker Hub: https://hub.docker.com/r/symptoma/activemq

## ActiveMQ version

Current version of ActiveMQ is **5.16.0**: https://activemq.apache.org/activemq-5160-release

## Build
```
docker build -t symptoma/activemq . 
```

## Run
```
docker run -it -p 61616:61616 8161:8161 symptoma/activemq:latest
```
Bind more ports if you need to.

## Publish

First, commit your change to Git. 

`git commit -m "Update ActiveMQ to 5.16.0"`

Then tag it. 

`git tag -a v5.16.0 -m 'Release 5.16.0'`

Then push it to Github.

`git push && git push origin --tags`

Each commit to master is automatically published to Docker Hub in the `latest` label. Tags are published in the corresponding versions.

Publishing manually works like this (after `docker login`):

```
docker tag f1aa123a520f symptoma/activemq:5.16.0
docker push symptoma/activemq
```
