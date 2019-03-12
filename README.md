# Docker - Elasticsearch Logstash Kibana

## hosts

add line.

```
127.0.0.1 elasticsearch
```

## docker version

```
Client:
 Version:	17.12.0-ce
 API version:	1.35
 Go version:	go1.9.2
 Git commit:	c97c6d6
 Built:	Wed Dec 27 20:03:51 2017
 OS/Arch:	darwin/amd64

Server:
 Engine:
  Version:	17.12.0-ce
  API version:	1.35 (minimum version 1.12)
  Go version:	go1.9.2
  Git commit:	c97c6d6
  Built:	Wed Dec 27 20:12:29 2017
  OS/Arch:	linux/amd64
  Experimental:	true
```
## build

```
docker-compose build
```

## up

```
docker-compose up
```

## Create kibana index pattern

```
curl -XPOST -D- 'http://localhost:5601/api/saved_objects/index-pattern' \
    -H 'Content-Type: application/json' \
    -H 'kbn-version: 6.2.2' \
    -d '{"attributes":{"title":"logstash-*","timeFieldName":"@timestamp"}}'
```
## API

```
curl -H "content-type: application/json" -XPUT 'http://127.0.0.1:5000/twitter/twit/1' -d '{
    "user" : "kimchy",
    "post_date" : "2009-11-15T14:12:12",
    "message" : "trying out Elasticsearch"
}'
```
output(logstash-codec[rubydebug])
```
{
      "@version" => "1",
      "headers" => {
           "request_path" => "/twitter/tweet/1",
           "http_user_agent" => "curl/7.54.0",
           "http_host" => "127.0.0.1:5000",
           "http_accept" => "*/*",
           "content_length" => "110",
           "request_method" => "PUT",
           "request_uri" => "/twitter/tweet/1",
           "http_version" => "HTTP/1.1",
           "content_type" => "application/json"
      },
      "host" => "192.168.160.1",
      "user" => "kimchy",
      "post_date" => "2009-11-15T14:12:12",
      "@timestamp" => 2019-03-12T02:40:49.087Z,
      "message" => "trying out Elasticsearch"
}
```
elasticsearch
```
{
  "_index": "logstash-2019.03.12",
  "_type": "doc",
  "_id": "Yuvvb2kBGyXcqLaXr-TE",
  "_version": 1,
  "_score": null,
  "_source": {
    "@version": "1",
    "user": "kimchy",
    "post_date": "2009-11-15T14:12:12",
    "message": "trying out Elasticsearch",
    "@timestamp": "2019-03-12T03:26:12.822Z",
    "host": "192.168.176.1",
    "headers": {
      "http_version": "HTTP/1.1",
      "request_method": "PUT",
      "http_host": "127.0.0.1:5000",
      "http_user_agent": "curl/7.54.0",
      "content_length": "110",
      "http_accept": "*/*",
      "request_uri": "/twitter/twit/1",
      "content_type": "application/json",
      "request_path": "/twitter/twit/1"
    }
  },
  "fields": {
    "post_date": [
      "2009-11-15T14:12:12.000Z"
    ],
    "@timestamp": [
      "2019-03-12T03:26:12.822Z"
    ]
  },
  "sort": [
    1552361172822
  ]
}
```
