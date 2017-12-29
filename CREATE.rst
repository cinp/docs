CREATE
======

The CREATE request verb creates a new object for a given model.

The Path of the URI must be to a Model::

  /api/v1/Namespace/Model

The created object will returned in response to this request.

The Request body should be the encoded data for the new object.

Request Headers
---------------

No Request Additional Headers

Response Headers
----------------

Object-Id::

  Will return the full Path to the newly created object.

Examples
--------

Sucessfull Create::

  $ curl -sv -H "CInP-Version:0.9" -X CREATE --data-raw "{ \"make\": \"Atom\", \"model\": \"Electron\", \"year\": 1897 }" -H "Content-Type: application/json"  http://127.0.0.1:8888/api/v1/Car/Model | python -mjson.tool*   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > CREATE /api/v1/Car/Model HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Content-Type: application/json
  > Content-Length: 53
  >
  } [53 bytes data]
  * upload completely sent off: 53 out of 53 bytes
  < HTTP/1.1 201 CREATED
  < Server: gunicorn/19.7.1
  < Date: Fri, 29 Dec 2017 03:54:55 GMT
  < Connection: close
  < Verb: CREATE
  < Cache-Control: no-cache
  < Object-Id: /api/v1/Car/Model:7:
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 145
  <
  { [145 bytes data]
  * Closing connection 0
  {
      "created": "2017-12-29T03:54:55.119949+00:00",
      "make": "Atom",
      "model": "Electron",
      "updated": "2017-12-29T03:54:55.119897+00:00",
      "year": 1897
  }

Unsucessfull Create, with field error detail::

  $ curl -sv -H "CInP-Version:0.9" -X CREATE --data-raw "{ \"make\": \"Atom\", \"model\": \"Electron\", \"year\": \"sdf\" }" -H "Content-Type: application/json"  http://127.0.0.1:8888/api/v1/Car/Model | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > CREATE /api/v1/Car/Model HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Content-Type: application/json
  > Content-Length: 54
  >
  } [54 bytes data]
  * upload completely sent off: 54 out of 54 bytes
  < HTTP/1.1 400 BAD REQUEST
  < Server: gunicorn/19.7.1
  < Date: Fri, 29 Dec 2017 03:56:29 GMT
  < Connection: close
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 57
  <
  { [57 bytes data]
  * Closing connection 0
  {
      "year": "Invalid Value \"Unable to convert to an int\""
  }

Unsucessfull Create, with goobal error::

  $ curl -sv -H "CInP-Version:0.9" -X CREATE --data-raw "{ \"make\": \"Atom\", \"model\": \"Electron\", \"year\": 1897 }" -H "Content-Type: application/json"  http://127.0.0.1:8888/api/v1/Car/Model | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > CREATE /api/v1/Car/Model HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Content-Type: application/json
  > Content-Length: 53
  >
  } [53 bytes data]
  * upload completely sent off: 53 out of 53 bytes
  < HTTP/1.1 400 BAD REQUEST
  < Server: gunicorn/19.7.1
  < Date: Fri, 29 Dec 2017 04:07:58 GMT
  < Connection: close
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 69
  <
  { [69 bytes data]
  * Closing connection 0
  {
      "__all__": [
          "Model with this Make, Model and Year already exists."
      ]
  }
