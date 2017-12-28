LIST
====

The LIST request method is to reterive a list of object IDs.

The Path of the URI must be to a Model, for example::

  /api/v1/Namespace/Model

If a filter is specified, the filter paramaters are encoded and sent in the
request body.

Request Headers
---------------

Filter::

  If specified, indicates the name of the filter to use.  The list of avaible
  filter names and parmaters can be obtained from DESCRIBING the Model.

Count::

  How many object to reterieve.  If not specified, the server will use it's default
  value.  NOTE: The server may have an internal limit to the number of ids to
  respond with, or may not have the time/resources or some other restriction that
  prevents it from returning the full count.  The Count, Position, Total response
  headers will indicate what was returned.  NOTE2: The results will all be contigious.

Position::

  Which numeric offset to start the list at.

Response Headers
----------------

Count::

  Number of IDs returned.

Position::

  Position the list starts at

Total::

  Total number of objects in the set


Examples
--------

List all::

  $ curl -sv -H "CInP-Version:0.9" -X LIST http://127.0.0.1:8888/api/v1/Car/Car | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > LIST /api/v1/Car/Car HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 19:10:00 GMT
  < Connection: close
  < Method: LIST
  < Cache-Control: no-cache
  < Count: 8
  < Position: 0
  < Total: 8
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 240
  <
  { [240 bytes data]
  * Closing connection 0
  [
      "/api/v1/Car/Car:Commuter:",
      "/api/v1/Car/Car:Meteor:",
      "/api/v1/Car/Car:Meteor2:",
      "/api/v1/Car/Car:Planet_Hopper:",
      "/api/v1/Car/Car:Red_Beast:",
      "/api/v1/Car/Car:Smasher:",
      "/api/v1/Car/Car:Star_Chaser:",
      "/api/v1/Car/Car:Star_Hopper:"
  ]

List 5 starting at position 2::

  $ curl -sv -H "CInP-Version:0.9" -X LIST -H "Count: 5" -H "Position: 2" http://127.0.0.1:8888/api/v1/Car/Car | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > LIST /api/v1/Car/Car HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Count: 5
  > Position: 2
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 19:11:09 GMT
  < Connection: close
  < Method: LIST
  < Cache-Control: no-cache
  < Count: 5
  < Position: 2
  < Total: 8
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 152
  <
  { [152 bytes data]
  * Closing connection 0
  [
      "/api/v1/Car/Car:Meteor2:",
      "/api/v1/Car/Car:Planet_Hopper:",
      "/api/v1/Car/Car:Red_Beast:",
      "/api/v1/Car/Car:Smasher:",
      "/api/v1/Car/Car:Star_Chaser:"
  ]

Filter::

  $ + curl -sv -H "CInP-Version:0.9" -X LIST -H "Filter: owner" --data-raw "{\"owner\": \"/api/v1/User/User:bob:\"}" -H "Content-Type: application/json" http://127.0.0.1:8888/api/v1/Car/Car | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > LIST /api/v1/Car/Car HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Filter: owner
  > Content-Type: application/json
  > Content-Length: 35
  >
  } [35 bytes data]
  * upload completely sent off: 35 out of 35 bytes
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Thu, 28 Dec 2017 19:21:44 GMT
  < Connection: close
  < Method: LIST
  < Cache-Control: no-cache
  < Count: 2
  < Position: 0
  < Total: 2
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 59
  <
  { [59 bytes data]
  * Closing connection 0
  [
      "/api/v1/Car/Car:Red_Beast:",
      "/api/v1/Car/Car:Commuter:"
  ]
