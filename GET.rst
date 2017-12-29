GET
===

The GET request verb is to reterive the detail of one or more objects for a model.

The Path of the URI must be to a Model with an ID list, for example::

  /api/v1/Namespace/Model:id:

Request Headers
---------------

Multi-Object::

  If set to True, the response is forces into mutli object response mode, otherwise
  the server will auto-detect if there are multiple objects in the response.

Response Headers
----------------

Multi-Object::

   Indicates if the response is in Mutli Object mode.

Examples
--------

Single Id::

  $ curl -sv -H "CInP-Version:0.9" http://127.0.0.1:8888/api/v1/Car/Model:2: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > GET /api/v1/Car/Model:2: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 18:21:10 GMT
  < Connection: close
  < Verb: GET
  < Cache-Control: no-cache
  < Multi-Object: False
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 146
  <
  { [146 bytes data]
  * Closing connection 0
  {
      "created": "2017-12-27T17:31:34.806368+00:00",
      "make": "Galaxy",
      "model": "Jupiter",
      "updated": "2017-12-27T17:31:34.806315+00:00",
      "year": 2012
  }

Multi Id::

  $ curl -sv -H "CInP-Version:0.9" http://127.0.0.1:8888/api/v1/Car/Model:2:3:4: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > GET /api/v1/Car/Model:2:3:4: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 18:20:39 GMT
  < Connection: close
  < Verb: GET
  < Cache-Control: no-cache
  < Multi-Object: True
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 514
  <
  { [514 bytes data]
  * Closing connection 0
  {
      "/api/v1/Car/Model:2:": {
          "created": "2017-12-27T17:31:34.806368+00:00",
          "make": "Galaxy",
          "model": "Jupiter",
          "updated": "2017-12-27T17:31:34.806315+00:00",
          "year": 2012
      },
      "/api/v1/Car/Model:3:": {
          "created": "2017-12-27T17:31:34.806830+00:00",
          "make": "Galaxy",
          "model": "Neptune",
          "updated": "2017-12-27T17:31:34.806801+00:00",
          "year": 2020
      },
      "/api/v1/Car/Model:4:": {
          "created": "2017-12-27T17:31:34.807199+00:00",
          "make": "System",
          "model": "Small",
          "updated": "2017-12-27T17:31:34.807168+00:00",
          "year": 2018
      }
  }

Single Id in Multi-mode::

  $ curl -sv -H "CInP-Version:0.9" -H "Multi-Object: True" http://127.0.0.1:8888/api/v1/Car/Model:2: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > GET /api/v1/Car/Model:2: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Multi-Object: True
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 18:22:10 GMT
  < Connection: close
  < Verb: GET
  < Cache-Control: no-cache
  < Multi-Object: True
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 172
  <
  { [172 bytes data]
  * Closing connection 0
  {
      "/api/v1/Car/Model:2:": {
          "created": "2017-12-27T17:31:34.806368+00:00",
          "make": "Galaxy",
          "model": "Jupiter",
          "updated": "2017-12-27T17:31:34.806315+00:00",
          "year": 2012
      }
  }

Requesting a non-exastant object::

  $ curl -sv -H "CInP-Version:0.9" http://127.0.0.1:8888/api/v1/Car/Model:300: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > GET /api/v1/Car/Model:300: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  >
  < HTTP/1.1 404 NOT FOUND
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 18:23:35 GMT
  < Connection: close
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 55
  <
  { [55 bytes data]
  * Closing connection 0
  {
      "model_path": "/api/v1/Car/Model",
      "object_id": "300"
  }

Asking for multiple and one does not exist::

  $ curl -sv -H "CInP-Version:0.9" http://127.0.0.1:8888/api/v1/Car/Model:1:300:2: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > GET /api/v1/Car/Model:1:300:2: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  >
  < HTTP/1.1 404 NOT FOUND
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 18:24:42 GMT
  < Connection: close
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 55
  <
  { [55 bytes data]
  * Closing connection 0
  {
      "model_path": "/api/v1/Car/Model",
      "object_id": "300"
  }

Single Id, in multi mode, that does not exist::

  $ curl -sv -H "CInP-Version:0.9" -H "Multi-Object: True" http://127.0.0.1:8888/api/v1/Car/Model:300: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > GET /api/v1/Car/Model:300: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Multi-Object: True
  >
  < HTTP/1.1 404 NOT FOUND
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 18:25:05 GMT
  < Connection: close
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 55
  <
  { [55 bytes data]
  * Closing connection 0
  {
      "model_path": "/api/v1/Car/Model",
      "object_id": "300"
  }

Asking for an object without authorization to do so::

  $ curl -sv -H "CInP-Version:0.9" http://127.0.0.1:8888/api/v1/Car/Car:Commuter: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > GET /api/v1/Car/Car:Commuter: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  >
  < HTTP/1.1 403 FORBIDDEN
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 18:29:14 GMT
  < Connection: close
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 29
  <
  { [29 bytes data]
  * Closing connection 0
  {
      "message": "Not Authorized"
  }

Adding Auth-id and Auth-Token for a session with authorization::

  $ curl -sv -H "CInP-Version:0.9" -H "Auth-Id: bob" -H "Auth-Token: IyithOrhjIGRCdscloNdveslOXzMLV" http://127.0.0.1:8888/api/v1/Car/Car:Commuter: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > GET /api/v1/Car/Car:Commuter: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Auth-Id: bob
  > Auth-Token: IyithOrhjIGRCdscloNdveslOXzMLV
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 18:30:10 GMT
  < Connection: close
  < Verb: GET
  < Cache-Control: no-cache
  < Multi-Object: False
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 197
  <
  { [197 bytes data]
  * Closing connection 0
  {
      "cost": 500.0,
      "created": "2017-12-27T17:31:34.818744+00:00",
      "model": "/api/v1/Car/Model:4:",
      "name": "Commuter",
      "owner": "/api/v1/User/User:bob:",
      "updated": "2017-12-27T17:31:34.818710+00:00"
  }
