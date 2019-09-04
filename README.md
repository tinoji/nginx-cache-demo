# nginx-cache-demo
ex. https://docs.nginx.com/nginx/admin-guide/content-cache/content-caching/#

## start
`docker-compose build && docker-compose up -d`

## demo
MISS
```
$ curl -i http://localhost:8080/static/sample.txt
HTTP/1.1 200 OK
Server: nginx/1.17.3
Date: Wed, 04 Sep 2019 14:41:47 GMT
Content-Type: text/plain
Content-Length: 16
Connection: keep-alive
Last-Modified: Wed, 04 Sep 2019 14:18:10 GMT
ETag: "5d6fc7a2-10"
X-Nginx-Cache: MISS
Accept-Ranges: bytes

this is sample.
```

HIT
```
$ curl -i http://localhost:8080/static/sample.txt
HTTP/1.1 200 OK
Server: nginx/1.17.3
Date: Wed, 04 Sep 2019 14:41:48 GMT
Content-Type: text/plain
Content-Length: 16
Connection: keep-alive
Last-Modified: Wed, 04 Sep 2019 14:18:10 GMT
ETag: "5d6fc7a2-10"
X-Nginx-Cache: HIT
Accept-Ranges: bytes

this is sample.
```

Check cache file.
```
$ docker exec -it nginx_cache /bin/sh
/ # ls /var/cache/nginx
7322fc7fc58b4c35b5c413965becc826
```

PURGE
```
$ curl -i http://localhost:8080/purge/static/sample.txt
HTTP/1.1 200 OK
Server: nginx/1.17.3
Date: Wed, 04 Sep 2019 14:41:52 GMT
Content-Type: text/html
Content-Length: 277
Connection: keep-alive

<html>
<head><title>Successful purge</title></head>
<body bgcolor="white">
<center><h1>Successful purge</h1>
<br>Key : localhost/static/sample.txt
<br>Path: /var/cache/nginx/7322fc7fc58b4c35b5c413965becc826
</center>
<hr><center>nginx/1.17.3</center>
</body>
</html>
```

Check cache file again.
```
/ # ls /var/cache/nginx
/ #
```

