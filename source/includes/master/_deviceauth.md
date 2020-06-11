

<!-- Generator: Widdershins v3.6.6 -->

<h1 id="device-authentication">Device authentication v2</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

An API for device authentication handling.

Base URLs:

* <a href="http://mender-device-auth:8080/api/management/v2/devauth/">http://mender-device-auth:8080/api/management/v2/devauth/</a>

<h1 id="device-authentication-default">Default</h1>

## Get a list of tenant's devices.

> Code samples

```shell
# You can also use wget
curl -X GET http://mender-device-auth:8080/api/management/v2/devauth/devices \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
GET http://mender-device-auth:8080/api/management/v2/devauth/devices HTTP/1.1
Host: mender-device-auth:8080
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/devices',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.get 'http://mender-device-auth:8080/api/management/v2/devauth/devices',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.get('http://mender-device-auth:8080/api/management/v2/devauth/devices', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','http://mender-device-auth:8080/api/management/v2/devauth/devices', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/devices");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://mender-device-auth:8080/api/management/v2/devauth/devices", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /devices`

Provides a list of tenant's devices, sorted by creation date, with optional device status filter.

<h3 id="get-a-list-of-tenant's-devices.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|status|query|string|false|Device status filter. If not specified, all devices are listed.|
|page|query|number(integer)|false|Results page number|
|per_page|query|number(integer)|false|Number of results per page|

#### Detailed descriptions

**status**: Device status filter. If not specified, all devices are listed.

#### Enumerated Values

|Parameter|Value|
|---|---|
|status|pending|
|status|accepted|
|status|rejected|
|status|preauthorized|

> Example responses

> 200 Response

<h3 id="get-a-list-of-tenant's-devices.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|An array of devices.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Missing/malformed request params.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected error|[Error](#schemaerror)|

<h3 id="get-a-list-of-tenant's-devices.-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Device](#schemadevice)]|false|none|none|
|» id|string|false|none|Mender assigned Device ID.|
|» identity_data|[IdentityData](#schemaidentitydata)|false|none|Device identity attributes, in the form of a JSON structure.<br><br>The attributes are completely vendor-specific, the provided ones are just an example.<br>In reference implementation structure contains vendor-selected fields,<br>such as MACs, serial numbers, etc.|
|»» mac|string|false|none|MAC address.|
|»» sku|string|false|none|Stock keeping unit.|
|»» sn|string|false|none|Serial number.|
|» status|string|false|none|none|
|» created_ts|string(datetime)|false|none|Created timestamp|
|» updated_ts|string(datetime)|false|none|Updated timestamp|
|» auth_sets|[[AuthSet](#schemaauthset)]|false|none|[Authentication data set]|
|»» id|string|false|none|Authentication data set ID.|
|»» pubkey|string|false|none|The device's public key, generated by the device or pre-provisioned by the vendor.|
|»» identity_data|[IdentityData](#schemaidentitydata)|false|none|Device identity attributes, in the form of a JSON structure.<br><br>The attributes are completely vendor-specific, the provided ones are just an example.<br>In reference implementation structure contains vendor-selected fields,<br>such as MACs, serial numbers, etc.|
|»» status|string|false|none|none|
|»» ts|string(datetime)|false|none|Created timestamp|
|» decommissioning|boolean|false|none|Devices that are part of ongoing decomissioning process will return True|

#### Enumerated Values

|Property|Value|
|---|---|
|status|pending|
|status|accepted|
|status|rejected|
|status|preauthorized|
|status|pending|
|status|accepted|
|status|rejected|
|status|preauthorized|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Link|string||Standard header, we support 'first', 'next', and 'prev'.|

<aside class="success">
This operation does not require authentication
</aside>

## Submit a preauthorized device.

> Code samples

```shell
# You can also use wget
curl -X POST http://mender-device-auth:8080/api/management/v2/devauth/devices \
  -H 'Content-Type: application/json' \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
POST http://mender-device-auth:8080/api/management/v2/devauth/devices HTTP/1.1
Host: mender-device-auth:8080
Content-Type: application/json
Accept: */*
Authorization: string

```

```javascript
const inputBody = '{
  "application/json": {
    "identity_data": {
      "mac": "00:01:02:03:04:05",
      "sku": "My Device 1",
      "sn": "SN1234567890"
    },
    "pubkey": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzogVU7RGDilbsoUt/DdH\nVJvcepl0A5+xzGQ50cq1VE/Dyyy8Zp0jzRXCnnu9nu395mAFSZGotZVr+sWEpO3c\nyC3VmXdBZmXmQdZqbdD/GuixJOYfqta2ytbIUPRXFN7/I7sgzxnXWBYXYmObYvdP\nokP0mQanY+WKxp7Q16pt1RoqoAd0kmV39g13rFl35muSHbSBoAW3GBF3gO+mF5Ty\n1ddp/XcgLOsmvNNjY+2HOD5F/RX0fs07mWnbD7x+xz7KEKjF+H7ZpkqCwmwCXaf0\niyYyh1852rti3Afw4mDxuVSD7sd9ggvYMc0QHIpQNkD4YWOhNiE1AB0zH57VbUYG\nUwIDAQAB\n-----END PUBLIC KEY-----\n"
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/devices',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.post 'http://mender-device-auth:8080/api/management/v2/devauth/devices',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.post('http://mender-device-auth:8080/api/management/v2/devauth/devices', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('POST','http://mender-device-auth:8080/api/management/v2/devauth/devices', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/devices");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "http://mender-device-auth:8080/api/management/v2/devauth/devices", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /devices`

Adds a given device/authentication data set in the 'preauthorized' state. The device identity data set must not yet exist in the DB (regardless of status).

When the device requests authentication from deviceauth the next time, it will be issued a token without further user intervention.

> Body parameter

```json
{
  "application/json": {
    "identity_data": {
      "mac": "00:01:02:03:04:05",
      "sku": "My Device 1",
      "sn": "SN1234567890"
    },
    "pubkey": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzogVU7RGDilbsoUt/DdH\nVJvcepl0A5+xzGQ50cq1VE/Dyyy8Zp0jzRXCnnu9nu395mAFSZGotZVr+sWEpO3c\nyC3VmXdBZmXmQdZqbdD/GuixJOYfqta2ytbIUPRXFN7/I7sgzxnXWBYXYmObYvdP\nokP0mQanY+WKxp7Q16pt1RoqoAd0kmV39g13rFl35muSHbSBoAW3GBF3gO+mF5Ty\n1ddp/XcgLOsmvNNjY+2HOD5F/RX0fs07mWnbD7x+xz7KEKjF+H7ZpkqCwmwCXaf0\niyYyh1852rti3Afw4mDxuVSD7sd9ggvYMc0QHIpQNkD4YWOhNiE1AB0zH57VbUYG\nUwIDAQAB\n-----END PUBLIC KEY-----\n"
  }
}
```

<h3 id="submit-a-preauthorized-device.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|body|body|[PreAuthSet](#schemapreauthset)|true|Preauthentication request.|

> Example responses

> 400 Response

<h3 id="submit-a-preauthorized-device.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Device submitted.|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Missing/malformed request params.|[Error](#schemaerror)|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|Device already exists. Response contains conflicting device.|[Device](#schemadevice)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected error|[Error](#schemaerror)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|string||URL of the newly created user-ID.|

<aside class="success">
This operation does not require authentication
</aside>

## Get a particular device.

> Code samples

```shell
# You can also use wget
curl -X GET http://mender-device-auth:8080/api/management/v2/devauth/devices/{id} \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
GET http://mender-device-auth:8080/api/management/v2/devauth/devices/{id} HTTP/1.1
Host: mender-device-auth:8080
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.get 'http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.get('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /devices/{id}`

<h3 id="get-a-particular-device.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Device identifier|

> Example responses

> 200 Response

<h3 id="get-a-particular-device.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Device found.|[Device](#schemadevice)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Device not found.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected error|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Decommission device

> Code samples

```shell
# You can also use wget
curl -X DELETE http://mender-device-auth:8080/api/management/v2/devauth/devices/{id} \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
DELETE http://mender-device-auth:8080/api/management/v2/devauth/devices/{id} HTTP/1.1
Host: mender-device-auth:8080
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.delete 'http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.delete('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('DELETE','http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /devices/{id}`

<h3 id="decommission-device-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Device identifier.|

> Example responses

> 404 Response

<h3 id="decommission-device-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|Device decommissioned.|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Device not found|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal server error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Remove the device authentication set

> Code samples

```shell
# You can also use wget
curl -X DELETE http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid} \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
DELETE http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid} HTTP/1.1
Host: mender-device-auth:8080
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.delete 'http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.delete('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('DELETE','http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /devices/{id}/auth/{aid}`

Removes the device authentication set.
Removing 'accepted' authentication set is equivalent
to rejecting device and removing authentication set.
If there is only one authentication set for the device
and the device is 'preauthorized' then the device
will also be deleted.

<h3 id="remove-the-device-authentication-set-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Device identifier.|
|aid|path|string|true|Authentication data set identifier.|

> Example responses

> 404 Response

<h3 id="remove-the-device-authentication-set-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|Device authentication set deleted.|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Device authentication set not found|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal server error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update the device authentication set status

> Code samples

```shell
# You can also use wget
curl -X PUT http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status \
  -H 'Content-Type: application/json' \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
PUT http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status HTTP/1.1
Host: mender-device-auth:8080
Content-Type: application/json
Accept: */*
Authorization: string

```

```javascript
const inputBody = '{
  "application/json": {
    "status": "accepted"
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.put 'http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.put('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('PUT','http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`PUT /devices/{id}/auth/{aid}/status`

Sets the status of a authentication data set of selected value.
Valid state transitions:
- 'pending' -> 'accepted'
- 'pending' -> 'rejected'
- 'rejected' -> 'accepted'
- 'accepted' -> 'rejected'

> Body parameter

```json
{
  "application/json": {
    "status": "accepted"
  }
}
```

<h3 id="update-the-device-authentication-set-status-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Device identifier.|
|aid|path|string|true|Authentication data set identifier.|
|body|body|[Status](#schemastatus)|true|New status.|

> Example responses

> 400 Response

<h3 id="update-the-device-authentication-set-status-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|The device authentication data set status was successfully updated.|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad request.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The device was not found.|[Error](#schemaerror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Request cannot be fulfilled e.g. due to exceeded limit on maximum accepted devices (see error message).|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal server error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Get the device authentication set status

> Code samples

```shell
# You can also use wget
curl -X GET http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
GET http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status HTTP/1.1
Host: mender-device-auth:8080
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.get 'http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.get('http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://mender-device-auth:8080/api/management/v2/devauth/devices/{id}/auth/{aid}/status", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /devices/{id}/auth/{aid}/status`

Returns the status of a particular device authentication data set.

<h3 id="get-the-device-authentication-set-status-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Device identifier.|
|aid|path|string|true|Authentication data set identifier.|

> Example responses

> 200 Response

> successful response - the device's authentication set status is returned.

```json
{
  "status": "accepted"
}
```

<h3 id="get-the-device-authentication-set-status-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful response - the device's authentication set status is returned.|[Status](#schemastatus)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The device was not found.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal server error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Get a count of devices, optionally filtered by status.

> Code samples

```shell
# You can also use wget
curl -X GET http://mender-device-auth:8080/api/management/v2/devauth/devices/count \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
GET http://mender-device-auth:8080/api/management/v2/devauth/devices/count HTTP/1.1
Host: mender-device-auth:8080
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/devices/count',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.get 'http://mender-device-auth:8080/api/management/v2/devauth/devices/count',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.get('http://mender-device-auth:8080/api/management/v2/devauth/devices/count', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','http://mender-device-auth:8080/api/management/v2/devauth/devices/count', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/devices/count");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://mender-device-auth:8080/api/management/v2/devauth/devices/count", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /devices/count`

Provides a list of devices, optionally filtered by status.

<h3 id="get-a-count-of-devices,-optionally-filtered-by-status.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|status|query|string|false|Device status filter, one of 'pending', 'accepted', 'rejected'. Default is 'all devices'.|

#### Detailed descriptions

**status**: Device status filter, one of 'pending', 'accepted', 'rejected'. Default is 'all devices'.

> Example responses

> 200 Response

<h3 id="get-a-count-of-devices,-optionally-filtered-by-status.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Device count.|[Count](#schemacount)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Missing/malformed request params.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected error|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete device token

> Code samples

```shell
# You can also use wget
curl -X DELETE http://mender-device-auth:8080/api/management/v2/devauth/tokens/{id} \
  -H 'Accept: */*'

```

```http
DELETE http://mender-device-auth:8080/api/management/v2/devauth/tokens/{id} HTTP/1.1
Host: mender-device-auth:8080
Accept: */*

```

```javascript

const headers = {
  'Accept':'*/*'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/tokens/{id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => '*/*'
}

result = RestClient.delete 'http://mender-device-auth:8080/api/management/v2/devauth/tokens/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': '*/*'
}

r = requests.delete('http://mender-device-auth:8080/api/management/v2/devauth/tokens/{id}', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => '*/*',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('DELETE','http://mender-device-auth:8080/api/management/v2/devauth/tokens/{id}', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/tokens/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"*/*"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "http://mender-device-auth:8080/api/management/v2/devauth/tokens/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /tokens/{id}`

Deletes the token, effectively revoking it. The device must
apply for a new one with a new authentication request.
The token 'id' corresponds to the standard 'jti' claim.

<h3 id="delete-device-token-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|string|true|Unique token identifier('jti').|

> Example responses

> 404 Response

<h3 id="delete-device-token-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|The token was successfully deleted.|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The token was not found.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal server error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Obtain limit of accepted devices.

> Code samples

```shell
# You can also use wget
curl -X GET http://mender-device-auth:8080/api/management/v2/devauth/limits/max_devices \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
GET http://mender-device-auth:8080/api/management/v2/devauth/limits/max_devices HTTP/1.1
Host: mender-device-auth:8080
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('http://mender-device-auth:8080/api/management/v2/devauth/limits/max_devices',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.get 'http://mender-device-auth:8080/api/management/v2/devauth/limits/max_devices',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.get('http://mender-device-auth:8080/api/management/v2/devauth/limits/max_devices', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','http://mender-device-auth:8080/api/management/v2/devauth/limits/max_devices', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://mender-device-auth:8080/api/management/v2/devauth/limits/max_devices");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://mender-device-auth:8080/api/management/v2/devauth/limits/max_devices", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /limits/max_devices`

<h3 id="obtain-limit-of-accepted-devices.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and|

#### Detailed descriptions

**Authorization**: Contains the JWT token issued by the User Administration and
Authentication Service.

> Example responses

> 200 Response

<h3 id="obtain-limit-of-accepted-devices.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Usage statistics and limits.|[Limit](#schemalimit)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal server error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocS_Status">Status</h2>
<!-- backwards compatibility -->
<a id="schemastatus"></a>
<a id="schema_Status"></a>
<a id="tocSstatus"></a>
<a id="tocsstatus"></a>

```json
{
  "application/json": {
    "status": "accepted"
  }
}

```

Admission status of the device.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|string|true|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|status|pending|
|status|accepted|
|status|rejected|

<h2 id="tocS_Limit">Limit</h2>
<!-- backwards compatibility -->
<a id="schemalimit"></a>
<a id="schema_Limit"></a>
<a id="tocSlimit"></a>
<a id="tocslimit"></a>

```json
{
  "application/json": {
    "limit": 123
  }
}

```

Limit definition

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|limit|integer|true|none|none|

<h2 id="tocS_Device">Device</h2>
<!-- backwards compatibility -->
<a id="schemadevice"></a>
<a id="schema_Device"></a>
<a id="tocSdevice"></a>
<a id="tocsdevice"></a>

```json
{
  "id": "string",
  "identity_data": {
    "application/json": {
      "mac": "00:01:02:03:04:05",
      "sku": "My Device 1",
      "sn": "SN1234567890"
    }
  },
  "status": "pending",
  "created_ts": "string",
  "updated_ts": "string",
  "auth_sets": [
    {
      "id": "string",
      "pubkey": "string",
      "identity_data": {
        "application/json": {
          "mac": "00:01:02:03:04:05",
          "sku": "My Device 1",
          "sn": "SN1234567890"
        }
      },
      "status": "pending",
      "ts": "string"
    }
  ],
  "decommissioning": true
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|Mender assigned Device ID.|
|identity_data|[IdentityData](#schemaidentitydata)|false|none|Device identity attributes, in the form of a JSON structure.<br><br>The attributes are completely vendor-specific, the provided ones are just an example.<br>In reference implementation structure contains vendor-selected fields,<br>such as MACs, serial numbers, etc.|
|status|string|false|none|none|
|created_ts|string(datetime)|false|none|Created timestamp|
|updated_ts|string(datetime)|false|none|Updated timestamp|
|auth_sets|[[AuthSet](#schemaauthset)]|false|none|[Authentication data set]|
|decommissioning|boolean|false|none|Devices that are part of ongoing decomissioning process will return True|

#### Enumerated Values

|Property|Value|
|---|---|
|status|pending|
|status|accepted|
|status|rejected|
|status|preauthorized|

<h2 id="tocS_AuthSet">AuthSet</h2>
<!-- backwards compatibility -->
<a id="schemaauthset"></a>
<a id="schema_AuthSet"></a>
<a id="tocSauthset"></a>
<a id="tocsauthset"></a>

```json
{
  "id": "string",
  "pubkey": "string",
  "identity_data": {
    "application/json": {
      "mac": "00:01:02:03:04:05",
      "sku": "My Device 1",
      "sn": "SN1234567890"
    }
  },
  "status": "pending",
  "ts": "string"
}

```

Authentication data set

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|Authentication data set ID.|
|pubkey|string|false|none|The device's public key, generated by the device or pre-provisioned by the vendor.|
|identity_data|[IdentityData](#schemaidentitydata)|false|none|Device identity attributes, in the form of a JSON structure.<br><br>The attributes are completely vendor-specific, the provided ones are just an example.<br>In reference implementation structure contains vendor-selected fields,<br>such as MACs, serial numbers, etc.|
|status|string|false|none|none|
|ts|string(datetime)|false|none|Created timestamp|

#### Enumerated Values

|Property|Value|
|---|---|
|status|pending|
|status|accepted|
|status|rejected|
|status|preauthorized|

<h2 id="tocS_Count">Count</h2>
<!-- backwards compatibility -->
<a id="schemacount"></a>
<a id="schema_Count"></a>
<a id="tocScount"></a>
<a id="tocscount"></a>

```json
{
  "count": "42"
}

```

Counter type

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|count|integer|false|none|The count of requested items.|

<h2 id="tocS_Error">Error</h2>
<!-- backwards compatibility -->
<a id="schemaerror"></a>
<a id="schema_Error"></a>
<a id="tocSerror"></a>
<a id="tocserror"></a>

```json
{
  "error": "string"
}

```

Error descriptor

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|error|string|false|none|Description of the error|

<h2 id="tocS_PreAuthSet">PreAuthSet</h2>
<!-- backwards compatibility -->
<a id="schemapreauthset"></a>
<a id="schema_PreAuthSet"></a>
<a id="tocSpreauthset"></a>
<a id="tocspreauthset"></a>

```json
{
  "application/json": {
    "identity_data": {
      "mac": "00:01:02:03:04:05",
      "sku": "My Device 1",
      "sn": "SN1234567890"
    },
    "pubkey": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzogVU7RGDilbsoUt/DdH\nVJvcepl0A5+xzGQ50cq1VE/Dyyy8Zp0jzRXCnnu9nu395mAFSZGotZVr+sWEpO3c\nyC3VmXdBZmXmQdZqbdD/GuixJOYfqta2ytbIUPRXFN7/I7sgzxnXWBYXYmObYvdP\nokP0mQanY+WKxp7Q16pt1RoqoAd0kmV39g13rFl35muSHbSBoAW3GBF3gO+mF5Ty\n1ddp/XcgLOsmvNNjY+2HOD5F/RX0fs07mWnbD7x+xz7KEKjF+H7ZpkqCwmwCXaf0\niyYyh1852rti3Afw4mDxuVSD7sd9ggvYMc0QHIpQNkD4YWOhNiE1AB0zH57VbUYG\nUwIDAQAB\n-----END PUBLIC KEY-----\n"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|identity_data|[IdentityData](#schemaidentitydata)|true|none|Device identity attributes, in the form of a JSON structure.<br><br>The attributes are completely vendor-specific, the provided ones are just an example.<br>In reference implementation structure contains vendor-selected fields,<br>such as MACs, serial numbers, etc.|
|pubkey|string|true|none|The device's public key, generated by the device or pre-provisioned by the vendor.|

<h2 id="tocS_IdentityData">IdentityData</h2>
<!-- backwards compatibility -->
<a id="schemaidentitydata"></a>
<a id="schema_IdentityData"></a>
<a id="tocSidentitydata"></a>
<a id="tocsidentitydata"></a>

```json
{
  "application/json": {
    "mac": "00:01:02:03:04:05",
    "sku": "My Device 1",
    "sn": "SN1234567890"
  }
}

```

Device identity attributes, in the form of a JSON structure.

The attributes are completely vendor-specific, the provided ones are just an example.
In reference implementation structure contains vendor-selected fields,
such as MACs, serial numbers, etc.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|mac|string|false|none|MAC address.|
|sku|string|false|none|Stock keeping unit.|
|sn|string|false|none|Serial number.|

