## Elasticsearch Dockerfile


This repository contains **Dockerfile** of [Elasticsearch](http://www.elasticsearch.org/) for [Docker](https://www.docker.com/)'s [automated build](https://hub.docker.com/r/trantect/docker-elasticsearch/) published to the public [Docker Hub Registry](https://registry.hub.docker.com/).


### Base Docker Image

* [jeanblanchard/busybox-java:7](https://hub.docker.com/r/jeanblanchard/busybox-java/)


### Installation

1. Install [Docker](https://www.docker.com/).

2. Download [automated build](https://hub.docker.com/r/trantect/docker-elasticsearch/) from public [Docker Hub Registry](https://registry.hub.docker.com/): `docker pull trantect/docker-elasticsearch`

   (alternatively, you can build an image from Dockerfile: `docker build -t="yours/docker-elasticsearch" github.com/Trantect/docker-elasticsearch`)


### Usage

    docker run -d -p 9200:9200 -p 9300:9300 yours/docker-elasticsearch

#### Attach persistent/shared directories

  1. Create a mountable data directory `<data-dir>` on the host.

  2. Create Elasticsearch config file at `<data-dir>/elasticsearch.yml`.

    ```yml
    path:
      logs: /data/log
      data: /data/data
    ```

  3. Start a container by mounting data directory and specifying the custom configuration file:

    ```sh
    docker run -d -p 9200:9200 -p 9300:9300 -v <data-dir>:/data yours/docker-elasticsearch /elasticsearch/bin/elasticsearch -Des.config=/data/elasticsearch.yml
    ```

After few seconds, open `http://<host>:9200` to see the result.
