DESCRIBE
========

The Describe Verb will return detail of how a Namespace, Model, or Action is
defined.

The Path of the URI may be a Namespace::

  /api/v1/Namespace/

A Model::

  /api/v1/Namespace/Model

Or Action::

  /api/v1/Namespace/Model(Action)

Request Headers
---------------

No Request Additional Headers

Response Headers
----------------

No Response Additional Headers

Examples
--------

Namespace::

  $ curl -sv -H "CInP-Version:0.9" -X DESCRIBE http://127.0.0.1:8888/api/v1/Car | python -mjson.tool*   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > DESCRIBE /api/v1/Car HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Fri, 29 Dec 2017 04:29:32 GMT
  < Connection: close
  < Verb: DESCRIBE
  < Type: Namespace
  < Cache-Control: max-age=0
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 185
  <
  { [185 bytes data]
  * Closing connection 0
  {
      "api-version": "0.1",
      "doc": "Cars and their Models",
      "models": [
          "/api/v1/Car/Model",
          "/api/v1/Car/Car"
      ],
      "multi-uri-max": 100,
      "name": "Car",
      "namespaces": [],
      "path": "/api/v1/Car/"
  }

Model::

  $ curl -sv -H "CInP-Version:0.9" -X DESCRIBE http://127.0.0.1:8888/api/v1/Car/Model | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > DESCRIBE /api/v1/Car/Model HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Fri, 29 Dec 2017 04:30:01 GMT
  < Connection: close
  < Verb: DESCRIBE
  < Type: Model
  < Cache-Control: max-age=0
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 568
  <
  { [568 bytes data]
  * Closing connection 0
  {
      "actions": [],
      "constants": {},
      "doc": "All the Make/Model/Years for the cars",
      "fields": [
          {
              "length": 100,
              "mode": "RW",
              "name": "make",
              "required": true,
              "type": "String"
          },
          {
              "length": 100,
              "mode": "RW",
              "name": "model",
              "required": true,
              "type": "String"
          },
          {
              "mode": "RW",
              "name": "year",
              "required": true,
              "type": "Integer"
          },
          {
              "mode": "RO",
              "name": "updated",
              "required": false,
              "type": "DateTime"
          },
          {
              "mode": "RO",
              "name": "created",
              "required": false,
              "type": "DateTime"
          }
      ],
      "list-filters": {},
      "name": "Model",
      "not-allowed-metods": [],
      "path": "/api/v1/Car/Model"
  }

Action::

  $ curl -sv -H "CInP-Version:0.9" -X DESCRIBE http://127.0.0.1:8888/api/v1/Car/Car\(sell\) | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > DESCRIBE /api/v1/Car/Car(sell) HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  >
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Fri, 29 Dec 2017 04:30:34 GMT
  < Connection: close
  < Verb: DESCRIBE
  < Type: Action
  < Cache-Control: max-age=0
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 393
  <
  { [393 bytes data]
  * Closing connection 0
  {
      "doc": "Change the ownership of the car to new_owner.  It is valid to sell it to one's\nself.  Does not handle any money,  that should be done else where.  If new_owner\nis left out, the car becomes unclaimed.",
      "name": "sell",
      "paramaters": [
          {
              "name": "new_owner",
              "type": "Model",
              "uri": "/api/v1/User/User"
          }
      ],
      "path": "/api/v1/Car/Car(sell)",
      "return-type": {
          "type": null
      },
      "static": false
  }
