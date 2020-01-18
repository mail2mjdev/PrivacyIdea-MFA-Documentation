# Questionnaire Token

Questionnaire Token in Privacy Idea MFA is an option where users will have an additional layer of security for authentication process. Here once the user enters a generic password, he/she will be asked a random question for which they have already saved the answers.

## Configuration

1. Login to your MFA instance with admin userid and password.
2. Create a SQL_RESOLVER under 'config' -> 'users' and map it properly with the col_name, table_name, sql_ip, sql_port, db_name etc. Test the connection (You can ignore this if you already have an sql_resolver)
3. Create a realm and map it to SQL_RESOLVER
4. Create a user account. Users -> Select Realm -> Add User (Fill up the required details).
[Note: If you already have these configs, then you can ignore the above steps]

## Step 1 (Add Policy)
1. Give a policy name. Eg: "WebQuestion"
2. Select Scope as "WebUI" from dropdown
3. Under action click "**miscellaneous**", a collapsible box will open
4. Check "login_mode" and select "**privacyIdea**" option
5. Next select "remote_user" select dropdown "**allowed**"
6. Then Select "user-realm" & "user-resolver" and finally click on "**Create Policy**"

## Step 2 (Auth to get Token)
**Endpoint :** /auth
**Method:** POST
**Payload :**
    {
    "username":"user-name",
    "password":"profile-password"
    }
**Response**
In response you will get a token on successful login. You need use this `token` for enrolling the question based token.

## Step 3 (Token Enroll with API)
**Endpoint :** /token/init
**Method:** POST
**Header:** 

    {
    "PI-Authorization":"token-value"
    }

**Payload :**

    {
	"timeStep":30,
	"otplen":6,
	"genkey":true,
	"type":"question",
	"hashlib":"sha1",
	"radius.system_settings":true,
	"2stepinit":false,
	"questions":{"What is your pet name":"dog","What is your home town":"home"},
	"validity_period_start":"",
	"validity_period_end":"",
	"pin":"123456",
	"user":"mj",
	"realm":"realm1"
}


## Step 4 (Login)
4.1. 
**Endpoint :** /auth
**Method :** POST
**Payload :**
    
    {
    "username":"user-name",
    "password":"pin-used-for-token-enrollment",
    }
**Response :**
You will get a transaction_id and the question for which you need to send the answer.

4.2.
**Endpoint :** /auth
**Method :** POST
**Payload :**

    {
    "username":"user-name",
    "password":"answer-of-the-given-question",
    "transaction_id":"transaction-id"
    }
Once successfully matched found, the status will be returned as true.

