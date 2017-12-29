CALL
====

The CALL request verb is to invoke actions/methods.  The Path of the URI must
be to a Model The action/method may be static, and use a path such as::

  /api/v1/Namespace/Model(action)

Or apply to one or models::

  /api/v1/Namespace/Model:id:(action)

The Request Body should be the encoded paramaters for the action.  Any return value
of the action will be returned in the response body.

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

Static (this is also an example login to get an Auth-Token)::

  $ curl -sv -H "CInP-Version:0.9" -X CALL --data-raw "{\"username\": \"bob\", \"password\": \"bob\"}" -H "Content-Type: application/json" http://127.0.0.1:8888/api/v1/User/Session\(login\) | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > CALL /api/v1/User/Session(login) HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Content-Type: application/json
  > Content-Length: 38
  >
  } [38 bytes data]
  * upload completely sent off: 38 out of 38 bytes
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 20:18:42 GMT
  < Connection: close
  < Verb: CALL
  < Cache-Control: no-cache
  < Multi-Object: False
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 32
  <
  { [32 bytes data]
  * Closing connection 0
  "fAzbVPrAlwZCtADeUIObKthODPkzjD"

On Object (This action requires that you are the owner to sell the car, so we use the Auth-Token from the previous example)::

  $ curl -sv -H "CInP-Version:0.9" -X CALL --data-raw "{ \"new_owner\": \"/api/v1/User/User:sally:\" }" -H "Content-Type: application/json" -H "Auth-Id: bob" -H "Auth-Token: fAzbVPrAlwZCtADeUIObKthODPkzjD" http://127.0.0.1:8888/api/v1/Car/Car:Commuter:\(sell\) | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > CALL /api/v1/Car/Car:Commuter:(sell) HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Content-Type: application/json
  > Auth-Id: bob
  > Auth-Token: fAzbVPrAlwZCtADeUIObKthODPkzjD
  > Content-Length: 43
  >
  } [43 bytes data]
  * upload completely sent off: 43 out of 43 bytes
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 20:26:49 GMT
  < Connection: close
  < Verb: CALL
  < Cache-Control: no-cache
  < Multi-Object: False
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 0
  <
  * Closing connection 0
  No JSON object could be decoded

NOTE: if you call this action again, you will et a 403 - Not Authorized, now that the car
is sold, you can't sell it again ;-).

The multi-opbject return values are the same format as GET
