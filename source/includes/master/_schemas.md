# Schemas

<h2 id="tocS_UserNew">UserNew</h2>
<!-- backwards compatibility -->
<a id="schemausernew"></a>
<a id="schema_UserNew"></a>
<a id="tocSusernew"></a>
<a id="tocsusernew"></a>

```json
{
  "application/json": {
    "email": "user@acme.com",
    "password": "mypass1234"
  }
}

```

New user descriptor.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|email|string|true|none|A unique email address. Invalid characters are non-ascii and '+'.|
|password|string|true|none|Password.|

<h2 id="tocS_UserUpdate">UserUpdate</h2>
<!-- backwards compatibility -->
<a id="schemauserupdate"></a>
<a id="schema_UserUpdate"></a>
<a id="tocSuserupdate"></a>
<a id="tocsuserupdate"></a>

```json
{
  "application/json": {
    "email": "new_email@acme.com"
  }
}

```

Update user information.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|email|string|false|none|A unique email address.|
|password|string|false|none|Password.|

<h2 id="tocS_User">User</h2>
<!-- backwards compatibility -->
<a id="schemauser"></a>
<a id="schema_User"></a>
<a id="tocSuser"></a>
<a id="tocsuser"></a>

```json
{
  "application/json": {
    "email": "user@acme.com",
    "id": "806603def19d417d004a4b67e",
    "created_ts": "2016-10-03T16:58:51.639Z",
    "updated_ts": "2016-10-04T11:33:66.611Z"
  }
}

```

User descriptor.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|email|string|true|none|A unique email address.|
|id|string|true|none|User Id.|
|created_ts|string(date-time)|false|none|Server-side timestamp of the user creation.|
|updated_ts|string(date-time)|false|none|Server-side timestamp of the last user information update.|

<h2 id="tocS_Error">Error</h2>
<!-- backwards compatibility -->
<a id="schemaerror"></a>
<a id="schema_Error"></a>
<a id="tocSerror"></a>
<a id="tocserror"></a>

```json
{
  "application/json": {
    "error": "missing Authorization header",
    "request_id": "f7881e82-0492-49fb-b459-795654e7188a"
  }
}

```

Error descriptor.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|error|string|false|none|Description of the error.|
|request_id|string|false|none|Request ID (same as in X-MEN-RequestID header).|

<h2 id="tocS_Settings">Settings</h2>
<!-- backwards compatibility -->
<a id="schemasettings"></a>
<a id="schema_Settings"></a>
<a id="tocSsettings"></a>
<a id="tocssettings"></a>

```json
{}

```

User settings.

### Properties

*None*

<h2 id="tocS_Twofactor">Twofactor</h2>
<!-- backwards compatibility -->
<a id="schematwofactor"></a>
<a id="schema_Twofactor"></a>
<a id="tocStwofactor"></a>
<a id="tocstwofactor"></a>

```json
{
  "application/json": {
    "token2fa": "012234"
  }
}

```

Two factor authentication token

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|token2fa|string|true|none|Two factor authentication token|




<h2 id="tocS_Error">Error</h2>
<!-- backwards compatibility -->
<a id="schemaerror"></a>
<a id="schema_Error"></a>
<a id="tocSerror"></a>
<a id="tocserror"></a>

```json
{
  "application/json": {
    "error": "failed to decode device group data: JSON payload is empty",
    "request_id": "f7881e82-0492-49fb-b459-795654e7188a"
  }
}

```

Error descriptor.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|error|string|false|none|Description of the error.|
|request_id|string|false|none|Request ID (same as in X-MEN-RequestID header).|

<h2 id="tocS_NewDeployment">NewDeployment</h2>
<!-- backwards compatibility -->
<a id="schemanewdeployment"></a>
<a id="schema_NewDeployment"></a>
<a id="tocSnewdeployment"></a>
<a id="tocsnewdeployment"></a>

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

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|none|
|artifact_name|string|true|none|none|
|devices|[string]|true|none|none|
|phases|[[NewDeploymentPhase](#schemanewdeploymentphase)]|false|none|none|

<h2 id="tocS_Deployment">Deployment</h2>
<!-- backwards compatibility -->
<a id="schemadeployment"></a>
<a id="schema_Deployment"></a>
<a id="tocSdeployment"></a>
<a id="tocsdeployment"></a>

```json
{
  "application/json": {
    "created": "2016-02-11T13:03:17.063493443Z",
    "status": "finished",
    "name": "production",
    "artifact_name": "Application 0.0.1",
    "id": "00a0c91e6-7dec-11d0-a765-f81d4faebf6",
    "finished": "2016-03-11T13:03:17.063493443Z",
    "phases": [
      {
        "batch_size": 5,
        "start_ts": "2019-07-07T21:16:17.063+0000",
        "device_count": 27
      },
      {
        "batch_size": 15,
        "start_ts": "2019-09-07T21:16:17.063+0000",
        "device_count": 0
      },
      {
        "start_ts": "2019-11-07T21:16:17.063+0000",
        "device_count": 0
      }
    ]
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|created|string(date-time)|true|none|none|
|name|string|true|none|none|
|artifact_name|string|true|none|none|
|id|string|true|none|none|
|finished|string(date-time)|false|none|none|
|status|string|true|none|none|
|device_count|integer|true|none|none|
|artifacts|[string]|false|none|none|
|phases|[[DeploymentPhase](#schemadeploymentphase)]|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|status|inprogress|
|status|pending|
|status|finished|

<h2 id="tocS_NewDeploymentPhase">NewDeploymentPhase</h2>
<!-- backwards compatibility -->
<a id="schemanewdeploymentphase"></a>
<a id="schema_NewDeploymentPhase"></a>
<a id="tocSnewdeploymentphase"></a>
<a id="tocsnewdeploymentphase"></a>

```json
{
  "application/json": {
    "start_ts": "2019-07-07T21:10:17.063493443Z",
    "batch_size": 5
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|batch_size|integer|false|none|Percentage of devices to update in the phase.<br>This field is optional for the last phase.<br>The last phase will contain the rest of the devices.<br>Note that if the percentage of devices entered does not<br>add up to a whole number of devices it is rounded down,<br>and in the case it is rounded down to zero, a 400 error<br>will be returned. This is mostly a concern when the deployment<br>consists of a low number of devices, like say 5 percent of 11<br>devices will round to zero, and an error is returned by the server.|
|start_ts|string(date-time)|false|none|Start date of a phase.<br>Can be skipped for the first phase of a new deployment definition ('start immediately').|

<h2 id="tocS_DeploymentPhase">DeploymentPhase</h2>
<!-- backwards compatibility -->
<a id="schemadeploymentphase"></a>
<a id="schema_DeploymentPhase"></a>
<a id="tocSdeploymentphase"></a>
<a id="tocsdeploymentphase"></a>

```json
{
  "application/json": {
    "id": "foo",
    "start_ts": "2019-07-07T21:10:17.063493443Z",
    "batch_size": 5,
    "device_count": 42
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|Phase identifier.|
|batch_size|integer|false|none|Percentage of devices to update in the phase.|
|start_ts|string(date-time)|false|none|Start date of a phase.<br>May be undefined for the first phase of a deployment.|
|device_count|integer|false|none|Number of devices which already requested an update within this phase.|

<h2 id="tocS_DeploymentStatistics">DeploymentStatistics</h2>
<!-- backwards compatibility -->
<a id="schemadeploymentstatistics"></a>
<a id="schema_DeploymentStatistics"></a>
<a id="tocSdeploymentstatistics"></a>
<a id="tocsdeploymentstatistics"></a>

```json
{
  "application/json": {
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
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|success|integer|true|none|Number of successful deployments.|
|pending|integer|true|none|Number of pending deployments.|
|downloading|integer|true|none|Number of deployments being downloaded.|
|rebooting|integer|true|none|Number of deployments devices are rebooting into.|
|installing|integer|true|none|Number of deployments devices being installed.|
|failure|integer|true|none|Number of failed deployments.|
|noartifact|integer|true|none|Do not have appropriate artifact for device type.|
|already-installed|integer|true|none|Number of devices unaffected by upgrade, since they are already running the specified software version.|
|aborted|integer|true|none|Number of deployments aborted by user.|

<h2 id="tocS_Device">Device</h2>
<!-- backwards compatibility -->
<a id="schemadevice"></a>
<a id="schema_Device"></a>
<a id="tocSdevice"></a>
<a id="tocsdevice"></a>

```json
{
  "application/json": [
    {
      "id": "00a0c91e6-7dec-11d0-a765-f81d4faebf6",
      "finished": "2016-03-11T13:03:17.063493443Z",
      "status": "inprogress",
      "created": "2016-02-11T13:03:17.063493443Z",
      "device_type": "Raspberry Pi 3",
      "log": false,
      "state": "installing",
      "substate": "installing.enter;script:foo-bar"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|true|none|Device identifier.|
|finished|string(date-time)|false|none|none|
|status|string|true|none|none|
|created|string(date-time)|false|none|none|
|device_type|string|false|none|none|
|log|boolean|true|none|Availability of the device's deployment log.|
|state|string|false|none|State reported by device|
|substate|string|false|none|Additional state information|

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

<h2 id="tocS_ArtifactUpdate">ArtifactUpdate</h2>
<!-- backwards compatibility -->
<a id="schemaartifactupdate"></a>
<a id="schema_ArtifactUpdate"></a>
<a id="tocSartifactupdate"></a>
<a id="tocsartifactupdate"></a>

```json
{
  "description": "Some description"
}

```

Artifact information update.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|description|string|false|none|none|

<h2 id="tocS_ArtifactTypeInfo">ArtifactTypeInfo</h2>
<!-- backwards compatibility -->
<a id="schemaartifacttypeinfo"></a>
<a id="schema_ArtifactTypeInfo"></a>
<a id="tocSartifacttypeinfo"></a>
<a id="tocsartifacttypeinfo"></a>

```json
{
  "type": "string"
}

```

Information about update type.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|false|none|none|

<h2 id="tocS_UpdateFile">UpdateFile</h2>
<!-- backwards compatibility -->
<a id="schemaupdatefile"></a>
<a id="schema_UpdateFile"></a>
<a id="tocSupdatefile"></a>
<a id="tocsupdatefile"></a>

```json
{
  "name": "string",
  "checksum": "string",
  "size": 0,
  "date": "2019-11-04T14:16:07Z"
}

```

Information about particular update file.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|checksum|string|false|none|none|
|size|integer|false|none|none|
|date|string(date-time)|false|none|none|

<h2 id="tocS_Update">Update</h2>
<!-- backwards compatibility -->
<a id="schemaupdate"></a>
<a id="schema_Update"></a>
<a id="tocSupdate"></a>
<a id="tocsupdate"></a>

```json
{
  "type_info": {
    "type": "string"
  },
  "files": [
    {
      "name": "string",
      "checksum": "string",
      "size": 0,
      "date": "2019-11-04T14:16:07Z"
    }
  ],
  "meta_data": {}
}

```

Single updated to be applied.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type_info|[ArtifactTypeInfo](#schemaartifacttypeinfo)|false|none|Information about update type.|
|files|[[UpdateFile](#schemaupdatefile)]|false|none|[Information about particular update file.<br>]|
|meta_data|object|false|none|meta_data is an object of unknown structure as this is dependent of update type (also custom defined by user)|

<h2 id="tocS_ArtifactInfo">ArtifactInfo</h2>
<!-- backwards compatibility -->
<a id="schemaartifactinfo"></a>
<a id="schema_ArtifactInfo"></a>
<a id="tocSartifactinfo"></a>
<a id="tocsartifactinfo"></a>

```json
{
  "format": "string",
  "version": 0
}

```

Information about artifact format and version.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|format|string|false|none|none|
|version|integer|false|none|none|

<h2 id="tocS_Artifact">Artifact</h2>
<!-- backwards compatibility -->
<a id="schemaartifact"></a>
<a id="schema_Artifact"></a>
<a id="tocSartifact"></a>
<a id="tocsartifact"></a>

```json
{
  "application/json": {
    "name": "Application 1.0.0",
    "size": 36891648,
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
}

```

Detailed artifact.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|none|
|description|string|true|none|none|
|device_types_compatible|[string]|true|none|none|
|id|string|true|none|none|
|signed|boolean|false|none|Idicates if artifact is signed or not.|
|modified|string(date-time)|true|none|Represents creation / last edition of any of the artifact properties.|
|size|number(integer)|false|none|Artifact total size in bytes - the size of the actual file that will be transferred to the device (compressed).|
|info|[ArtifactInfo](#schemaartifactinfo)|false|none|Information about artifact format and version.|
|updates|[[Update](#schemaupdate)]|false|none|[Single updated to be applied.<br>]|

<h2 id="tocS_ArtifactLink">ArtifactLink</h2>
<!-- backwards compatibility -->
<a id="schemaartifactlink"></a>
<a id="schema_ArtifactLink"></a>
<a id="tocSartifactlink"></a>
<a id="tocsartifactlink"></a>

```json
{
  "application/json": {
    "uri": "http://mender.io/artifact.tar.gz.mender",
    "expire": "2016-10-29T10:45:34Z"
  }
}

```

URL for artifact file download.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|uri|string|true|none|none|
|expire|string(date-time)|true|none|none|

<h2 id="tocS_StorageLimit">StorageLimit</h2>
<!-- backwards compatibility -->
<a id="schemastoragelimit"></a>
<a id="schema_StorageLimit"></a>
<a id="tocSstoragelimit"></a>
<a id="tocsstoragelimit"></a>

```json
{
  "application/json": {
    "limit": 1073741824,
    "usage": 536870912
  }
}

```

Tenant account storage limit and storage usage.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|limit|integer|true|none|Storage limit in bytes. If set to 0 - there is no limit for storage.|
|usage|integer|true|none|Current storage usage in bytes.|

<h2 id="tocS_Release">Release</h2>
<!-- backwards compatibility -->
<a id="schemarelease"></a>
<a id="schema_Release"></a>
<a id="tocSrelease"></a>
<a id="tocsrelease"></a>

```json
{
  "application/json": {
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
  }
}

```

Groups artifacts with the same release name into a single resource.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|release name.|
|artifacts|[[Artifact](#schemaartifact)]|false|none|list of artifacts for this release.|


