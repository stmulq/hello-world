# Autoruns/Plugins Endpoints (2022/06)

The Autoruns/Plugins endpoints allow users to manage autorun plugins on a network. 

**Base URL for this endpoint:**  [***https://api.bsn.cloud/2022/06/REST/Autoruns/Plugins***](https://api.bsn.cloud/2022/06/REST/Autoruns/Plugins)

*\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_*

## GET /

Returns a list of autorun plugins on a network

**Required Scope Token**

bsn.api.main.autoruns.plugins.retrieve

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Query String Parameters**

`filter` string optional

An [expression](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1169785260/Filtering+and+Sorting+Expressions+in+the+Main+API) for filtering search results. The default value is null.

`sort` string optional

An expression for sorting the search results. The sort expression specifies the entry used for sorting and the ascending/descending (ASC/DESC) sorting order (see [this page](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1169785260/Filtering+and+Sorting+Expressions+in+the+Main+API) for more information). The default value is null.

`marker` string optional

A value specifying which page to retrieve. This value is useful if the `isTruncated` entry in the response body of the previous GET call indicates that the number of autorun plugin instances exceeds the `pageSize`.

This parameter is only required if you need more elements in the paged list than the `pageSize` (100).

`pageSize` int optional

The maximum number of autorun plugin instances that can be contained in the response body. This defaults to the maximum allowed page size (100).

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Request Example**

The example request parameters and headers are set as follows:

*   `marker` value is set to the `[PagedList].[NextMarker]` property value from the previous BSN.cloud API response.
    
*   `pageSize` is set to `1`
    
*   `filter` is set to `[FileInfo].[Type] IS 'Stored' AND [FileInfo].[Size] IS GREATER THAN 0 AND [FileInfo].[Name] IS '*.brs'`
    
*   `sort` is set to `[FileInfo].[CreationDate] ASC`
    

```
GET /2022/06/REST/Autoruns/Plugins/?marker=MjAyMy0wOC0zMVQyMDo1Nzo0Mi41MDdaLDE1Mjc3&pageSize=1&filter=%5BFileInfo%5D.%5BType%5D%20IS%20%27Stored%27%20AND%20%5BFileInfo%5D.%5BSize%5D%20IS%20GREATER%20THAN%200%20AND%20%5BFileInfo%5D.%5BName%5D%20IS%20%27*.brs%27&sort=%5BFileInfo%5D.%5BCreationDate%5D%20ASC HTTP/1.1
Host: api.bsn.cloud
Connection: Keep-Alive
Authorization: Bearer {{UserAccessToken}}
Accept: application/json, application/vnd.bsn.error+json
Accept-Encoding: gzip,deflate
```

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Success Response Body**

200: Returns a [paged list](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1364394535/Paged+List+Entity+2022+06) of [Autorun Plugin Entity](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1364361253/Autorun+Plugin+Entity+2022+06) instances on a network. This will return not more than 100 entities along with the information necessary to return any other remaining pages.

**Example**

```
{
   "items": [   {
      "id": 15342,
      "name": "liveTextPlugin",
      "fileInfo":       {
         "id": 15342,
         "path": "https://bsncloud.s3.amazonaws.com/bsts/9b6a47d278ad065a03ba680c345f0ea7",
         "type": "Stored",
         "name": "livetextboth.brs",
         "size": 12,
         "hash": "430CE34D020724ED75A196DFC2AD67C77772D169",
         "creationDate": "2023-09-08T15:44:01.717Z",
         "lastModifiedDate": "2023-09-08T15:44:01.717Z"
      },
      "presentations": [   {
         "id": 65425,
         "name": "GreatPresentation",
         "type": "Presentation",
         "link": null
   }],
   "totalItemCount": 4,
   "matchingItemCount": 4,
   "pageSize": 1,
   "nextMarker": "MjAyMy0wOS0wOFQxNTo0NDowMS43MTdaLDE1MzQy",
   "isTruncated": false,
   "sortExpression": "[FileInfo].[CreationDate] ASC",
   "filterExpression": "[FileInfo].[Type] IS 'Stored' AND [FileInfo].[Size] IS GREATER THAN 0 AND [FileInfo].[Name] IS '*.brs'"
}
```

**Failure Response**

300: The requested representation could not be returned because it is ambiguous (there are multiple requested representations)

400: The request is malformed and therefore invalid

401: The access token is invalid or not specified

403: The supplied access token, though valid, doesn't provide access to this method 

406: The server cannot return the data representation that you requested (as specified in the "Accept" header)

5XX: Any 500 code is an internal server error

## POST /

Create a new autorun plugin on a network

**Required Scope Token**

bsn.api.main.autoruns.plugins.create

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Request Body**

The [Autorun Plugin Entity](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1364361253/Autorun+Plugin+Entity+2022+06)

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Request Example**

The example request parameters and headers are set as follows:

```
POST /2022/06/REST/Autoruns/Plugins/ HTTP/1.1
Host: api.bsn.cloud
Connection: Keep-Alive
Authorization: Bearer {{UserAccessToken}}
Accept: application/json, application/vnd.bsn.error+json
Accept-Encoding: gzip,deflate
Content-Type: application/json
Content-Length: 271
```

This is the example request body:

```
{
	"id":0,
	"name":"liveTextPlugin",
	"fileInfo": {
		"id":0,
		"name":"livetextboth.brs",
		"type":"New",
		"body":"aGVsbG8gd29ybGQh",
		"transferEncoding":"base64",
		"size":0,
		"hash":"",
		"creationDate": "0001-01-01T00:00:00",
		"lastModifiedDate": "0001-01-01T00:00:00"
	},
	"presentations":null
} 
```

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Success Response Body**

201: Returns the [Autorun Plugin Entity](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1364361253/Autorun+Plugin+Entity+2022+06) created and referenced by the Uri (given by the Location header field) in the response. 

**Example**

```
{
   "id": 15342,
   "name": "liveTextPlugin",
   "fileInfo":    {
      "id": 15342,
      "path": "https://bsncloud.s3.amazonaws.com/bsts/9b7f49d765ad795k06ba600c345f0ea7",
      "type": "Stored",
      "name": "livetextboth.brs",
      "size": 12,
      "hash": "430CE34D020724ED75A196DFC2AD67C77772D169",
      "creationDate": "2023-09-08T15:44:01.7152901Z",
      "lastModifiedDate": "2023-09-08T15:44:01.7152901Z"
   },
   "presentations": null
}
```

**Failure Response**

300: The requested representation could not be returned because it is ambiguous (there are multiple requested representations)

400: The request or request body is malformed and therefore invalid, or it is rejected in accordance with the business rules (for example, the name must be unique)

401: The access token is invalid or not specified

403: The supplied access token, though valid, doesn't provide access to this method 

406: The server cannot return the data representation that you requested (as specified in the "Accept" header)

415: The server cannot accept the data representation that you sent (as specified in the "Content-Type" header)

5XX: Any 500 code is an internal server error

## DELETE /

Removes autorun plugins matching the specified filter expression from a network. This allows multiple autorun plugins to be deleted at once.

**Required Scope Token**

bsn.api.main.autoruns.plugins.delete

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Query String Parameters**

`filter` string required

An [expression](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1169785260/Filtering+and+Sorting+Expressions+in+the+Main+API) for filtering search results.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Request Example**

The example request parameters and headers are set as follows:

*   `filter` is set to `[FileInfo].[Name] IS 'livetextboth.brs'`
    

```
DELETE /2022/06/REST/Autoruns/Plugins/?filter=%5BFileInfo%5D.%5BName%5D%20IS%20%27livetextboth.brs%27 HTTP/1.1
Host: api.bsn.cloud
Connection: Keep-Alive
Authorization: Bearer {{UserAccessToken}}
Accept: application/json, application/vnd.bsn.error+json
Accept-Encoding: gzip,deflate
```

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Success Response Body**

200: Returns the number of affected autorun plugins as an integer value.

**Failure Response**

300: The requested representation could not be returned because it is ambiguous (there are multiple requested representations)

400: The request or request body is malformed and therefore invalid, or it is rejected in accordance with the business rules

401: The access token is invalid or not specified

403: The supplied access token, though valid, doesn't provide access to this method 

406: The server cannot return the data representation that you requested (as specified in the "Accept" header)

5XX: Any 500 code is an internal server error

## GET /Count/ 

Returns the number of autorun plugins matching the specified filter expression in the network

**Required Scope Token**

bsn.api.main.autoruns.plugins.retrieve

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Query String Parameters**

`filter` string optional

An [expression](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1169785260/Filtering+and+Sorting+Expressions+in+the+Main+API) for filtering search results. The default value is null.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Request Example**

The example request parameters and headers are set as follows:

*   `filter` is set to `[FileInfo].[Type] IS 'Stored' AND [FileInfo].[Size] IS GREATER THAN 0 AND [FileInfo].[Name] IS '*.brs'`
    

```
GET /2022/06/REST/Autoruns/Plugins/Count/?filter=%5BFileInfo%5D.%5BType%5D%20IS%20%27Stored%27%20AND%20%5BFileInfo%5D.%5BSize%5D%20IS%20GREATER%20THAN%200%20AND%20%5BFileInfo%5D.%5BName%5D%20IS%20%27*.brs%27 HTTP/1.1
Host: api.bsn.cloud
Connection: Keep-Alive
Authorization: Bearer {{UserAccessToken}}
Accept: application/json, application/vnd.bsn.error+json
Accept-Encoding: gzip,deflate
```

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Success Response Body**

200: The autorun plugin count is returned as an integer value.

**Failure Response**

300: The requested representation could not be returned because it is ambiguous (there are multiple requested representations)

400: The request is malformed and therefore invalid

401: The access token is invalid or not specified

403: The supplied access token, though valid, doesn't provide access to this method

406: The server cannot return the data representation that you requested (as specified in the "Accept" header)

5XX: Any 500 code is an internal server error

## GET /{id:int}/ 

Returns the specified autorun plugin on a network

**Required Scope Token**

bsn.api.main.autoruns.plugins.retrieve

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Segment**

`id` int

A unique identifier for an autorun plugin instance

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Request Example**

The example request parameters and headers are set as follows:

*   `id` is set to `12345`
    

```
GET /2022/06/REST/Autoruns/Plugins/12345/ HTTP/1.1
Host: api.bsn.cloud
Connection: Keep-Alive
Authorization: Bearer {{UserAccessToken}}
Accept: application/json, application/vnd.bsn.error+json
Accept-Encoding: gzip,deflate
```

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Success Response Body**

200: Returns the [Autorun Plugin Entity](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1364361253/Autorun+Plugin+Entity+2022+06)

**Example**

```
{
  "id": 12345,
  "name": "liveTextPlugin",
  "fileInfo": {
    "id": 15342,
    "path": "https://bsncloud.s3.amazonaws.com/bsts/9b7f47d765ad105k06ba680c345f0ea7",
    "type": "Stored",
    "name": "livetextboth.brs",
    "size": 12,
    "hash": "430CE34D020724ED75A196DFC2AD67C77772D169",
    "creationDate": "2023-09-08T15:44:01.717Z",
    "lastModifiedDate": "2023-09-08T15:44:01.717Z"
  },
  "presentations": [
    {
      "id": 65425,
      "name": "GreatPresentation",
      "type": "Presentation",
      "link": null
    }
  ]
}
```

**Failure Response**

300: The requested representation could not be returned because it is ambiguous (there are multiple requested representations)

400: The request is malformed and therefore invalid

401: The access token is invalid or not specified

403: The supplied access token, though valid, doesn't provide access to this method

404: An autorun plugin with the specified id does not exist

406: The server cannot return the data representation that you requested (as specified in the "Accept" header)

5XX: Any 500 code is an internal server error

## PUT  /{id:int}/  

Update a specified autorun plugin on a network

**Required Scope Token**

bsn.api.main.autoruns.plugins.update

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Segment**

`id` int 

A unique identifier for an autorun plugin instance

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Request Body**

The [Autorun Plugin Entity](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1364361253/Autorun+Plugin+Entity+2022+06)

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Request Example**

The example request parameters and headers are set as follows:

*   `id` is `12345`
    

```
PUT /2022/06/REST/Autoruns/Plugins/12345/ HTTP/1.1
Host: api.bsn.cloud
Connection: Keep-Alive
Authorization: Bearer {{UserAccessToken}}
Accept: application/json, application/vnd.bsn.error+json
Accept-Encoding: gzip,deflate
Content-Type: application/json
Content-Length: 421
```

This is the example request body:

```
{
   "id": 0,
   "name": "liveTextPlugin",
   "fileInfo":    {
      "id": 1,
      "path": "https://bsncloud.s3.amazonaws.com/bsts/3d1a47da65ed068k76ba641c345f3dd5",
      "type": "Stored",
      "name": "plugin.brs",
      "size": 4,
      "hash": "5BF1FD927DFB8679496A2E6CF00CBE50C1C87145",
      "creationDate": "0001-01-01T00:00:00",
      "lastModifiedDate": "0001-01-01T00:00:00"
   },
   "presentations": []
}
```

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Success Response**

204: The specified autorun plugin has been updated on the network 

**Failure Response**

300: The requested representation could not be returned because it is ambiguous (there are multiple requested representations)

400: The request or request body is malformed and therefore invalid, or it is rejected in accordance with the business rules

401: The access token is invalid or not specified

403: The supplied access token, though valid, doesn't provide access to this method

404: The server cannot find the requested resource

406: The server cannot return the data representation that you requested (as specified in the "Accept" header)

412: Precondition failed (the resource/autorun plugin changed since the time specified in the “If-Unmodified-Since” header value)

415: The server cannot accept the data representation that you sent (as specified in the "Content-Type" header)

5XX: Any 500 code is an internal server error

## DELETE /{id:int}/ 

Remove a specified autorun plugin from a network

**Required Scope Token**

bsn.api.main.autoruns.plugins.delete

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Segment**

`id` int 

A unique identifier for an autorun plugin instance

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Request Example**

The example request parameters and headers are set as follows:

*   `id` is set to `12345`
    

```
DELETE /2022/06/REST/Autoruns/Plugins/12345/ HTTP/1.1
Host: api.bsn.cloud
Connection: Keep-Alive
Authorization: Bearer {{UserAccessToken}}}
Accept: application/json, application/vnd.bsn.error+json
Accept-Encoding: gzip,deflate
```

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Success Response**

204: The specified autorun plugin has been removed from the network 

**Failure Response**

300: The requested representation could not be returned because it is ambiguous (there are multiple requested representations)

400: The request or request body is malformed and therefore invalid, or it is rejected in accordance with the business rules

401: The access token is invalid or not specified

403: The supplied access token, though valid, doesn't provide access to this method

404: The server cannot find the requested resource

406: The server cannot return the data representation that you requested (as specified in the "Accept" header)

412: Precondition failed (the resource changed since the time specified in the “If-Unmodified-Since” header value)

5XX: Any 500 code is an internal server error
