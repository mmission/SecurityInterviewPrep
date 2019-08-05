### Authentication


Multi-factor Authentication (MFA)
  * MFA involves providing an extra layer of security by ensuring users provide more than 1 piece of information for identification/authentication
    * it typically requires a combo of something the user knows (pin, password, secret question answer) and something the user has (card, hardware token, phone)
    * usually 2FA is the most used type of multifactor authentication

Different ways to implement MFA:
  * Time-based One-Time Password (TOTP)
  * Event or Hash based One-Time Password (HOTP)
  * Short Message Service (SMS)
  * Electronic Mail (email)
  * push notification
  * UTF

TOTP:
  * generate a one time password from a shared secret key and the current timestamp using a specific crypto hash function (like SHA-256) and then a mod is taken of how many digits the OTP should be and the OTP is valid for a specific time duration then
  * TOTP involves the enrollment & login processes
    * enrollment process:
      * a user logs into a website with username/password
      * if the creds are valid, they progress to enable 2FA
      * a shared-key is requested (usually in the form of a QR code)
      * the key is stored by an app that implements TOTP (like Google Authenticator or Auth0 Guardian)
      * 2FA is then enabled
    * login process:
      * user logs in with valid username/password
      * then the user is prompted to enter a OTP generated from the mfa app
      * the server verifies that the code is valid and finally authenticates the user

UTF:
  * The U2F protocol involves the client in the authentication process (for example, when logging in to a web application, the web browser is the client). When a user registers a U2F device with an online service, a public/private key pair is generated.
  * After registration, when the user attempts to log in, the service provider sends a challenge to the client. The client compiles information about the source of the challenge, among other information. This is signed by the U2F device (using the private key) and sent back to the server (service provider).
  * Real-time challenge-response schemes like U2F address OTP vulnerabilities such as phishing and various forms of man-in-the-middle attacks. As the legitimate server is issuing the challenge, if a rogue site or middle-man manipulates the flow, the server will detect an abnormality in the response and deny the transaction
