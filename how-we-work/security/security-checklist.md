# Security checklist


## Introduction
Security in web applications is very important and, at this moment, we consider that few developers are taking it seriously.
We want to do it right, reason for which we have put together a small checklist to help us guide through the must have security checks. Some of the checks can be implemented at the code-level while others are musts on a server setup.
Most of the solutions mentioned here are focused on Javascript.
The main topics discussed on this page are:
* [System Misconfiguration](#system-misconfiguration)
* [Sensitive Data Exposure](#sensitive-data-exposure)
* [Dependency Vulnerabilities](#dependency-vulnerabilities)
* [Broken Authentication and Session Management](#broken-authentication-and-session-management)
* [Input Validation](#input-validation)
* [Cross-Site Request Forgery ( CSRF )](#cross-site-request-forgery--csrf-)
* [Cross-Site Scripting ( XSS )](#cross-site-scripting--xss-)
* [Clickjacking](#clickjacking)
* [Injection - SQL Injection](#injection---sql-injection)
* [Direct object references](#direct-object-references)


## System Misconfiguration
Most of the security attacks occur when[ server/system configuration](https://www.owasp.org/index.php/Top_10_2013-A5-Security_Misconfiguration) is not done properly.
We propose the following to be implemented:
* Inside the app configuration, disable HTTP header “x-powered by”. When using Node framework this can be implemented by using a syntax like `app.disable("x-powered-by")`.
* Always use HTTPS. If you are using HTTP, our advise is to switch to HTPPS. Also, make sure that, in the server configuration, the only opened port is `443`. Check it using `nmap` to scan all open ports on your server’s IP or using the command `netstat -lan | grep LISTEN` to display very detailed informations about how your server is communicating with other servers or network devices.
* Use SSL certificates and change them periodically or at least self signed certificates. Currently there are options like [Let's Encrypt](https://letsencrypt.org/) that can be used to get a free certificate.
* Setup firewalls.
* Use server providers that use ip filters.
* Use [iptables](https://help.ubuntu.com/community/IptablesHowTo) that filters IPs.
* Check the server's configuration and make sure it does not show its distribution ( NGINX, Apache, Haproxy, etc. ) and more importantly to not display the version of the installed distribution.
* Use machines that forward internet to production(px) servers. Px servers should not be connected directly to the internet - use instead internet gateways or [NATs](https://en.wikipedia.org/wiki/Network_address_translation).
* Implement credential rotation i.e. once in a while authorization keys/app tokens should be changed automatically.
* Implement logging system to detect flaws in applications or attacks for rogue users i.e.:
    - make sure that the logs don’t contain sensitive/invalidated information i.e. don’t log the source code, access tokens, authentication passwords, encryption keys, payment details ( account, card holder personal data ), session identification values, user’s personal data, database connection strings or any other data that should be private.
    - store the logs in a dedicated server/separate partition. The simplest server configuration will generate local logs of their actions and errors, consuming the disk on the server. In the case of this system configuration, in the case of an attack, the system is compromised and the logs can be wiped out by the intruder to clean up all the traces ( with tools like  log zapper all traces are cleaned including the ip address of the attacker ). If that happens there is no notification of the attack or no way to trace back how the attack occurred in the first place. By keeping the logs in a separate location and not on the web server itself, it is much easier to aggregate logs from different sources, logs cannot be found easily by the attackers, the log analysis can be done without affecting the server itself by not using the server’s resources, the application will not fail in case it is unable to write on the disk (  [Denial of Service condition](https://en.wikipedia.org/wiki/Denial-of-service_attack) ).
    - rotate the logs i.e. compress logs after a limited amount of time or after a maximum given size was reached.
    - monitor/review the logs to detect targeted attacks i.e. check the logs for 40x( not found errors ) and 50x( server errors ) messages. A large amount of 40x error messages might appear from [CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface) scanner tools used. The 50x server error messages appear when parts of the apps are failing e.g. the first phases of a SQL injection attack will produce these error message when the SQL query is not properly constructed and its execution fails on the back end database. Conclusions from the log analysis should be stored in a different server than the app’s server to hide any possible vulnerabilities and improper configurations.
    - implement emailing streams when too many errors with the same error code is logged.
    - keep the logs sufficient time and make backups.


## Sensitive Data Exposure
Attackers steal keys, execute man-in-the-middle attacks, or steal clear text data off the server, while in transit, or from the user’s client/browser. Previously retrieved password databases could be brute forced by Graphics Processing Units (GPUs).
We propose to focus on the following actions:
* Classify data processed, stored or transmitted by the application.
* Apply controls depending on the classification i.e. try to implement roles and multiple authentication sessions.
* Remove code comments that may reveal any sensitive information.
* Do not store any sensitive data. If it is a must, then encrypt it.
* Do not store passwords in plain text. Use instead hashed/encrypted passwords. For Node, there are packages that hash passwords e.g. [bcrypt](https://www.npmjs.com/package/bcrypt) or [scrypt](https://en.wikipedia.org/wiki/Scrypt). Also, regarding passwords, don’t allow:
    - default, weak, or well-known passwords, such as "Password1" or "admin/admin“
    - weak or ineffective credential recovery and forgotpassword processes, such as "knowledge-based answers", which cannot be made safe
    - using plain text, encrypted, or weakly hashed passwords.
* Ensure that the encryption algorithms that are used are up-to-date and have strong standards/protocols.
* Encrypt all data in transit with secure protocols such as SSL or TLS with PFS ciphers ( perfect forward secrecy ).
* Disable caching for responses that contain sensitive data.
* Verify the effectiveness of the db’s configuration.


## Dependency Vulnerabilities
Some of the attacks occur because some of the applications use already built components or dependencies that have vulnerabilities.
We propose to focus on the following actions:
* Remove unused dependencies.
* Remove unnecessary features and components.
* Do not add or expose files or documentation that is not supposed to be there (e.g. api docs).
* Check the versioning of components ( both front-end and back-end dependencies ) - use `yarn outdated` or `npm outdated` to check it.
* Use components from official sources and use secure links.
* Check for libraries and components that are unmaintained or have no security patches for older versions.
* For Javascript you can use [snyk](https://snyk.io/) to determine any possible vulnerabilities in the app’s packages.


## Broken Authentication and Session Management
The simplest application attack is automated and consists of credential stuffing i.e. the attacker has a list of valid usernames and passwords and tries them all until one is valid. That is why the app should not permit:
* Brute force or other automated attacks,
* Default, weak, or well-known passwords, such as "Password1" or "admin/admin“, uses weak or ineffective credential recovery and forgotpassword processes, such as "knowledge-based answers", which cannot be made safe,
* Plain text, encrypted, or weakly hashed passwords.


Read more about broken authentication and session management at this [link](https://www.owasp.org/index.php/Broken_Authentication_and_Session_Management).


Still, to avoid this we propose the following:
* Implement multi-factor authentication (MFA) - prevents automated, credential stuffing, brute force and stolen credential reuse attacks. E.g. gmail, internet banking apps.
* Apply the principle of least privilege - allow an user to access only the user's dedicated content; the rest should be denied.
* Use JWT (JSON Web Tokens) - read more on this [link](https://jwt.io/). To add it to your application you can find the following [tutorial](https://medium.freecodecamp.org/securing-node-js-restful-apis-with-json-web-tokens-9f811a92bb52).
* Do not deploy any default credentials, particularly for admin users.
* Implement weak-password checks ( test new or changed passwords against a list of the top [10000 worst passwords](https://github.com/danielmiessler/SecLists/tree/master/Passwords) ).
* Do not allow default, weak, or well-known passwords, such as "Password1" or "admin/admin".
* Do not allow weak or ineffective credential recovery and forgotpassword processes, such as "knowledge-based" answers.
* Align password length, complexity and rotation policies with the newest standards.
* Limit or add delay for repeatedly failed login attempts. Log all failed login attempts and alert the administrator and user for credential stuffing or brute force.
* Generate session ids with higher entropies on the server-side.
* Do not send session ids via URLs.
* In Node, brute force protection can be avoided with a package called [ratelimiter](https://www.npmjs.com/package/ratelimiter) or by implementing a middleware that adds a small delay if the same request is done to many times/minute.


## Input Validation
Input validation is a must that should be performed to ensure that only properly formed data is used in the application. The validation of input should be implemented as early as possible in the data flow mostly to prevent malformed data from persisting in the database and triggering malfunction of various downstream components.
For validation, the focus is on:
* Data validation - mostly on the server-side. If you are validating on client-side build your own reqular expressions and make sure you do not use wildcards.
* Validate data before processing i.e. check API token/key, HTTP headers, URLS, parameters.
* Specify proper character sets, such as UTF-8, for all sources of input.
* Validation agains DB schemas.
* Validate uploaded files i.e. check format, size, content, etc.
* Specify proper character sets, such as UTF-8, for all sources of input
* Type validation of expected data.
* Defining minimum and maximum value range checks for numerical parameters.
* Defining minimum and maximum length check for string parameters.
* Validate the input against a whitelist of allowed characters, whenever possible. Prefer whitelist over blacklist for input validation i.e. define arrays of allowed values for small sets of string parameters e.g. days of the week, status, flags, etc.


## Cross-Site Request Forgery ( CSRF )
[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) is an attack that occurs when a malicious web site, email, blog, instant message, or program causes a user’s web browser to perform an unwanted action on a trusted site for which the user is currently authenticated. This attack can result in transfer funds, password changing, items purchased in the user’s name.
To prevent this type of the attack we suggest the following checks:
* Check standard headers to verify the request has the same origin i.e. :     
    1. Determine where is the request coming from ( source origin ). To identify the source origin, we recommend using one of these two standard headers that almost all requests include one or both of the Origin Header or the Referer Header.
    2. Determine where is the request going to ( target origin ).
* Add CSRF token validation
* Use POST instead of GET. This option is not always effective but it gives more work to the attacker.
* Implement intermediate confirmation pages to inform the user that the operation might have other output that the one desired ( “Are you sure you really want to do this?”, “Do you want to leave the current page?” ) - not always effective but it gives more work to the attacker.
* Implement automatic logout mechanisms.
* For Node applications use [helmet](https://github.com/helmetjs/helmet) package to hide several details about the app. Helmet is a pluggable library for [ExpressJS](https://github.com/helmetjs/helmet) and [KOA](https://github.com/venables/koa-helmet) frameworks which provides a wide range of solutions related to the transport security layer. For example add the following to your code:
    - `app.use(helmet.noCache());` to prevent the browser from caching/storing the page
    - `app.use(helmet.csp());` to allow loading websites/resources only from whitelisted domains;
    - `app.use(helmet.hsts());` to block any HTTP requests and allows communication only on HTTPS;
    - `app.use(csrf());` to enable express CSRF protection;
    - `app.use(nosniff());` to force the browser to only use the Content-Type set in the response header instead of sniffing or guessing it.
* For Node, there is another package that can be used. [CSRF](https://www.npmjs.com/package/csrf) module can be used as middleware to validate an additional token that can come from the front-end part of the app.


## Cross-Site Scripting ( XSS )
[XSS](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)) is an attack that implies code injection on a web site. Basically, one site manages to run a malicious script on another site, with the privileges of you, the user. [XSS attacks](https://www.acunetix.com/websitesecurity/cross-site-scripting/) do not target a direct victim - the attack exploits a vulnerability within a website/web app that any user can visit and by that vulnerability a malicious script is delivered.
To prevent an attack we suggest the focus on the following:
* Don’t allow inserting data except in the allowed locations.
* Applying context-sensitive encoding when modifying the browser document on the client side acts against DOM XSS.
* Use frameworks that automatically escape XSS by design ( ReactJS, RoR )
* For Node use the `helmet` package mentioned above to hide several details about the app. For example:
    - `app.use(helmet.hsts());` to block any HTTP requests and to allow communication only on HTTPS
    - `app.use(helmet.xssFilter());` to enables XSS filter
    - `app.use(helmet.iexss());` to enable XSS filter in IE (it is `on` by default)

## Clickjacking
[Clickjacking](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet) is an attack that consists in tricking an user into clicking on something different from what the user perceives they is clicking on. The result might be revealing confidential information, losing control of the device in use, making a payment, etc. The attack takes the form of embedded code or script that is executed without the user’s knowledge when a simple operation of clicking ( of a different function ) on a button is performed.
The security checks that one should consider implementing are:
* Employing defensive code in the UI to ensure that the current frame is the most top level window
* Sending the proper Content Security Policy (CSP) frame-ancestors directive response headers that instruct the browser to not allow framing from other domains. This replaces the older X-Frame-Options HTTP headers.
* For Node apps use `helmet` package to prevent opening a page inside of an frame or iframe i.e. add `app.use(helmet.xframe());` to your index file.

## Injection - SQL Injection
In general, when speaking about injection in terms of security we refer at the process of inserting any source of data inside the app i.e. over-writing environment variables, parameters, etc. with hostile data.
Some security check are listed below:
* Use a safe API, which avoids the use of the interpreter entirely or provides a parameterized interface, or migrate to use Object Relational Mapping Tools (ORMs).
* Validate, filter and sanitize user-supplied data ( Use server-side input validation )
* Use LIMIT and other SQL controls within queries to prevent mass disclosure of records in case of SQL injection.

In particular, [SQL Injection](https://en.wikipedia.org/wiki/SQL_injection) is an attack that consists in accessing/corrupting database structure by using application codes. This type of attack allows creating, reading, updating, altering or deleting data stored in the database. Used when user input is incorrectly filtered for string literal escape characters embedded in sql or when user input in not strongly type and unexpectedly executed.
For this type of attack, one should focus on:
* Never building SQL statements from the user input. To implement this read more at this [link](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet).

## Direct object references
[Insecure Direct Object References](https://www.owasp.org/index.php/Testing_for_Insecure_Direct_Object_References_(OTG-AUTHZ-004)) allow attackers to bypass authorization and access resources directly by modifying the value of a parameter used to directly point to an object. Such resources can be database entries belonging to other users, files in the system, and more. This is caused by the fact that the application takes user supplied input and uses it to retrieve an object without performing sufficient authorization checks.
To prevent this type of attack one can:
* Use per user or session indirect object references to prevent from directly targeting unauthorized resources.
* Check access at every user action i.e. each use of a direct object reference from an untrusted source must include an access control check to ensure that the user is authorized for the requested object.
Read more at this [link](https://www.owasp.org/index.php/Top_10_2013-A4-Insecure_Direct_Object_References).

### Resources:
* [OWASP](https://www.owasp.org)
