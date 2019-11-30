## Configure Scope - Authentication Policy

```
Policy Name   : 'Any Name You Want'
Scope         : `authentication` 
Action
    * __miscellaneous__
    >  challenge_response : `email`
    >
    >  emailsubject       : `MFA OTP Request` - the email OTP Subject
    >
    >  passthru           : `userstore` - to authenticate against userstore.
    >
    > reset_all_user_tokens : (Checked)
    >
    >

User-Realm   : Select your Realm
User-Resolver: Select User Resolver(s)

```
