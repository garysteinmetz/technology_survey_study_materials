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

#### HTTPS

##### Public-Key Encryption

Hashing
NP-Complete
Encryption
Certificates
Trust Store
encryption types
quantum computing to break encryption

## Web-Browser Security

### Within Browser
http-only cookie
Client-side scripting
httponly cookie


## Network Security
Denial-of-service attack
Brute-force attack
blacklist and whitelist



## Human Element

Inside Job

Bamford's Theorem

### Outside Organization
Cross-site scripting
captcha
two-factor authentication


Hashing prevents outsiders from guessing the next number in the sequence

Bit coin
