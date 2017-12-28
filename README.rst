CInP - Concise Interaction Protocol
===================================

CInP is a messaging protocol that allows software and systems  to communicate
via Hypertext Transfer Protocol (HTTP).  CInP was created to solve some
of the ambiguities with REST and to add a few non CRUD abilities.

Building these Docs
-------------------

...

HTTP Methods
------------

CInP Methods (or in REST Verbs)::

  * DESCRIBE - Describes the endpoint, see Describe.rst
  * GET - Get one or more Objest, see Get.rst
  * LIST - Get a List of Objects, see List.rst
  * CREATE - Create a new Object, see Create.rst
  * UPDATE - Update one or more Existing Object(s), see Update.rst
  * DELETE - Delete one or more Existing Objest(s), see Delete.rst
  * CALL - Invoke a Method on zero, one, or more Object(s), see CALL.rst
  * OPTIONS - Tells the browser what Methos are Allowed, and if configured, returns CORS headers

URI/Paths
---------

A CInP URI consists of a Scheme, Host, Port, Base Path, Namespace(s), Model, Id
and Action::

  scheme://host[:port]/root path/[namespace[/namespace...]/][model[:id:[id2:...]][(action)]]

NOTE: if the uri ends in `/` it is a path to a namespace, otherwise it is a path
to a model

scheme::

  curently supported schemes are http and https.  NOTE: HTTP/2 is planed for future versions.

host, port::

  hostname/ip address and port of the CInP service

root path::

  prefixed to all paths, ie: `/api/v1/`.  The root path is path of the root/base Namespace.
  It has been common pratice to embed the protocol version in the URI (ie: the `v1` of `/api/v1/`),
  this is allowed and recommended for CInP as well.  CInP adds an additional API version header
  so the client/server can verify the version independantly of the URI/Path.

namespace::

  grouping of simmaler and/or related models.  This is also handy for
  layer 7 load balancers to combine multiple backend servers into a simgle service.
  Each namespace caries it's own API version, enabling seperate namespaces to be
  intereated seperately from the others.  Namespces can be embeded inside of other
  namespaces.

model::

  the identifier of the model to work with.  The model inherits the
  API version of the namespace it resides in.

id::

  the id of the object of the model being worked with.  Multiple id's can be
  delimited by `:`.  The maximum number of ids that can be used is specified by the
  `multi-uri-max` paramater of the parent namespace.

action::

  the action to call on the model.  If a id(s) are specified the method is
  called on the object.  If no ids are specified, the method is `static` and called
  on the model.

HTTP Return codes
-----------------

200::

  OK/Deleted/Results returned

201::

  Created/Saved

400::

  Bad Request - some type of problem with the request.  The response body may be
  encoded and containe either a map of fields with errors messages for each field
  in error.  Or a error message.

401::

  Not Authorized (special exception for authentication)

404::

  Not Found

500::

  Exception, with the exception detail in the response body.  The response may be
  encoded, if so it may contain an error message, and optionally a stack trace.

HTTP Headers
------------

NOTE: Headers specific to each Method are in that Method's Documentation.

Request headers
---------------

CInP-Version::

  Specifies the CInP Protocol version.  It is curently `0.9`

Accept::

  Allows the client to specify what encodgins the client accepts.  At this end
  only `application/json` is implemented.  If omited the server will pick it's
  default, or may chose to return a 400.

Content-Type::

  The Encoding of the request application/json
