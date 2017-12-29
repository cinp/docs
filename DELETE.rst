DELETE
======

The DELETE request verb is to delete one or more objects for a model.

The Path of the URI must be to a Model with an ID list, for example::

  /api/v1/Namespace/Model:id:

Request Headers
---------------

No Request Additional Headers

Response Headers
----------------

No Response Additional Headers

Examples
--------

Delete one object::

  $ curl -sv -H "CInP-Version:0.9" -X DELETE -H "Content-Type: application/json" -H "Auth-Id: bob" -H "Auth-Token: fAzbVPrAlwZCtADeUIObKthODPkzjD" http://127.0.0.1:8888/api/v1/Car/Car:Red_Beast: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > DELETE /api/v1/Car/Car:Red_Beast: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Content-Type: application/json
  > Auth-Id: bob
  > Auth-Token: fAzbVPrAlwZCtADeUIObKthODPkzjD
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Fri, 29 Dec 2017 03:18:21 GMT
  < Connection: close
  < Verb: DELETE
  < Cache-Control: no-cache
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 0
  <
  * Closing connection 0
  No JSON object could be decoded

Trying to Delete when not authorized::

  $ curl -sv -H "CInP-Version:0.9" -X DELETE -H "Content-Type: application/json" -H "Auth-Id: bob" -H "Auth-Token: fAzbVPrAlwZCtADeUIObKthODPkzjD" http://127.0.0.1:8888/api/v1/Car/Car:Commuter: | python -mjson.tool*   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > DELETE /api/v1/Car/Car:Commuter: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Content-Type: application/json
  > Auth-Id: bob
  > Auth-Token: fAzbVPrAlwZCtADeUIObKthODPkzjD
  >
  < HTTP/1.1 403 FORBIDDEN
  < Server: gunicorn/19.7.1
  < Date: Fri, 29 Dec 2017 03:17:26 GMT
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
