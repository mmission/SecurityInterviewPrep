## Web App Security Principles


### Server Side Input Validation
Input validation is the process of ensuring input data is consistent with application expectations. Data that falls outside of an expected set of values can cause our application to yield unexpected results, for example violating business logic, triggering faults, and even allowing an attacker to take control of resources or the application itself. Input that is evaluated on the server as executable code, such as a database query, or executed on the client as HTML JavaScript is particularly dangerous. Validating input is an important first line of defense to protect against this risk.

Techniques for Input validation
* whitelisting
  * only allowing known acceptable types (positive validation)
    * For example, only allowing numbers for a input field that requires a number only
* blacklisting
  * rejecting input that contains known dangerous values (negative validation)
    * main concern with blacklist is that the number of possible bad inputs is extremely large, so maintaining a list can be time consuming and difficult
* if you need to reflect back the user's improper input... make sure to output encode the input
  * otherwise you might get a reflective XSS attack that steals your session cookie  
* Sanitization
  * a blacklist where you remove undesirable input rather than rejecting it all together
  * main problem here, is that it is hard to do because an attacker can try to evade the sanitization  
    * ex: sanitizing <script> would be evaded with: <scr<script>ipt>


Some Frameworks have built-in validation:
* Ruby on Rails
  * built in Active Record Validators
* Play
  * built in validators
* NodeJS
  * validator-js
* Javascript
  * xss-filters
* In general
  * regex-based validation on application inputs


In Summary
  * White list when you can
  * Black list when you can't whitelist
  * Keep your contract as restrictive as possible
  * Make sure you alert about the possible attack
  * Avoid reflecting input back to a user
  * Reject the web content before it gets deeper into application logic to minimize ways to mishandle untrusted data or, even better, use your web framework to whitelist input
  * Remember: if you don't control it, you can't trust it. If it violates the contract, reject it!


### Encode HTML/CSS/JavaScript Output
Browsers try their best to render the content even if its malformed. Attackers have the luxury of injecting content into your pages to break through execution contexts, without even having to worry about whether the page is valid.

Output Encoding = is converting outgoing data to a final output format.


Pro tips/In Summary:
* You are much better off storing the data in its most raw form, then handling encoding at rendering time (this evades unneeded complexity)
* Finally, it's worth noting that nested rendering contexts add an enormous amount of complexity and should be avoided whenever possible. It's hard enough to get a single output string right, but when you are rendering a URL, in HTML within JavaScript, you have three contexts to worry about for a single string.
* Output encode all application data on output with an appropriate codec
* Avoid unsafe framework and JavaScript calls that avoid encoding
* Use your framework's output encoding capability, if available

### Bind Parameters for Database Queries
Parameter Binding provides a means of separating executable code (such as SQL) from content, transparently handling content encoding and escaping.


All query languages (SQL or otherwise, so even NoSQL) require a clear separation between executable code and content so the execution doesn't confuse the command from the parameter.


You can still be vulnerable to an injection attack even if you use an ORM if the queries you are building are using untrusted input without binding


For example:
* Ruby on Rails
  * good
    * where (foo: bar)
    * where ("foo = ?", bar)
  * bad
    * where("foo = '#{bar}'")
    * where("foo = '" + bar + "'")
* JDBC
  * good
    * Connection.prepareStatement() used with setXXX() methods and bound parameters for all input
  * bad
    * any query or update method called with string concatenation rather than binding
* MySQL
  * good
    * prepare() used with bind_param
  * bad
    * any query or update method called with string concatenation rather than binding
* MongoDB
  * good
    * Basic CRUD operations such as find(), insert(), with BSON document field names controlled by application.
  * bad
    * Operations, including find, when field names are allowed to be determined by untrusted data or use of Mongo operations such as "$where" that allow arbitrary JavaScript conditions.

In Summary
  * Avoid building SQL (or NoSQL equivalent) from user input
  * Bind all parameterized data, both queries and stored procedures
  * Use the native driver binding function rather than trying to handle the encoding yourself
  * Don't think stored procedures or ORM tools will save you. You need to use binding functions for those, too
  * NoSQL doesn't make you injection-proof

### Protect Data in Transit

HTTPS & Transport Layer Security
HSTS
Protect cookies
* secure flag on a cookie, instructs browser to only send the cookie using HTTPS
* httponly flag on a cookie means the cookie cannot be accessed through client side script (only if the browser supports this flag)
* same-site flag, which prevents the browser from sending this cookie along with cross-site requests.

In Summary
* Use HTTPS for everything!
* Use HSTS to enforce it
* You will need a certificate from a trusted certificate authority if you plan to trust normal web browsers
* Protect your private key
* Use a configuration tool to help adopt a secure HTTPS configuration
* Set the "secure" flag in cookies
* Be mindful not to leak sensitive data in URLs
* Verify your server configuration after enabling HTTPS and every few months thereafter

### Hash & Salt User passwords
Argon2 for hashing passwords  because it is resistant to attacks using GPUs and other specialized hardware
salt needs to be unique per user

### Authenticate Users Safely
Authentication is the process of verification that an individual, entity, or website is who it claims to be.

Authentication Solution and Sensitive Accounts
  * Do NOT allow login with sensitive accounts (i.e. accounts that can be used internally within the solution such as to a back-end / middle-ware / DB) to any front end user interface
  * Do NOT use the same authentication solution (e.g. IDP / AD) used internally for unsecured access (e.g. public access / DMZ)

Passwords
* password strength - length, complexity, ban common used passwords
* implement secure password recovery
  * forgot password cheat sheet [forgot password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html)
* store passwords in a secure fashion [password storage](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
* transmit passwords only over TLS
* re-require authentication for sensitive features
  * in order to mitigate CSRF & session hijacking, it's important to require the current credentials for an account before updating sensitive account info such as the user's password, user's email, sensitive transactions (shipping a purchase to a new address)
  * w/o this an attacker could execute sensitive transactions thru a CSRF or XSS attack without needing to know the user's credentials


MFA/2FA
* adds a second method of identity verification to secure your account
  * can use a unique one time code through a text message, or through an application like Google Authenticator

### Protect User Sessions

### Authorize actions
Authorization defines whether a user is allowed to do something











#### resources
[Web Security Basics](https://martinfowler.com/articles/web-security-basics.html)
[Authentication](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)
