<!-- Generator: Widdershins v3.6.6 -->

<h1 id="deployments">Deployments v1</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

An API for deployments and artifacts management.
Intended for use by the web GUI.

Base URLs:

* <a href="https://docker.mender.io/api/management/v1/deployments">https://docker.mender.io/api/management/v1/deployments</a>


## Find all deployments

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/deployments \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/deployments HTTP/1.1
Host: docker.mender.io
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/deployments',
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
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/deployments',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://docker.mender.io/api/management/v1/deployments/deployments', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => 'application/json',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/deployments', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/deployments");
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
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/deployments", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /deployments`

Returns a filtered collection of deployments in the system,
including active and historical. If both 'status' and 'query' are
not specified, all devices are listed.

<h3 id="find-all-deployments-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|status|query|string|false|Deployment status filter.|
|search|query|string|false|Deployment name or description filter.|
|page|query|number(integer)|false|Results page number|
|per_page|query|number(integer)|false|Number of results per page|
|created_before|query|number(integer)|false|List only deployments created before and equal to Unix timestamp (UTC)|
|created_after|query|number(integer)|false|List only deployments created after and equal to Unix timestamp (UTC)|

#### Enumerated Values

|Parameter|Value|
|---|---|
|status|inprogress|
|status|finished|
|status|pending|

> Example responses

> Successful response.

```json
[
  {
    "created": "2016-02-11T13:03:17.063493443Z",
    "status": "finished",
    "name": "production",
    "artifact_name": "Application 0.0.1",
    "id": "00a0c91e6-7dec-11d0-a765-f81d4faebf6",
    "finished": "2016-03-11T13:03:17.063493443Z",
    "device_count": 10
  }
]
```

> 400 Response

<h3 id="find-all-deployments-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid Request.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<h3 id="find-all-deployments-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Deployment](#schemadeployment)]|false|none|none|
|» created|string(date-time)|true|none|none|
|» name|string|true|none|none|
|» artifact_name|string|true|none|none|
|» id|string|true|none|none|
|» finished|string(date-time)|false|none|none|
|» status|string|true|none|none|
|» device_count|integer|true|none|none|
|» artifacts|[string]|false|none|none|
|» phases|[[DeploymentPhase](#schemadeploymentphase)]|false|none|none|
|»» id|string|false|none|Phase identifier.|
|»» batch_size|integer|false|none|Percentage of devices to update in the phase.|
|»» start_ts|string(date-time)|false|none|Start date of a phase.<br>May be undefined for the first phase of a deployment.|
|»» device_count|integer|false|none|Number of devices which already requested an update within this phase.|

#### Enumerated Values

|Property|Value|
|---|---|
|status|inprogress|
|status|pending|
|status|finished|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Link|string||Standard header, we support 'first', 'next', and 'prev'.|

<aside class="success">
This operation does not require authentication
</aside>

## Create a deployment

> Code samples

```shell
# You can also use wget
curl -X POST https://docker.mender.io/api/management/v1/deployments/deployments \
  -H 'Content-Type: application/json' \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
POST https://docker.mender.io/api/management/v1/deployments/deployments HTTP/1.1
Host: docker.mender.io
Content-Type: application/json
Accept: */*
Authorization: string

```

```javascript
const inputBody = '{
  "application/json": [
    {
      "name": "production",
      "artifact_name": "Application 0.0.1",
      "devices": [
        "00a0c91e6-7dec-11d0-a765-f81d4faebf6"
      ],
      "phases": [
        {
          "batch_size": 5,
          "start_ts": "2019-07-07T21:16:17.063+0000"
        },
        {
          "batch_size": 15,
          "start_ts": "2019-09-07T21:16:17.063+0000"
        },
        {
          "start_ts": "2019-11-07T21:16:17.063+0000"
        }
      ]
    }
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/deployments',
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

result = RestClient.post 'https://docker.mender.io/api/management/v1/deployments/deployments',
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

r = requests.post('https://docker.mender.io/api/management/v1/deployments/deployments', headers = headers)

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
    $response = $client->request('POST','https://docker.mender.io/api/management/v1/deployments/deployments', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/deployments");
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
    req, err := http.NewRequest("POST", "https://docker.mender.io/api/management/v1/deployments/deployments", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /deployments`

Deploy software to specified devices. Artifact is auto assigned to the
device from all available artifacts based on artifact name and device type.
Devices for which there are no compatible artifacts to be installed are
considered finished successfully as well as receive status of `noartifact`.
If there is no artifacts for the deployment, deployment will not be created
and the 422 Unprocessable Entity status code will be returned.

> Body parameter

```json
{
  "application/json": [
    {
      "name": "production",
      "artifact_name": "Application 0.0.1",
      "devices": [
        "00a0c91e6-7dec-11d0-a765-f81d4faebf6"
      ],
      "phases": [
        {
          "batch_size": 5,
          "start_ts": "2019-07-07T21:16:17.063+0000"
        },
        {
          "batch_size": 15,
          "start_ts": "2019-09-07T21:16:17.063+0000"
        },
        {
          "start_ts": "2019-11-07T21:16:17.063+0000"
        }
      ]
    }
  ]
}
```

<h3 id="create-a-deployment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|body|body|[NewDeployment](#schemanewdeployment)|true|New deployment that needs to be created.|

> Example responses

> 400 Response

<h3 id="create-a-deployment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|New deployment created.|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid Request.|[Error](#schemaerror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Unprocessable Entity.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|string||URL of the newly created deployment.|

<aside class="success">
This operation does not require authentication
</aside>

## Get the details of a selected deployment

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/deployments/{id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/deployments/{id} HTTP/1.1
Host: docker.mender.io
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/deployments/{id}',
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
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/deployments/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://docker.mender.io/api/management/v1/deployments/deployments/{id}', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => 'application/json',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/deployments/{id}', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/deployments/{id}");
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
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/deployments/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /deployments/{id}`

Returns the details of a particular deployment.

<h3 id="get-the-details-of-a-selected-deployment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Deployment identifier.|

> Example responses

> Successful response.

```json
{
  "created": "2016-02-11T13:03:17.063493443Z",
  "name": "production",
  "artifact_name": "Application 0.0.1",
  "id": "00a0c91e6-7dec-11d0-a765-f81d4faebf6",
  "finished": "2016-03-11T13:03:17.063493443Z"
}
```

> 404 Response

<h3 id="get-the-details-of-a-selected-deployment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful response.|[Deployment](#schemadeployment)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Abort the deployment

> Code samples

```shell
# You can also use wget
curl -X PUT https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/status \
  -H 'Content-Type: application/json' \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
PUT https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/status HTTP/1.1
Host: docker.mender.io
Content-Type: application/json
Accept: */*
Authorization: string

```

```javascript
const inputBody = '{
  "status": "aborted"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/status',
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

result = RestClient.put 'https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/status',
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

r = requests.put('https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/status', headers = headers)

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
    $response = $client->request('PUT','https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/status', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/status");
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
    req, err := http.NewRequest("PUT", "https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/status", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`PUT /deployments/{deployment_id}/status`

Aborts the deployment that is pending or in progress. For devices included in this deployment it means that:
- Devices that have completed the deployment (i.e. reported final status) are not affected by the abort, and their original status is kept in the deployment report.
- Devices that do not yet know about the deployment at time of abort will not start the deployment.
- Devices that are in the middle of the deployment at time of abort will finish its deployment normally, but they will not be able to change its deployment status so they will perform rollback.

> Body parameter

```json
{
  "status": "aborted"
}
```

<h3 id="abort-the-deployment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|deployment_id|path|string|true|Deployment identifier.|
|body|body|object|true|Deployment status.|
|» status|body|string|true|none|

#### Enumerated Values

|Parameter|Value|
|---|---|
|» status|aborted|

> Example responses

> 400 Response

<h3 id="abort-the-deployment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|Status updated successfully.|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid Request.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found.|[Error](#schemaerror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Unprocessable Entity.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Get the statistics of a selected deployment

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/statistics \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/statistics HTTP/1.1
Host: docker.mender.io
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/statistics',
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
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/statistics',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/statistics', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => 'application/json',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/statistics', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/statistics");
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
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/statistics", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /deployments/{deployment_id}/statistics`

Returns the statistics of a selected deployment statuses.

<h3 id="get-the-statistics-of-a-selected-deployment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|deployment_id|path|string|true|Deployment identifier|

> Example responses

> OK

```json
{
  "success": 3,
  "pending": 1,
  "failure": 0,
  "downloading": 1,
  "installing": 2,
  "rebooting": 3,
  "noartifact": 0,
  "already-installed": 0,
  "aborted": 0
}
```

> 404 Response

<h3 id="get-the-statistics-of-a-selected-deployment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[DeploymentStatistics](#schemadeploymentstatistics)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## List devices of a deployment

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices HTTP/1.1
Host: docker.mender.io
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices',
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
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => 'application/json',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices");
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
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /deployments/{deployment_id}/devices`

Returns a collection of a selected deployment's status for each assigned device.

<h3 id="list-devices-of-a-deployment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|deployment_id|path|string|true|Deployment identifier.|

> Example responses

> OK

```json
[
  {
    "id": "00a0c91e6-7dec-11d0-a765-f81d4faebf6",
    "finished": "2016-03-11T13:03:17.063493443Z",
    "status": "pending",
    "created": "2016-02-11T13:03:17.063493443Z",
    "device_type": "Raspberry Pi 3"
  }
]
```

> 404 Response

<h3 id="list-devices-of-a-deployment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<h3 id="list-devices-of-a-deployment-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Device](#schemadevice)]|false|none|none|
|» id|string|true|none|Device identifier.|
|» finished|string(date-time)|false|none|none|
|» status|string|true|none|none|
|» created|string(date-time)|false|none|none|
|» device_type|string|false|none|none|
|» log|boolean|true|none|Availability of the device's deployment log.|
|» state|string|false|none|State reported by device|
|» substate|string|false|none|Additional state information|

#### Enumerated Values

|Property|Value|
|---|---|
|status|downloading|
|status|installing|
|status|rebooting|
|status|pending|
|status|success|
|status|failure|
|status|noartifact|
|status|already-installed|
|status|aborted|
|status|decommissioned|

<aside class="success">
This operation does not require authentication
</aside>

## Get the log of a selected device's deployment

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices/{device_id}/log \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices/{device_id}/log HTTP/1.1
Host: docker.mender.io
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices/{device_id}/log',
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

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices/{device_id}/log',
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

r = requests.get('https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices/{device_id}/log', headers = headers)

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
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices/{device_id}/log', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices/{device_id}/log");
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
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/deployments/{deployment_id}/devices/{device_id}/log", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /deployments/{deployment_id}/devices/{device_id}/log`

Returns the log of a selected device, collected during a particular deployment.

<h3 id="get-the-log-of-a-selected-device's-deployment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|deployment_id|path|string|true|Deployment identifier.|
|device_id|path|string|true|Device identifier.|

> Example responses

> 404 Response

<h3 id="get-the-log-of-a-selected-device's-deployment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful response.|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Remove device from all deployments

> Code samples

```shell
# You can also use wget
curl -X DELETE https://docker.mender.io/api/management/v1/deployments/deployments/devices/{id} \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
DELETE https://docker.mender.io/api/management/v1/deployments/deployments/devices/{id} HTTP/1.1
Host: docker.mender.io
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/deployments/devices/{id}',
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

result = RestClient.delete 'https://docker.mender.io/api/management/v1/deployments/deployments/devices/{id}',
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

r = requests.delete('https://docker.mender.io/api/management/v1/deployments/deployments/devices/{id}', headers = headers)

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
    $response = $client->request('DELETE','https://docker.mender.io/api/management/v1/deployments/deployments/devices/{id}', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/deployments/devices/{id}");
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
    req, err := http.NewRequest("DELETE", "https://docker.mender.io/api/management/v1/deployments/deployments/devices/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /deployments/devices/{id}`

Set 'decommissioned' status to all pending device deployments for a given device

<h3 id="remove-device-from-all-deployments-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|string|true|System wide device identifier|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|

> Example responses

> 500 Response

<h3 id="remove-device-from-all-deployments-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|Device was removed|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal server error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## List releases

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/deployments/releases \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/deployments/releases HTTP/1.1
Host: docker.mender.io
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/deployments/releases',
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
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/deployments/releases',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://docker.mender.io/api/management/v1/deployments/deployments/releases', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => 'application/json',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/deployments/releases', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/deployments/releases");
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
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/deployments/releases", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /deployments/releases`

Returns a collection of releases, allows filtering by release name.

<h3 id="list-releases-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|name|query|string|false|Release name filter.|

> Example responses

> Successful response.

```json
[
  {
    "name": "my-app-v1.0.1",
    "artifacts": [
      {
        "name": "my-app-v1.0.1",
        "description": "Application v1.0.1",
        "device_types_compatible": [
          "Beagle Bone"
        ],
        "id": "0c13a0e6-6b63-475d-8260-ee42a590e8ff",
        "signed": false,
        "modified": "2016-03-11T13:03:17.063493443Z",
        "info": {
          "type_info": {
            "type": "rootfs"
          }
        },
        "files": [
          {
            "name": "rootfs-image-1",
            "checksum": "cc436f982bc60a8255fe1926a450db5f195a19ad",
            "size": 23421351,
            "date": "2016-03-11T13:03:17.063+0000"
          }
        ],
        "metadata": {}
      },
      {
        "name": "my-app-v1.0.1",
        "description": "Application v1.0.1",
        "device_types_compatible": [
          "Raspberry Pi"
        ],
        "id": "0c13a0e6-6b63-475d-8260-ee42a590e8ff",
        "signed": false,
        "modified": "2016-03-11T13:03:17.063493443Z",
        "info": {
          "type_info": {
            "type": "rootfs"
          }
        },
        "files": [
          {
            "name": "rootfs-image-1",
            "checksum": "cc436f982bc60a8255fe1926a450db5f195a19ad",
            "size": 23421351,
            "date": "2016-03-11T13:03:17.063+0000"
          }
        ],
        "metadata": {}
      }
    ]
  },
  {
    "name": "my-app-v2.0.0",
    "artifacts": [
      {
        "name": "my-app-v2.0.0",
        "description": "Application v2.0.0",
        "device_types_compatible": [
          "Beagle Bone"
        ],
        "id": "0c13a0e6-6b63-475d-8260-ee42a590e8ff",
        "signed": false,
        "modified": "2016-03-11T13:03:17.063493443Z",
        "info": {
          "type_info": {
            "type": "rootfs"
          }
        },
        "files": [
          {
            "name": "rootfs-image-1",
            "checksum": "cc436f982bc60a8255fe1926a450db5f195a19ad",
            "size": 23421351,
            "date": "2016-03-11T13:03:17.063+0000"
          }
        ],
        "metadata": {}
      }
    ]
  }
]
```

> 500 Response

<h3 id="list-releases-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful response.|Inline|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<h3 id="list-releases-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Release](#schemarelease)]|false|none|[Groups artifacts with the same release name into a single resource.]|
|» name|string|false|none|release name.|
|» artifacts|[[Artifact](#schemaartifact)]|false|none|list of artifacts for this release.|
|»» name|string|true|none|none|
|»» description|string|true|none|none|
|»» device_types_compatible|[string]|true|none|none|
|»» id|string|true|none|none|
|»» signed|boolean|false|none|Idicates if artifact is signed or not.|
|»» modified|string(date-time)|true|none|Represents creation / last edition of any of the artifact properties.|
|»» size|number(integer)|false|none|Artifact total size in bytes - the size of the actual file that will be transferred to the device (compressed).|
|»» info|[ArtifactInfo](#schemaartifactinfo)|false|none|Information about artifact format and version.|
|»»» format|string|false|none|none|
|»»» version|integer|false|none|none|
|»» updates|[[Update](#schemaupdate)]|false|none|[Single updated to be applied.<br>]|
|»»» type_info|[ArtifactTypeInfo](#schemaartifacttypeinfo)|false|none|Information about update type.|
|»»»» type|string|false|none|none|
|»»» files|[[UpdateFile](#schemaupdatefile)]|false|none|[Information about particular update file.<br>]|
|»»»» name|string|false|none|none|
|»»»» checksum|string|false|none|none|
|»»»» size|integer|false|none|none|
|»»»» date|string(date-time)|false|none|none|
|»»» meta_data|object|false|none|meta_data is an object of unknown structure as this is dependent of update type (also custom defined by user)|

<aside class="success">
This operation does not require authentication
</aside>

## List known artifacts

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/artifacts \
  -H 'Accept: application/json'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/artifacts HTTP/1.1
Host: docker.mender.io
Accept: application/json

```

```javascript

const headers = {
  'Accept':'application/json'

};

fetch('https://docker.mender.io/api/management/v1/deployments/artifacts',
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
  'Accept' => 'application/json'
}

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/artifacts',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://docker.mender.io/api/management/v1/deployments/artifacts', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => 'application/json',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/artifacts', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/artifacts");
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
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/artifacts", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /artifacts`

Returns a collection of all artifacts.

> Example responses

> OK

```json
[
  {
    "name": "Application 1.0.0",
    "description": "Johns Monday test build",
    "device_types_compatible": [
      "Beagle Bone"
    ],
    "id": "0c13a0e6-6b63-475d-8260-ee42a590e8ff",
    "signed": false,
    "modified": "2016-03-11T13:03:17.063493443Z",
    "info": {
      "type_info": {
        "type": "rootfs"
      }
    },
    "files": [
      {
        "name": "rootfs-image-1",
        "checksum": "cc436f982bc60a8255fe1926a450db5f195a19ad",
        "size": 123,
        "date": "2016-03-11T13:03:17.063+0000"
      }
    ],
    "metadata": {}
  }
]
```

> 500 Response

<h3 id="list-known-artifacts-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<h3 id="list-known-artifacts-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Artifact](#schemaartifact)]|false|none|[Detailed artifact.]|
|» name|string|true|none|none|
|» description|string|true|none|none|
|» device_types_compatible|[string]|true|none|none|
|» id|string|true|none|none|
|» signed|boolean|false|none|Idicates if artifact is signed or not.|
|» modified|string(date-time)|true|none|Represents creation / last edition of any of the artifact properties.|
|» size|number(integer)|false|none|Artifact total size in bytes - the size of the actual file that will be transferred to the device (compressed).|
|» info|[ArtifactInfo](#schemaartifactinfo)|false|none|Information about artifact format and version.|
|»» format|string|false|none|none|
|»» version|integer|false|none|none|
|» updates|[[Update](#schemaupdate)]|false|none|[Single updated to be applied.<br>]|
|»» type_info|[ArtifactTypeInfo](#schemaartifacttypeinfo)|false|none|Information about update type.|
|»»» type|string|false|none|none|
|»» files|[[UpdateFile](#schemaupdatefile)]|false|none|[Information about particular update file.<br>]|
|»»» name|string|false|none|none|
|»»» checksum|string|false|none|none|
|»»» size|integer|false|none|none|
|»»» date|string(date-time)|false|none|none|
|»» meta_data|object|false|none|meta_data is an object of unknown structure as this is dependent of update type (also custom defined by user)|

<aside class="success">
This operation does not require authentication
</aside>

## Upload mender artifact

> Code samples

```shell
# You can also use wget
curl -X POST https://docker.mender.io/api/management/v1/deployments/artifacts \
  -H 'Content-Type: multipart/form-data' \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
POST https://docker.mender.io/api/management/v1/deployments/artifacts HTTP/1.1
Host: docker.mender.io
Content-Type: multipart/form-data
Accept: */*
Authorization: string

```

```javascript
const inputBody = '{
  "size": 0,
  "description": "string",
  "artifact": "string"
}';
const headers = {
  'Content-Type':'multipart/form-data',
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/artifacts',
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
  'Content-Type' => 'multipart/form-data',
  'Accept' => '*/*',
  'Authorization' => 'string'
}

result = RestClient.post 'https://docker.mender.io/api/management/v1/deployments/artifacts',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'multipart/form-data',
  'Accept': '*/*',
  'Authorization': 'string'
}

r = requests.post('https://docker.mender.io/api/management/v1/deployments/artifacts', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'multipart/form-data',
    'Accept' => '*/*',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('POST','https://docker.mender.io/api/management/v1/deployments/artifacts', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/artifacts");
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
        "Content-Type": []string{"multipart/form-data"},
        "Accept": []string{"*/*"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://docker.mender.io/api/management/v1/deployments/artifacts", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /artifacts`

Upload mender artifact. Multipart request with meta and artifact.

Supports artifact (versions v1, v2)[https://docs.mender.io/development/architecture/mender-artifacts#versions].

> Body parameter

```yaml
size: 0
description: string
artifact: string

```

<h3 id="upload-mender-artifact-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|body|body|object|false|none|
|» size|body|integer(long)|true|Size of the artifact file in bytes.|
|» description|body|string|false|none|
|» artifact|body|string(binary)|true|Artifact. It has to be the last part of request.|

> Example responses

> 400 Response

<h3 id="upload-mender-artifact-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Artifact uploaded.|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid Request.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|201|Location|string||URL of the newly uploaded artifact.|

<aside class="success">
This operation does not require authentication
</aside>

## Get the details of a selected artifact

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/artifacts/{id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/artifacts/{id} HTTP/1.1
Host: docker.mender.io
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/artifacts/{id}',
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
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/artifacts/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://docker.mender.io/api/management/v1/deployments/artifacts/{id}', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => 'application/json',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/artifacts/{id}', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/artifacts/{id}");
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
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/artifacts/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /artifacts/{id}`

Returns the details of a selected artifact.

<h3 id="get-the-details-of-a-selected-artifact-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Artifact identifier.|

> Example responses

> Successful response.

```json
{
  "name": "Application 1.0.0",
  "description": "Johns Monday test build",
  "device_types_compatible": [
    "Beagle Bone"
  ],
  "id": "0c13a0e6-6b63-475d-8260-ee42a590e8ff",
  "signed": false,
  "modified": "2016-03-11T13:03:17.063493443Z",
  "info": {
    "type_info": {
      "type": "rootfs"
    }
  },
  "files": [
    {
      "name": "rootfs-image-1",
      "checksum": "cc436f982bc60a8255fe1926a450db5f195a19ad",
      "size": 123,
      "date": "2016-03-11T13:03:17.063+0000"
    }
  ],
  "metadata": {}
}
```

> 400 Response

<h3 id="get-the-details-of-a-selected-artifact-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful response.|[Artifact](#schemaartifact)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid Request.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update description of a selected artifact

> Code samples

```shell
# You can also use wget
curl -X PUT https://docker.mender.io/api/management/v1/deployments/artifacts/{id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
PUT https://docker.mender.io/api/management/v1/deployments/artifacts/{id} HTTP/1.1
Host: docker.mender.io
Content-Type: application/json
Accept: */*
Authorization: string

```

```javascript
const inputBody = '{
  "description": "Some description"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/artifacts/{id}',
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

result = RestClient.put 'https://docker.mender.io/api/management/v1/deployments/artifacts/{id}',
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

r = requests.put('https://docker.mender.io/api/management/v1/deployments/artifacts/{id}', headers = headers)

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
    $response = $client->request('PUT','https://docker.mender.io/api/management/v1/deployments/artifacts/{id}', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/artifacts/{id}");
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
    req, err := http.NewRequest("PUT", "https://docker.mender.io/api/management/v1/deployments/artifacts/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`PUT /artifacts/{id}`

Edit description. Artifact is not allowed to be edited if it was used
in any deployment.

> Body parameter

```json
{
  "description": "Some description"
}
```

<h3 id="update-description-of-a-selected-artifact-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Artifact identifier.|
|body|body|[ArtifactUpdate](#schemaartifactupdate)|false|none|

> Example responses

> 400 Response

<h3 id="update-description-of-a-selected-artifact-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|The artifact metadata updated successfully.|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid Request.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found.|[Error](#schemaerror)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Unprocessable Entity.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete the artifact

> Code samples

```shell
# You can also use wget
curl -X DELETE https://docker.mender.io/api/management/v1/deployments/artifacts/{id} \
  -H 'Accept: */*' \
  -H 'Authorization: string'

```

```http
DELETE https://docker.mender.io/api/management/v1/deployments/artifacts/{id} HTTP/1.1
Host: docker.mender.io
Accept: */*
Authorization: string

```

```javascript

const headers = {
  'Accept':'*/*',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/artifacts/{id}',
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

result = RestClient.delete 'https://docker.mender.io/api/management/v1/deployments/artifacts/{id}',
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

r = requests.delete('https://docker.mender.io/api/management/v1/deployments/artifacts/{id}', headers = headers)

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
    $response = $client->request('DELETE','https://docker.mender.io/api/management/v1/deployments/artifacts/{id}', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/artifacts/{id}");
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
    req, err := http.NewRequest("DELETE", "https://docker.mender.io/api/management/v1/deployments/artifacts/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /artifacts/{id}`

Deletes the artifact from file and artifacts storage.
Artifacts used by deployments in progress can not be deleted
until deployment finishes.

<h3 id="delete-the-artifact-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Artifact identifier.|

> Example responses

> 404 Response

> 409 Response

```json
{
  "application/json": {
    "error": "failed to decode device group data: JSON payload is empty",
    "request_id": "f7881e82-0492-49fb-b459-795654e7188a"
  }
}
```

<h3 id="delete-the-artifact-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|The artifact deleted successfully.|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found.|[Error](#schemaerror)|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|Artifact used by active deployment.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Get the download link of a selected artifact

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/artifacts/{id}/download \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/artifacts/{id}/download HTTP/1.1
Host: docker.mender.io
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/artifacts/{id}/download',
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
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/artifacts/{id}/download',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://docker.mender.io/api/management/v1/deployments/artifacts/{id}/download', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => 'application/json',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/artifacts/{id}/download', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/artifacts/{id}/download");
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
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/artifacts/{id}/download", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /artifacts/{id}/download`

Generates signed URL for downloading artifact file. URI can be used only
with GET HTTP method. Link supports such HTTP headers: 'Range',
'If-Modified-Since', 'If-Unmodified-Since' It is valid for specified
period of time.

<h3 id="get-the-download-link-of-a-selected-artifact-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|
|id|path|string|true|Artifact identifier.|

> Example responses

> 200 Response

```json
{
  "application/json": {
    "uri": "http://mender.io/artifact.tar.gz.mender",
    "expire": "2016-10-29T10:45:34Z"
  }
}
```

> 400 Response

<h3 id="get-the-download-link-of-a-selected-artifact-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful response.|[ArtifactLink](#schemaartifactlink)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid Request.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Get storage limit and current storage usage

> Code samples

```shell
# You can also use wget
curl -X GET https://docker.mender.io/api/management/v1/deployments/limits/storage \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://docker.mender.io/api/management/v1/deployments/limits/storage HTTP/1.1
Host: docker.mender.io
Accept: application/json
Authorization: string

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://docker.mender.io/api/management/v1/deployments/limits/storage',
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
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://docker.mender.io/api/management/v1/deployments/limits/storage',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://docker.mender.io/api/management/v1/deployments/limits/storage', headers = headers)

print r.json()

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Accept' => 'application/json',
    'Authorization' => 'string',
    
    );

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('GET','https://docker.mender.io/api/management/v1/deployments/limits/storage', array(
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
URL obj = new URL("https://docker.mender.io/api/management/v1/deployments/limits/storage");
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
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://docker.mender.io/api/management/v1/deployments/limits/storage", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /limits/storage`

Get storage limit and current storage usage for currently logged in user.
If the limit value is 0 it means there is no limit for storage for logged in user.

<h3 id="get-storage-limit-and-current-storage-usage-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authorization|header|string(Bearer [token])|true|Contains the JWT token issued by the User Administration and Authentication Service.|

> Example responses

> 200 Response

```json
{
  "application/json": {
    "limit": 1073741824,
    "usage": 536870912
  }
}
```

> 500 Response

<h3 id="get-storage-limit-and-current-storage-usage-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful response.|[StorageLimit](#schemastoragelimit)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error.|[Error](#schemaerror)|

<aside class="success">
This operation does not require authentication
</aside>

