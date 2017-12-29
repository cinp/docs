UPDATE
======

The UPDATE request verb creates a new object for a given model.

The Path of the URI must be to a Model with an ID list, for example::

  /api/v1/Namespace/Model:id:

The updated object(s) will returned in response to this request.

The Request body should be the encoded data for the fields you want to update.

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

Sucessfull Update of one field for one object::

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

Update one filed in multiple objects::

  $ curl -sv -H "CInP-Version:0.9" -X UPDATE --data-raw "{ \"year\": 2040 }" -H "Content-Type: application/json"  http://127.0.0.1:8888/api/v1/Car/Model:4:5:6: | python -mjson.tool
  *   Trying 127.0.0.1...
  * TCP_NODELAY set
  * Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
  > UPDATE /api/v1/Car/Model:4:5:6: HTTP/1.1
  > Host: 127.0.0.1:8888
  > User-Agent: curl/7.55.1
  > Accept: */*
  > CInP-Version:0.9
  > Content-Type: application/json
  > Content-Length: 16
  >
  } [16 bytes data]
  * upload completely sent off: 16 out of 16 bytes
  < HTTP/1.1 200 OK
  < Server: gunicorn/19.7.1
  < Date: Fri, 29 Dec 2017 04:20:02 GMT
  < Connection: close
  < Verb: UPDATE
  < Cache-Control: no-cache
  < Multi-Object: True
  < Cinp-Version: 0.9
  < Access-Control-Allow-Origin: *
  < Access-Control-Expose-Headers: Method, Type, Cinp-Version, Count, Position, Total, Multi-Object, Object-Id
  < Content-Type: application/json;charset=utf-8
  < Content-Length: 509
  <
  { [509 bytes data]
  * Closing connection 0
  {
      "/api/v1/Car/Model:4:": {
          "created": "2017-12-29T04:05:18.408215+00:00",
          "make": "System",
          "model": "Small",
          "updated": "2017-12-29T04:20:02.803832+00:00",
          "year": 2040
      },
      "/api/v1/Car/Model:5:": {
          "created": "2017-12-29T04:05:18.409387+00:00",
          "make": "System",
          "model": "Bus",
          "updated": "2017-12-29T04:20:02.816171+00:00",
          "year": 2040
      },
      "/api/v1/Car/Model:6:": {
          "created": "2017-12-29T04:07:57.073544+00:00",
          "make": "Atom",
          "model": "Electron",
          "updated": "2017-12-29T04:20:02.832690+00:00",
          "year": 2040
      }
  }



Uncuessful Updates will have simmaler restuls as the Create Verb
