### Authentication

**Request Type : POST**
`/auth`

**Request Payload Type** {JSON}

* "username" : "user_name"
* "password" : "password"

Response Type

```
{
    "jsonrpc": "2.0",
    "signature": "rsa_sha256_pss:........",
    "detail": {
        "message": "some message",
        "threadid": 123123123
    },
    "versionnumber": "1.0.0",
    "version": "Kryptoblocks",
    "result": {
        "status": true,
        "value": {
            "dialog_no_token": false,........
           
            "token_wizard": false,
            "token": "generated_token",
            "show_seed": false,
            "policy_template_url": "https://raw.githubusercontent.com/privacyidea/policy-templates/master/templates/"
        }
    },
    "time": 1574624980.079785,
    "id": 1
}

```


### Token Init

**Request Type : POST**
`/token/init`

[Note] Token generated from Auth need to passed in 

**Header** (Required)
`
{
    PI-Authorization: < token_generated_after_auth >
}

`

**Request Payload Type** {JSON}

* "timeStep":30,
* "otplen":6,
* "otpkey":"123456",
* "genkey":1,
* "type":"email",
* "hashlib":"sha1",
* "radius.system_settings":true,
* "2stepinit":0,
* "email":"useremail@gmail.com",
* "phone":"9090909090",
* "pin":"123456",
* "user":"user_name",
* "realm":"user_realm"

**Response Type**

`
{
    "jsonrpc": "2.0",
    "signature": "rsa_sha256_pss:..........",
    "detail": {
        "oathurl": {
            "value": "oathtoken:///addToken?name=..............&lockdown=true&key=............",
            "description": "URL for OATH token",
            .
            .
            .
        },
        "googleurl": {
            "value": "otpauth://email/............?secret=...............&digits=6&issuer=privacyIDEA",
            "description": "URL for google Authenticator",
            "img": ""
            .
            .
            .
        },
        "rollout_state": "",
        "threadid": 140018026297152,
        "serial": "PIEM0000E725",
        "otpkey": {
            "value": "seed://c47afc5128eaca3f02bf0aa75a641d0ff7bd3f6a",
            .
            .
            .
        }
    },
    "versionnumber": "1.0.0",
    "version": "Kryptoblocks",
    "result": {
        "status": true,
        "value": true
    },
    "time": 1574625010.912343,
    "id": 1
}

`

### Request OTP

*will be updated soon...*

### OTP Validate

*will be updated soon...*