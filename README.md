# SquareBoat Security Guidelines

At SquareBoat, we take mobile and web security seriously. Though we do understand that security is a never-ending pursuit and no matter how many doors you lock, you'll still leave a few open, we would like to do our best to ensure that.

## Laptop security

1. Only use UNIX-based operating systems for all day to day operations, which includes MacOS and Linux. Other OS's are permitted but for testing purposes only.
2. User a strong laptop password which is difficult to guess or brute-force.
3. Enable disk encryption so that others cannot unplug your hard disk and copy your data
4. No passwords stored in plain text anywhere. Use tools like Dashlane for all passwords, including personal accounts
5. Enable 2FA for all supported accounts, including email accounts etc.

## Wireless security

1. Use of strong Wifi passwords (with WPA2 encryption) which are difficult to brute-force.
2. Non trusted machines can connect but only via guest networks
3. Turn off your Wifi router when not in use.
4. Disable SSID broadcast

## Production Server security

1. No password logins on any server. Only SSH keys.
2. Default SSH port should be changed from 22 to some other port.
3. Direct SSH (even with a valid key) is not allowed. SSH access is only permitted via a jumphost.
4. fail2ban is enabled to detect multiple failed SSH attempts
5. All ports except port 80 are closed.

## Web Server security

1. SSL always - No product will be ever launched with an http:// URL.
2. Directory listings are turned off
3. Always use the latest version of Apache, PHP etc. when starting off a new project and upgrade periodically.
4. Disable directory listing

## Application security

1. Use Blade or any other templating engine to prevent XSS attacks.
2. CSRF tokens are a must for all form submissions and AJAX requests.
3. Admin login page and user login pages must be separate. The admin login page must have a captcha.
4. Send an email to the user whenever his password has changed
5. Uploaded files must be scanned for virused and malware
6. Prevent or restrict the uploading of any file that may be interpreted by the web server.
7. Validate uploaded files are the expected type by checking file headers. Checking for file type by extension alone is not sufficient.
8. Validate your redirects - Do not allow the user to supply (parts of) the URL to be redirected to.
9. Validate data on both frontend and backend
10. Always hash and save passwords, ideally using bcrypt and a salt
11. Temporary passwords and links should have a short expiration time. Enforce the changing of temporary passwords on the next use.
12. Log all authentication attempts, especially the failed attempts
13. Do not log passwords in log files
14. Turn off execution privileges on file upload directories
15. Cookies must be httponly
16. Never connect to the database with the root user
17. Throttle all API's, especially ones that can be brute forced
18. Require to enter a CAPTCHA after a number of failed logins from a certain IP address
19. Users must enter their password if they are updating their primary email or phone number which they are using for logging in.
20. When sanitizing, protecting or verifying something, prefer whitelists over blacklists.
21. Never upload user files in a directory which can be directly accessed by Apache. Always store them one level below it.
22. Never construct SQL queries manually. Always use ORM tools.
23. Never store any passwords in version control.
24. Force minimum password length rules for atleast 6 characters, if not more.
25. Re-authenticate users prior to performing critical operations. Example: Delete your account
26. For very high value accounts, use MFA (Multi-factor authentication)
27. If long authenticated sessions are allowed, periodically revalidate a user’s authorization to ensure that their privileges have not changed and if they have, log the user out and force them to re-authenticate. The application must support disabling of accounts and terminating sessions when authorization ceases.
28. Disable debug mode on production servers
29. Testing servers should always be behind HTTP auth
30. Users having admin right must use a secure password. The application should not allow weak passwords for admins (Minimum 10 characters, mix of lowercase, uppercase and digits)
31. Disable autocomplete on form fields expected to contain sensitive information (Example: Secret answers, PAN number etc.)
32. Never display code errors on production
33. Set common security headers like  Content Security Policy, X-Frame-Options, X-XSS-Protection etc.

* Content-Security-Policy: The new Content-Security-Policy HTTP response header helps you reduce XSS risks on modern browsers by declaring what dynamic resources are allowed to load via a HTTP Header

* X-Frame-Options: 'SAMEORIGIN' - allow framing on same domain. Set it to 'DENY' to deny framing at all or 'ALLOWALL' if you want to allow framing for all website. Sites can use this to avoid clickjacking attacks, by ensuring that their content is not embedded into other sites

* X-XSS-Protection: Largely unnecessary in modern browsers when sites implement a strong Content-Security-Policy.

* X-Content-Type-Options: 'nosniff' by default - stops the browser from guessing the MIME type of a file.

* Access-Control-Allow-Origin: Used to control which sites are allowed to bypass same origin policies and send cross-origin requests.

* Strict-Transport-Security: Used to control if the browser is allowed to only access a site over a secure connection. Example: Strict-Transport-Security: max-age=31536000; includeSubDomains (All present and future subdomains will be HTTPS for a max-age of 1 year. This blocks access to pages or sub domains that can only be served over HTTP.)

### Footnotes
Further reading: https://www.owasp.org/images/0/08/OWASP_SCP_Quick_Reference_Guide_v2.pdf

---
#### SquareBoat builds awesome mobile and web applications for startups. We are based out of Gurgaon, India.
---