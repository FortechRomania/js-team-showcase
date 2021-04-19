# QA's Security checklist

## Introduction
Security in web applications is very important and, at this moment, we believe that few developers are taking it seriously.
As QA, we want to make sure all is set in a proper way and the apps have no security breaches. For this reason we have put together a small checklist to help us guide through the must have security checks. Some of the checks can be included in the app's automated tests while others (e.g. security checks focused on the server setup) should run as scripts in the terminals.

The solutions mentioned here are focused on Javascript.

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
Most of the security attacks occur when [server/system configuration](https://www.owasp.org/index.php/Top_10_2013-A5-Security_Misconfiguration) is not done properly.

Things we suggest to be tested:
* Verify that HTTP header “x-powered by” is disabled. When dealing with Node API check the response for `app.disable("x-powered-by")`.
* Make sure the applications always uses HTTPS. Check that, in the server configuration, the only opened port is `443`. Check it using `nmap` to scan all open ports on your server’s IP e.g. `nmap website.com`. To check specific things read about [Linux scanning network for open ports](https://www.cyberciti.biz/tips/linux-scanning-network-for-open-ports.html). Another option might be checking some of the ports on [canyouseeme.org/](http://canyouseeme.org/).
* The app should have its own SSL certificates. To verify the presence of the certificates check the response of `curl -vvI https://website.com`
* Verify that server distribution (NGINX, Apache, Haproxy, etc.) and more importantly the version are not visible.
* Use tools like Locust.io to check if a logging system is implemented and [Denial of Service condition](https://en.wikipedia.org/wiki/Denial-of-service_attack) is not applied. Use brute force for requests like `/login` to make sure delay is added on fail.

More information can be read on [tutorialspoint.com, Testing security misconfiguration](https://www.tutorialspoint.com/security_testing/testing_security_misconfiguration.htm).

## Sensitive Data Exposure
Attackers steal keys, execute man-in-the-middle attacks, or steal clear text data off the server, while in transit, or from the user’s client/browser. Previously retrieved password databases could be brute forced by Graphics Processing Units (GPUs).
Things we suggest to be tested:
* Check that developers classify the data processed, stored or transmitted by the application.
* Check if the app's control depends on the classification i.e. make sure roles are implemented and that multiple authentication sessions are in place.
* Make sure that no sensitive data is stored. If it is a must, make sure it is encrypted and that the key is not public.
* Make sure sensitive data is not exposed or hardcoded in the code/logs. To do that use `grep -r –E "Pass | password | pwd |user | guest| admin | encry | key | decrypt | sharekey " ./PathToSearch/` or `grep -r " {2\}[0-9]\{6\} "  ./PathToSearch/`
* Verify that the passwords are not stored in plain text. Verify if packages that hash/encrypt passwords e.g. [bcrypt](https://www.npmjs.com/package/bcrypt) or [scrypt](https://en.wikipedia.org/wiki/Scrypt) are used. Also, regarding passwords, make sure you test for:
    - default, weak, or well-known passwords, such as "Password1" or "admin/admin“
    - weak or ineffective credential recovery and forgotpassword processes, such as "knowledge-based answers", which cannot be made safe

More details can be found [on owasp.org, Testing for Sensitive Information](https://www.owasp.org/index.php/Testing_for_Sensitive_information_sent_via_unencrypted_channels_(OTG-CRYPST-003)).

## Dependency Vulnerabilities
Some of the attacks occur because some of the applications use already built components or dependencies that have vulnerabilities.
Things we suggest to be tested:
* Check that there are no unused dependencies.
* Check if unnecessary features and components are present - make sure the automated tests have a good coverage.
* Make sure that files or documentation that is not supposed to be there (e.g. api docs) is not displayed to the public.
* Check the versioning of components (both front-end and back-end dependencies) - use `yarn outdated` or `npm outdated` to check it.
* Make sure the components are from official sources and use secure links.
* Check for libraries and components that are unmaintained or have no security patches for older versions.
* Use tools like [snyk](https://snyk.io/) to determine any possible vulnerabilities in the app’s packages. Other tools can be found on [techbeacon.com](https://techbeacon.com/13-tools-checking-security-risk-open-source-dependencies-0).

## Broken Authentication and Session Management
The simplest application attack is automated and consists of credential stuffing i.e. the attacker has a list of valid usernames and passwords and tries them all until one is valid.

To avoid this we to check if the following are in place:
* Multi-factor authentication (MFA) - prevents automated, credential stuffing, brute force and stolen credential reuse attacks. E.g. gmail, internet banking apps.
* The principle of least privilege - allows an user to access only the user's dedicated content; the rest should be denied. Use `curl -kis http://website.com/notsupposetosee/` to verify.
* JWT (JSON Web Tokens) - read more on [jwt.io](https://jwt.io/). Check if it is added to your application.
* Weak-password checks (test new or changed passwords against a list of the top [10000 worst passwords](https://github.com/danielmiessler/SecLists/tree/master/Passwords)).
* No default, weak, or well-known passwords, such as "Password1" or "admin/admin".
* No weak or ineffective credential recovery and forgotpassword processes, such as "knowledge-based" answers.
* Password length, complexity and rotation policies aligns with the newest standards.
* Limited or delayed responses for repeatedly failed login attempts. Also, make sure al failed login attempts are logged and alert the administrator for credential stuffing or brute force.
* Session ids have higher entropies on the server-side.
* Session ids are not sent via URLs.
* Check if in Node, brute force protection is avoided with packages like [ratelimiter](https://www.npmjs.com/package/ratelimiter) or by implementing a middleware that adds a small delay if the same request is done to many times/minute.

More details can be found on [tutorialspoint.com, Testing Broken Authentication](https://www.tutorialspoint.com/security_testing/testing_broken_authentication.htm) or on [owasp.org, Testing for Session Management](https://www.owasp.org/index.php/Testing_for_Session_Management).

## Input Validation
Input validation is a must that should be performed to ensure that only properly formed data is used in the application. The validation of input should be implemented as early as possible in the data flow mostly to prevent malformed data from persisting in the database and triggering malfunction of various downstream components.

Check for the following:
* Data validation - mostly on the server-side. If you are validating on client-side make sure the reqular expressions does not contain wildcards.
* Validate data before processing i.e. check API token/key, HTTP headers, URLS, parameters.
* Check if proper character sets e.g. UTF-8, are used for all sources of input.
* Check for validation against DB schemas.
* Check if uploaded files are valid i.e. check format, size, content, etc.
* Check the validity of expected data.
* Check minimum and maximum value range for numerical parameters.
* Check minimum and maximum length for string parameters.
* Check the input against a whitelist of allowed characters, whenever possible. Makes sure it is preferred whitelists over blacklists for input validation i.e. check if there is a defined array of allowed values for small sets of string parameters e.g. days of the week, status, flags, etc.

More details can be found on [owasp.org, Testing for Input Validation](https://www.owasp.org/index.php/Testing_for_Input_Validation).

## Cross-Site Request Forgery (CSRF)
[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) is an attack that occurs when a malicious web site, email, blog, instant message, or program causes a user’s web browser to perform an unwanted action on a trusted site for which the user is currently authenticated. This attack can result in transfer funds, password changing, items purchased in the user’s name.

To prevent this type of the attack we suggest the following checks:
* Check standard headers to verify the request has the same origin i.e.:     
    1. Determine where is the request coming from (source origin). To identify the source origin, we recommend using one of these two standard headers that almost all requests include one or both of the Origin Header or the Referer Header.
    2. Determine where is the request going to (target origin).
* Check for CSRF token validation
* Check POST is used instead of GET. This option is not always effective but it gives more work to the attacker.
* Check for intermediate confirmation pages to inform the user that the operation might have other output that the one desired (“Are you sure you really want to do this?”, “Do you want to leave the current page?”).
* Check for automatic logout mechanisms.
* Make sure Node applications use [helmet](https://github.com/helmetjs/helmet) package to hide several details about the app.
* Make sure that packages like [CSRF](https://www.npmjs.com/package/csrf) are used. This is a module used as middleware to validate an additional token that can come from the front-end part of the app.

More details can be found on [owasp.org, Testing for CSRF](https://www.owasp.org/index.php/Testing_for_CSRF_(OTG-SESS-005)).

## Cross-Site Scripting (XSS)
[XSS](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)) is an attack that implies code injection on a web site. Basically, one site manages to run a malicious script on another site, with the privileges of you, the user. [XSS attacks](https://www.acunetix.com/websitesecurity/cross-site-scripting/) do not target a direct victim - the attack exploits a vulnerability within a website/web app that any user can visit and by that vulnerability a malicious script is delivered.
To check if this type of attacks might happen test for the following:
* Data cannot be inserted in any other locations except in the allowed ones.
* The app is built in frameworks that automatically escape XSS by design (ReactJS, Ruby on Rails)
* If Node is in use, check for packages like `helmet`. For example:
    - check that the browser from caching/storing the page - check if the index file contains a syntax like `app.use(helmet.noCache());`.
    - check that the loading websites/resources is allowed only from whitelisted domains - check if the index file contains `app.use(helmet.csp());`
    - check that HTTP requests are blocked and that the only allowed communication is done on HTTPS - check for `app.use(helmet.hsts());` syntax.
    - check if express CSRF protection is enabled - check if the syntax `app.use(csrf());` is added.
    - check if the browser is forced to only use the Content-Type set in the response header instead of sniffing or guessing it. Check for `app.use(nosniff());` syntax.

Other particularities can be found on [owasp.org, Testing for XSS](https://www.owasp.org/index.php/Testing_for_Cross_site_scripting).

## Clickjacking
[Clickjacking](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet) is an attack that consists in tricking an user into clicking on something different from what the user perceives they is clicking on. The result might be revealing confidential information, losing control of the device in use, making a payment, etc. The attack takes the form of embedded code or script that is executed without the user’s knowledge when a simple operation of clicking (of a different function) on a button is performed.
The security checks that should be verified are:
* In the UI, the current frame is the most top level window.
* The proper Content Security Policy (CSP) frame-ancestors directive response headers are used i.e. the browser does not allow framing from other domains.
* If the app is built with Node, check if packages like `helmet` are used to prevent opening a page inside of an frame or iframe i.e. check if the index file contains a syntax like `app.use(helmet.xframe());`.

Other particularities can be found on [owasp.org, Testing for Clickjacking](https://www.owasp.org/index.php/Testing_for_Clickjacking_(OTG-CLIENT-009)).

## Injection - SQL Injection
In general, when speaking about injection in terms of security we refer at the process of inserting any source of data inside the app i.e. over-writing environment variables, parameters, etc. with hostile data.
In particular, [SQL Injection](https://en.wikipedia.org/wiki/SQL_injection) is an attack that consists in accessing/corrupting database structure by using application codes. This type of attack allows creating, reading, updating, altering or deleting data stored in the database. Used when user input is incorrectly filtered for string literal escape characters embedded in sql or when user input in not strongly type and unexpectedly executed.

For this type of attack, one should test if:
* SQL statements cannot be built from the user input.

More details can be found on [owasp.org, Testing for SQL Injection](https://www.owasp.org/index.php/Testing_for_SQL_Injection_(OTG-INPVAL-005)).

## Direct object references
[Insecure Direct Object References](https://www.owasp.org/index.php/Testing_for_Insecure_Direct_Object_References_(OTG-AUTHZ-004)) allow attackers to bypass authorization and access resources directly by modifying the value of a parameter used to directly point to an object. Such resources can be database entries belonging to other users, files in the system, and more. This is caused by the fact that the application takes user supplied input and uses it to retrieve an object without performing sufficient authorization checks.
To prevent this type of attack one should check [owasp.org, Testing for Insecure Direct Object Reference](https://www.owasp.org/index.php/Testing_for_Insecure_Direct_Object_References_(OTG-AUTHZ-004)).

### Resources:
* [OWASP](https://www.owasp.org)
