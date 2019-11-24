## MFA Process

1. Register user (if new) to Privacy Idea 
2. User Authentication (with valid username and password)
..* On successful authentication it generates a 'authentication token' which is required for other API calls
3. Token Init
..* It is the process which will generate a 'token' (MFA token), which will (Generate Email OTP / other OTP )
4. Token Auth
..* Process of validating the OTP