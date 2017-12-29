Field/Paramater Data types
==========================

* String - String
* Integer - Integer Number
* Float - Floating point number
* Boolean - true/false t/f 1/0 (case-insensitive )
* DateTime - ISO 8691 Format ie: YYYY-MM-DD HH:MM:SS
* Map - Hash/Assositive Array.  NOTE: the values are type enforced, you must check the key and value types
* Model - Reference to an object of another model, the full path is required ie: /api/v1/Namespace/Model:id:
* File - See File type below


File
----

The File type is passed as a link to the contense of the file.  The schemas
that are accepted depend on the API's implementation.  The Describe of the
field/paramater will indicate the allowed schemas for uploading.  For download,
the server will return a uri that can be used to retrieve that file, usuall
a HTTP request.

Upload schemas curently implemented by the python implementaion are:

* http(s): in this case the API will download from the http(s) location and store
that file internally
* inline: the file is base64 encoded and append after the schema ie: inline://<base 64 data>
* djfh: Django File Handler, the file is uploaded to a endpoint that is specific
to the server, that will return a djfh://<token> uri, which can then be used
as the file for the file field.  Internally the server copies the file from internal
temporary storage to perminante store.  NOTE: after use the file is removed from djfh,
also there is usally a max lifetime (default is 2 hours) before the file is cleaned
up, regardless of it is used.
