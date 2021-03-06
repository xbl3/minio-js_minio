# JavaScript Client API Reference [![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/Minio/minio?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## Initialize Minio Client object.  

## Minio

```js

var Minio = require('minio')

var minioClient = new Minio({
    endPoint: 'play.minio.io',
    port: 9000,
  	secure: true,
    accessKey: 'Q3AM3UQ867SPQQA43P2F',
    secretKey: 'zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG'
});

```

## AWS S3

```js

var Minio = require('minio')

var s3Client = new Minio({
    endPoint:  's3.amazonaws.com',
	  accessKey: 'YOUR-ACCESSKEYID',
	  secretKey: 'YOUR-SECRETACCESSKEY'
})

```

| Bucket operations       | Object operations      | Presigned operations |
| ------------- |-------------| -----|
| [`makeBucket`](#makeBucket)    | [`getObject`](#getObject) | [`presignedGetObject`](#presignedGetObject) |
| [`listBuckets`](#listBuckets)  | [`getPartialObject`](#getPartialObject)    |   [`presignedPutObject`](#presignedPutObject) |
| [`bucketExists`](#bucketExists) | [`fGetObject`](#fGetObject)    |    [`presignedPostPolicy`](#presignedPostPolicy) |
| [`removeBucket`](#removeBucket)      | [`putObject`](#putObject)       |
| [`listObjects`](#listObjects) | [`fPutObject`](#fPutObject)   |
| [`listIncompleteUploads`](#listIncompleteUploads) |[`statObject`](#statObject) |
|     |  [`removeObject`](#removeObject)    |
|  | [`removeIncompleteUpload`](#removeIncompleteUpload)  |


## 1.  Constructor

<a name="MinioClient_endpoint"></a>
###  new Minio ({endPoint, port, secure, accessKey, secretKey})

|     |
| ---- |
|``new Minio ({endPoint, port, secure, accessKey, secretKey})``|
|Initializes a new client object.|

__Parameters__


<table>
    <thead>
        <tr>
            <th>Param</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
         <code>  endPoint <code>
            </td>
            <td>
           <i>  string </i>
            </td>
            <td>
            endPoint is an URL, domain name, IPv4 or IPv6 address.
<br/>Valid endpoints:
                <ul>
                    <li>https://s3.amazonaws.com</li>
                    <li>https://s3.amazonaws.com/</li>
                    <li>https://play.minio.io:9000</li>
                    <li>http://play.minio.io:9010/</li>
                    <li>localhost</li>
                    <li>localhost.localdomain</li>
                    <li>play.minio.io</li>
                    <li>127.0.0.1</li>
                    <li>192.168.1.60</li>
                    <li>::1</li>
                </ul>
            </td>
        </tr>
        <tr>
         <td>
          <code>  port </code>
            </td>
            <td>
           <i> number </i>
            </td>
            <td>
            TCP/IP port number. This input is optional. Default value set to 80 for HTTP and 443 for HTTPs.
            </td>
        </tr>
        <tr>
        <td> <code> accessKey </code> </td>
        <td> <i> string </i> </td>
        <td>accessKey is like user-id that uniquely identifies your account.</td>
        </tr>
        <tr>
        <td> <code> secretKey </code> </td>
        <td> <i> string </i> </td>
        <td> secretKey is the password to your account.</td>
        </tr>
        <tr>
        <td> <code> secure </code> </td>
        <td> <i> bool </i> </td>
        <td>If set to true, https is used instead of http. Default is https if not set. </td>
        </tr>
    </tbody>
</table>


__Example__

## Minio

```js

var Minio = require('minio')

var minioClient = new Minio({
    endPoint: 'play.minio.io',
    port: 9000,
    secure: true,
    accessKey: 'Q3AM3UQ867SPQQA43P2F',
    secretKey: 'zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG'
});

```

## AWS S3


```js


var Minio = require('minio')

var s3Client = new Minio({
    endPoint:  's3.amazonaws.com',
    accessKey: 'YOUR-ACCESSKEYID',
    secretKey: 'YOUR-SECRETACCESSKEY'
})


```


## 2. Bucket operations
<a name="makeBucket"></a>

### makeBucket(bucketName, region, callback)

Creates a new bucket.

__Parameters__


<table>
    <thead>
        <tr>
            <th>Param</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
          <code> bucketName </code>
            </td>
            <td>
            <i> string </i>
            </td>
            <td>
            Name of the bucket.
            </td>
        </tr>
        <tr>
         <td>
           <code> region </code>
            </td>
            <td>
            <i> string </i>
            </td>
            <td>
            Default value is us-east-1
Region where the bucket is created. Valid values are [  <i> us-east-1, us-west-1, us-west-2, eu-west-1, eu-central-1, ap-southeast-1, ap-northeast-1,
ap-southeast-2, sa-east-1 </i> ].
            </td>
        </tr>
        <tr>
        <td> <code> callback(err) </code> </td>
        <td> <i> function </i> </td>
        <td>Callback function with <code>err</code> as the error argument. <code>err</code>  is null if the bucket is successfully created. </td>
        </tr>
    </tbody>
</table>



__Example__


```js

minioClient.makeBucket('mybucket', 'us-east-1', function(err) {
  if (err) return console.log('Error creating bucket.', err)
  console.log('Bucket created successfully in "us-east-1".')
})

```

<a name="listBuckets"></a>
### listBuckets(callback)

Lists all buckets.


__Parameters__


<table>
    <thead>
        <tr>
            <th>Param</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
           <code> callback(err, bucketStream) </code>
            </td>
            <td>
            <i> function </i>
            </td>
            <td>
            Callback function with error as the first argument.
  <code>bucketStream</code> is the stream emitting bucket information.
  <br/><code>bucketStream</code> emits Object with the format:-
                <ul>
                    <li> <code>bucket.name</code> <i>string</i> : bucket name</li>
                    <li> <code>bucket.creationDate</code> <i>Date</i> : date when bucket was created.</li>

                </ul>
            </td>
        </tr>

    </tbody>
</table>


__Example__


```js

minioClient.listBuckets(function(err, buckets) {
  if (err) return console.log(err)
  console.log('buckets :', buckets)
})

```

<a name="bucketExists"></a>
#### bucketExists(bucketName, callback)

Checks if a bucket exists.


__Parameters__


| Param  | Type  | Description  |
|---|---|---|
| `bucketName`  |  _string_ | Name of the bucket.  |
| `callback(err)`  | _function_  | `err` is `null` if the bucket exists. `err.code` is `NoSuchBucket` in case the bucket does not exist. |

__Example__


```js


minioClient.bucketExists('mybucket', function(err) {
  if (err) {
     if (err.code == 'NoSuchBucket') return console.log("bucket does not exist.")
     return console.log(err)
  }
  // if err is null it indicates that the bucket exists.
  console.log('Bucket exists.')
})

```
<a name="removeBucket"></a>
### removeBucket(bucketName, callback)

Removes a bucket.

__Parameters__


| Param  |  Type | Description  |
|---|---|---|
| `bucketName`  | _string_  | Name of the bucket.  |
| `callback(err)`  | _function_  |  `err` is `null` if the bucket is removed successfully. |

__Example__


```js

minioClient.removeBucket('mybucket', function(err) {
  if (err) return console.log('unable to remove bucket.')
  console.log('Bucket removed successfully.')
})


```

<a name="listObjects"></a>
### listObjects(bucketName, prefix, recursive)

Lists all objects in a bucket.

__Parameters__


| Param | Type | Description |
| ---- | ---- | ---- |
| `bucketName` | _string_ | Name of the bucket. |
| `prefix`  | _string_  |  The prefix of the objects that should be listed (optional, default `''`). |
| `recursive`  | _bool_  | `true` indicates recursive style listing and `false` indicates directory style listing delimited by '/'. (optional, default `false`).  |


__Return Value__


<table>
    <thead>
        <tr>
            <th>Param</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
          <code> stream </code>
            </td>
            <td>
           <i> Stream </i>
            </td>
            <td>
            Stream emitting the objects in the bucket, the object is of the format:
                <ul>
                    <li> <code>obj.key</code> <i>string</i>: name of the object.</li>
                    <li> <code>obj.size</code> <i>number</i>: size of the object.</li>
                    <li> <code>obj.etag</code> <i>string</i>: etag of the object.</li>
                    <li> <code>obj.lastModified</code> <i>Date</i>: modified time stamp.</li>
                </ul>
            </td>
        </tr>

    </tbody>
</table>



__Example__


```js

var stream = minioClient.listObjects('mybucket','', true)
stream.on('data', function(obj) { console.log(obj) } )
stream.on('error', function(err) { console.log(err) } )

```

<a name="listIncompleteUploads"></a>
### listIncompleteUploads(bucketName, prefix, recursive)

Lists partially uploaded objects in a bucket.

__Parameters__


| Param  |  Type | Description  |
| ---| ---|---|
| `bucketname`  | _string_  |  Name of the bucket. |
| `prefix`  | _string_  | Prefix of the object names that are partially uploaded. (optional, default `''`)  |
| `recursive`  | _bool_  | `true` indicates recursive style listing and `false` indicates directory style listing delimited by '/'. (optional, default `false`).  |


__Return Value__


<table>
    <thead>
        <tr>
            <th>Param</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
           <code> stream </code>
            </td>
            <td>
          <i> Stream </i>
            </td>
            <td>
            Emits objects of the format:

                <ul>
                    <li> <code>part.key</code> <i>string</i>: name of the object.</li>
                    <li> <code>part.uploadId</code> <i>string</i>: upload ID of the object.</li>
                    <li> <code>part.size</code> <i>Integer</i>: size of the partially uploaded object.</li>
                </ul>
            </td>
        </tr>

    </tbody>
</table>


__Example__


```js

var Stream = minioClient.listIncompleteUploads('mybucket', '', true)
Stream.on('data', function(obj) {
  console.log(obj)
})
Stream.on('end', function() {
  console.log('End')
})
Stream.on('error', function(err) {
  console.log(err)
})

```

## 3.  Object operations

<a name="getObject"></a>
### getObject(bucketName, objectName, callback)

Downloads an object as a stream.

__Parameters__


| Param  |  Type | Description  |
|---|---|---|
| `bucketName`  | _string_  | Name of the bucket.  |
| `objectName`  | _string_  |  Name of the object. |
| `callback(err, stream)` | _function_ | Callback is called with `err` in case of error. `stream` is the object content stream.|

__Example__


```js

var size = 0
minioClient.getObject('mybucket', 'photo.jpg', function(err, dataStream) {
  if (err) {
    return console.log(err)
  }
  dataStream.on('data', function(chunk) {
    size += chunk.length
  })
  dataStream.on('end', function() {
    console.log('End. Total size = ' + size)
  })
  dataStream.on('error', function(err) {
    console.log(err)
  })
})

```
<a name="getPartialObject"></a>
### getPartialObject(bucketName, objectName, offset, length, callback)

Downloads the specified range bytes of an object as a stream.

__Parameters__


| Param  |  Type | Description  |
|---|---|---|
|  `bucketName` | _string_  | Name of the bucket.  |
| `objectName`   | _string_  | Name of the object.  |
| `offset`   | _number_  | `offset` of the object from where the stream will start.  |
| `length`  | _number_  | `length` of the object that will be read in the stream (optional, if not specified we read the rest of the file from the offset).  |
|`callback(err, stream)` | _function_  | Callback is called with `err` in case of error. `stream` is the object content stream.|

__Example__


```js

var size = 0
// reads 30 bytes from the offset 10.
minioClient.getPartialObject('mybucket', 'photo.jpg', 10, 30, function(err, dataStream) {
  if (err) {
    return console.log(err)
  }
  dataStream.on('data', function(chunk) {
    size += chunk.length
  })
  dataStream.on('end', function() {
    console.log('End. Total size = ' + size)
  })
  dataStream.on('error', function(err) {
    console.log(err)
  })
})

```

<a name="fGetObject"></a>
### fGetObject(bucketName, objectName, filePath, callback)

Downloads and saves the object as a file in the local filesystem.

__Parameters__



| Param  |  Type | Description  |
|---|---|---|
| `bucketName`  | _string_   | Name of the bucket.  |
| `objectName`  |_string_   | Name of the object.  |
| `filePath`  |  _string_ | Path on the local filesystem to which the object data will be written.  |
| `callback(err)`  | _function_  | Callback is called with `err` in case of error.  |


__Example__


```js

var size = 0
minioClient.fGetObject('mybucket', 'photo.jpg', '/tmp/photo.jpg', function(err) {
  if (err) {
    return console.log(err)
  }
  console.log('success')
})

```
<a name="putObject"></a>
### putObject(bucketName, objectName, stream, size, contentType, callback)

Uploads an object from a stream/Buffer.


##### From a stream

__Parameters__


| Param  |  Type | Description  |
|---|---|---|
| `bucketName`  |_string_   | Name of the bucket.  |
| `objectName`  |_string_   | Name of the object.  |
| `stream`  | _Stream_  |Readable stream.   |
|`size`   | _number_  | Size of the object.  |
|`contentType`   | _string_  | Content-Type of the object (optional, default `application/octet-stream`).  |
| `callback(err, etag)` | _function_ | Non-null `err` indicates error, `etag` _string_ is the etag of the object uploaded.|

__Example__

The maximum size of a single object is limited to 5TB. putObject transparently uploads objects larger than 5MiB in multiple parts. This allows failed uploads to resume safely by only uploading the missing parts. Uploaded data is carefully verified using MD5SUM signatures.

```js

var Fs = require('fs')
var file = '/tmp/40mbfile'
var fileStream = Fs.createReadStream(file)
var fileStat = Fs.stat(file, function(err, stats) {
  if (err) {
    return console.log(err)
  }
  minioClient.putObject('mybucket', '40mbfile', fileStream, stats.size, 'application/octet-stream', function(err, etag) {
    return console.log(err, etag) // err should be null
  })
})

```

##### From a "Buffer" or a "string"

__Parameters__


| Param  |  Type | Description  |
|---|---|---|
| `bucketName`  |_string_   | Name of the bucket.  |
| `objectName`  |_string_   | Name of the object.  |
|`string or Buffer`   | _Stream_ or _Buffer_  |Readable stream.   |
| `contentType`  | _string_   | Content-Type of the object (optional, default `application/octet-stream`).  |
| `callback(err, etag)`  | _function_  |Non-null `err` indicates error, `etag` _string_ is the etag of the object uploaded.   |


__Example__


```js

var buffer = 'Hello World'
minioClient.putObject('mybucket', 'hello-file', buffer, 'application/octet-stream', function(err, etag) {
  return console.log(err, etag) // err should be null
})

```
<a name="fPutObject"></a>
### fPutObject(bucketName, objectName, filePath, contentType, callback)

Uploads contents from a file to objectName.

__Parameters__


| Param  |  Type | Description  |
|---|---|---|
| `bucketName`  | _string_  | Name of the bucket.  |
|`objectName`   |_string_   | Name of the object.  |
| `filePath`  | _string_  | Path of the file to be uploaded.  |
| `contentType`  | _string_  | Content-Type of the object.  |
| `callback(err, etag)`  |  _function_ | Non-null `err` indicates error, `etag` _string_ is the etag of the object uploaded.  |

__Example__


The maximum size of a single object is limited to 5TB. fPutObject transparently uploads objects larger than 5MiB in multiple parts. This allows failed uploads to resume safely by only uploading the missing parts. Uploaded data is carefully verified using MD5SUM signatures.

```js

var file = '/tmp/40mbfile'
minioClient.fPutObject('mybucket', '40mbfile', file, 'application/octet-stream', function(err, etag) {
  return console.log(err, etag) // err should be null
})

```

<a name="statObject"></a>
### statObject(bucketName, objectName, callback)

Gets metadata of an object.

__Parameters__


<table>
    <thead>
        <tr>
            <th>Param</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
           <code> bucketName </code>
            </td>
            <td>
            <i> string </i>
            </td>
            <td>
            Name of the bucket.
            </td>
           </tr>
          <tr>
          <td> <code> objectName </code> </td>
          <td> <i> string </i> </td>
          <td>Name of the object.</td>
          </tr>       
        <tr>
         <td>
           <code> callback(err, stat) </code>
            </td>
            <td>
           <i> function </i>
            </td>
            <td>
            <code>err</code> is not <code>null</code> in case of error, <code>stat</code> contains the object information:
                <ul>
                    <li> <code>stat.size</code> <i>number</i>: size of the object.</li>
                    <li> <code>stat.etag</code> <i>string</i>: etag of the object.</li>
                    <li> <code>stat.contentType</code> <i>string</i>: Content-Type of the object.</li>
                    <li> <code>stat.lastModified</code> <i>string</i>: modified time stamp.</li>
                </ul>
            </td>
            </td>
        </tr>
    </tbody>
</table>


__Example__


```js

minioClient.statObject('mybucket', 'photo.jpg', function(err, stat) {
  if (err) {
    return console.log(err)
  }
  console.log(stat)
})

```

<a name="removeObject"></a>
### removeObject(bucketName, objectName, callback)

Removes an object.

__Parameters__


| Param  |  Type | Description  |
|---|---|---|
|`bucketName`   |  _string_ | Name of the bucket.  |
| objectName  |  _string_ | Name of the object.  |
| `callback(err)`  | _function_  | Callback function is called with non `null` value in case of error.  |


__Example__


```js

minioClient.removeObject('mybucket', 'photo.jpg', function(err) {
  if (err) {
    return console.log('Unable to remove object', err)
  }
  console.log('Removed the object')
})

```

<a name="removeIncompleteUpload"></a>
### removeIncompleteUpload(bucketName, objectName, callback)

Removes a partially uploaded object.

__Parameters__


| Param  |  Type | Description  |
|---|---|---|
| `bucketName`  |_string_   | Name of the bucket.  |
| `objectName`  | _string_  | Name of the object.  |
| `callback(err)`  | _function_  |Callback function is called with non `null` value in case of error.   |


__Example__


```js

minioClient.removeIncompleteUpload('mybucket', 'photo.jpg', function(err) {
  if (err) {
    return console.log('Unable to remove incomplete object', err)
  }
  console.log('Incomplete object removed successfully.')
})

```

## 4. Presigned operations

Presigned URLs are generated for temporary download/upload access to private objects.

<a name="presignedGetObject"></a>
### presignedGetObject(bucketName, objectName, expiry, cb)

Generates a presigned URL for HTTP GET operations. Browsers/Mobile clients may point to this URL to directly download objects even if the bucket is private. This presigned URL can have an associated expiration time in seconds after which the URL is no longer valid. The default expiry is set to 7 days.


__Parameters__



| Param  |  Type | Description  |
|---|---|---|
| `bucketName`  | _string_  | Name of the bucket.  |
|`objectName`   | _string_  | Name of the object.  |
| `expiry`  |_number_   | Expiry in seconds. Default expiry is set to 7 days.  |
| `callback(err, presignedUrl)`  | _function_  | Callback function is called with non `null` err value in case of error. `presignedUrl` will be the URL using which the object can be downloaded using GET request.  |


__Example__


```js

// expires in a day.
minioClient.presignedGetObject('mybucket', 'hello.txt', 24*60*60, function(err, presignedUrl) {
  if (err) return console.log(err)
  console.log(presignedUrl)
})

```

<a name="presignedPutObject"></a>
### presignedPutObject(bucketName, objectName, expiry, callback)

Generates a presigned URL for HTTP PUT operations. Browsers/Mobile clients may point to this URL to upload objects directly to a bucket even if it is private.  This presigned URL can have an associated expiration time in seconds after which the URL is no longer valid. The default expiry is set to 7 days.


__Parameters__


| Param  |  Type | Description  |
|---|---|---|
| `bucketName`  | _string_  | Name of the bucket.  |
| `objectName`  | _string_  | Name of the object.  |
| `expiry`  | _number_   | Expiry in seconds. Default expiry is set to 7 days.  |
| `callback(err, presignedUrl)`  | _function_  | Callback function is called with non `null` err value in case of error. `presignedUrl` will be the URL using which the object can be uploaded using PUT request.  |


__Example__


```js

// expires in a day.
minioClient.presignedPutObject('mybucket', 'hello.txt', 24*60*60, function(err, presignedUrl) {
  if (err) return console.log(err)
  console.log(presignedUrl)
})

```

<a name="presignedPostPolicy"></a>
### presignedPostPolicy(policy, callback)

Allows setting policy conditions to a presigned URL for POST operations. Policies such as bucket name to receive object uploads, key name prefixes, expiry policy may be set.

__Parameters__


| Param  |  Type | Description  |
|---|---|---|
| `policy`  | _object_  | Policy object created by minioClient.newPostPolicy() |
| `callback(err, postURL, formData)`  | _function_  | Callback function is called with non `null` err value in case of error. `postURL` will be the URL using which the object can be uploaded using POST request. `formData` is the object having key/value pairs for the Form data of POST body. |


Create policy:


```js

var policy = minioClient.newPostPolicy()

```

Apply upload policy restrictions:

```js

// Policy restricted only for bucket 'mybucket'.
policy.setBucket('mybucket')

// Policy restricted only for hello.txt object.
policy.setKey('hello.txt')

```
or

```js

// Policy restricted for incoming objects with keyPrefix.
policy.setKeyStartsWith('keyPrefix')

var expires = new Date
expires.setSeconds(24 * 60 * 60 * 10)
// Policy expires in 10 days.
policy.setExpires(expires)

// Only allow 'text'.
policy.setContentType('text/plain')

// Only allow content size in range 1KB to 1MB.
policy.setContentLengthRange(1024, 1024*1024)

```

POST your content from the browser using `superagent`:


```js

minioClient.presignedPostPolicy(policy, function(err, postURL, formData) {
  if (err) return console.log(err)

  var req = superagent.post(postURL)
  _.each(formData, function(value, key) {
    req.field(key, value)
  })

  // file contents.
  req.attach('file', '/path/to/hello.txt', 'hello.txt')

  req.end(function(err, res) {
    if (err) {
      return console.log(err.toString())
    }
    console.log('Upload successful.')
  })
})

```

## 5. Explore Further


- [Build your own Shopping App Example](https://docs.minio.io/docs/javascript-shopping-app)
