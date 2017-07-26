# hello-world-jresty

## how to run

### for users

``` bash
$ tar zxvf hello-world-jresty-1.1.0.tar.gz
$ cd hello-world-jresty-1.1.0

$ jresty start
jresty web app is listening on 8080 ...

$ curl http://localhost:8080/jresty/ping.json -i
some json response

$ jresty stop
```

if the port ``8080`` is already used by others, you can change the listening port in  ``hello-world-jresty-1.1.0/tomcat/conf/server.xml``


``` xml
<Connector port="8080 -> ${port}" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```


### for developers

- run in ``eclipse`` or ``IntelliJ IDEA``

	``org.example.jresty.runner.JettyEmbedRunner``

- run with maven

``` bash

# in rd env (development environment)
mvn -Djetty.port=8080 jetty:run -Dmaven.test.skip=true -Prd

# in op env (production environment)
mvn -Djetty.port=8080 jetty:run -Pop
```

## how to access

## multi representation

``` bash
curl http://localhost:8080/jresty/ping.json -i
curl http://localhost:8080/jresty/ping.jsonp -i
curl http://localhost:8080/jresty/ping.xml -i
curl http://localhost:8080/jresty/ping.html -i
curl http://localhost:8080/jresty/ping.jsp -i
```

``redirect`` support for ``.html`` or ``.jsp``

```
$ curl http://localhost:8080/jresty/ping.jsp?redirect=http://www.baidu.com -i
HTTP/1.1 302 Found
Content-Language: zh-cn
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true
Location: http://www.baidu.com?status=200&message=OK
Content-Length: 0
Server: Jetty(7.2.0.v20101020)

$ curl http://localhost:8080/jresty/ping.html?redirect=http://www.baidu.com -i

```

## two URLs for one method

``` bash
# GET ping.json is equal to GET ping-index.json
# POST ping.json is equal to GET ping-create.json
# DELETE ping.json is equal to GET ping-remove.json
# PUT ping.json is equal to GET ping-update.json
# GET ping/ABC.json is equal to GET ping-view.json?id=ABC

$ curl http://localhost:8080/jresty/ping.json -i
$ curl http://localhost:8080/jresty/ping-index.json -i
```

## some examples

``` bash
$ curl http://localhost:8080/jresty/ping.json -i
	HTTP/1.1 200 OK
	Content-Language: zh-cn
	Access-Control-Allow-Origin: *
	Content-Length: 97
	Content-Type: application/json;charset=UTF-8
	Cache-Control: max-age=0
	Server: Jetty(7.2.0.v20101020)

$ curl http://localhost:8080/jresty/ping.xml -i
	HTTP/1.1 200 OK
	Content-Language: zh-cn
	Access-Control-Allow-Origin: *
	Content-Length: 200
	Content-Type: application/xml;charset=UTF-8
	Cache-Control: max-age=0
	Server: Jetty(7.2.0.v20101020)

	<io.downgoon.jresty.rest.model.UnifiedResponse>
  		<status>200</status>
  		<message>OK</message>
  		<debug>20161218152559257318:系统正在运行</debug>
	</io.downgoon.jresty.rest.model.UnifiedResponse
```
