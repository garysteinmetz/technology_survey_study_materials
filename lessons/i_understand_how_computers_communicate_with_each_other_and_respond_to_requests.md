# I Understand How Computers Communicate with Each Other and Respond to Requests

## Ye Olden Days

Decades ago, most computers were very big (room-sized `mainframes`) and did all the processing
by their own selves or entirely within their own firm (like a government agency).
Data sharing between computers was often slow and frequently involved the physical transfer
of a storage device like a large roll of magnetic tape.

All of these things (like mainframes and magnetic tape) are still used but the vast
majority of computers now are PCs, laptops, tablets, and mobile phones.

### Ye Modern Times

Now, with the internet, computers are constantly communicating with each other.
By default, they use the `IP Protocol` over a `TCP connection` to communicate.

## Identifiers

### Physical (MAC) Address

Internet-ready computers have one or more `network interface cards` (NICs) which enable
Internet-based communication. These are chips that allow wireless communication
or a more traditional `RJ45 jack` (outlet) where the end of an internet cable can be
plugged into.

Each of these NICs has a unique identifier assigned to it known as a `MAC address`.
A MAC address is a ordered grouping of six two-digit `hexadecimal` numbers, like
`59:A6:12:E4:BC:FD`. `Because MAC addresses are supposed to be unique,
no two NIC cards should share the same MAC address.`

#### What Is Hexadecimal?
The decimal system (used by everyone) has a total of ten combinations per digit
(0 through 9). A hexadecimal system uses a total of sixteen combinations per digit
(0 through 15). To represent the numbers 10, 11, 12, 13, 14, and 15, the letters
'A', 'B', 'C', 'D', 'E', and 'F' are used, respectively.

In decimal, each more significant digit has 10 times more value than the one that
preceded it. Here's an example.

```
125 =

1 * 100 = 100
2 * 10 = 20
5 * 1 = 5

= 100 + 20 + 5 = 125
```

In hexadecimal, each more significant digit has 16 times more value than the one that
preceded it. Here's an example.

```
B7 =

B = 11*16 = 176
7 = 7*1 = 7

= 176 + 7 = 183 (in decimal)
```

#### Why Is Hexadecimal Used?
At its foundation, a computer represents a number using one or more transistors
that are either in a high-voltage (represented by the number one) or a low-voltage
(represented by the number zero) state. This collection of ones and zeros forms
a `binary` number (just two combinations per digit). Here's an example.

```
1011 =

1 * 8 = 8
0 * 4 = 0
1 * 2 = 2
1 * 1 = 1

= 8 + 0 + 2 + 1 = 11 (in decimal, or 'B' in hexadecimal)
```

A hexadecimal digit is just an ordered set of four binary numbers. It's more convenient
to write the hexadecimal number `F7EA` than `1111011111101010`.

Hexadecimal is used because binary is the native number system in computers and
hexadecimal is a convenient way of representing binary.

### Virtual (IP) Address

Computers don't share their MAC addresses over the entire internet, instead they obtain
an alias known as an `IP address` that maps to the MAC address and then communicate
using this IP address. An IP address is an ordered grouping of four two-digit
`hexadecimal` numbers, but each number is normally represented in decimal (a number
between 0 and 255 ('FF' in hexadecimal)).

An example of an IP address is `172.217.11.36` (which is the address of 'www.google.com'
at the time of this writing).

A computer can set the IP address, along with other information
like subnet and gateway address on a NIC, but it normally just uses the `DHCP`
protocol to have one assigned to it.

While the traditional IP-address numbering system (`IPv4`) offers
over 4 billion combinations ('0.0.0.0' to '255.255.255.255'), that has increasingly
been considered too few with so many computers now being used. A newer standard (`IPv6`)
relies on a whopping 128 bits (32 hexadecimals instead of IPv4's 8) totalling over
340 undecillion combinations!

#### Exercise - Getting the MAC Address and IP Address of One's Own Computer
From the command prompt in Windows, enter `ipconfig /all` to retrieve the IP and MAC
addresses assigned to each NIC on your computer. For Macs (and Linux), the comamnd
is `ifconfig -a`.

#### Exercise - Loopback Address
The IP address `127.0.0.1` is a reserved address meaning 'my own machine (myself)'.
It is known as the `loopback address` and generally given the label `localhost`
by machines. When web developers are testing web apps out on their own computers,
they will frequently use URLs like 'http://localhost:8080/index.html' in their browsers.

On Macs (and Linux), the `/etc/hosts` file declares this mapping. On Windows,
the file is located at `C:\Windows\System32\drivers\etc\hosts`. Review the contents
of this file and confirm that IP address `127.0.0.1` is associated with `localhost`.
Note that this file is considered important and may not be viewable by those
accounts without administrative access.

### DNS ('Friendly') Name
While it is possible to enter an IP address into a browser, a friendly `DNS Name`
(like 'www.google.com') is usually entered instead. DNS servers manage the mapping
between IP addresses and DNS names.

Beyond convenience, one advantage of using a DNS names is that switching from one
server (and its IP address) to another (and its IP address) is just a matter of updating
the DNS name's entry in the DNS server.

#### Exercise - Determine the IP address assigned to a DNS name

From the command line, use the `nslookup` command to get the IP address of a website.

```
nslookup www.google.com

Server:		192.168.1.1
Address:	192.168.1.1#53

Non-authoritative answer:
Name:	www.google.Com
Address: 172.217.12.196
```

In this case, 'www.google.com' has an assigned IP address of '172.217.12.196'.
Enter that address into the browser with 'http://' prefix ('http://172.217.12.196'
in this case) and confirm that the Google search page loads.

#### Exercise - Determine how a call gets to its destination

Internet calls get directed through different `gateways` (think of them as road
intersections) to reach their destinations. The `traceroute` command determines which
gateways the call goes through and how long it takes to go through each gateway,
which can be valuable for troubleshooting the location of problems ('latencies')
when calls hang or are unusually slow.

```
traceroute www.google.com

traceroute to www.google.com (172.217.12.164), 64 hops max, 52 byte packets
 1  fios_quantum_gateway (192.168.1.1)  4.264 ms  3.822 ms  6.533 ms
 2  * * *
 3  b4301.nwrknj-lcr-21.verizon-gni.net (130.81.58.126)  18.007 ms  11.105 ms
    b4301.nwrknj-lcr-22.verizon-gni.net (130.81.58.124)  4.532 ms
 4  * * *
 5  0.et-8-1-5.gw7.ewr6.alter.net (140.222.233.31)  10.089 ms
    0.et-11-3-0.gw7.ewr6.alter.net (140.222.239.51)  6.238 ms
    0.et-9-1-5.gw7.ewr6.alter.net (140.222.2.229)  7.838 ms
 6  209.85.149.208 (209.85.149.208)  10.049 ms  12.022 ms  9.150 ms
 7  * * *
 8  216.239.42.166 (216.239.42.166)  16.829 ms
    172.253.72.128 (172.253.72.128)  9.078 ms  9.513 ms
 9  108.170.248.52 (108.170.248.52)  11.283 ms
    108.170.248.116 (108.170.248.116)  10.231 ms
    172.253.69.227 (172.253.69.227)  8.254 ms
10  216.239.62.196 (216.239.62.196)  10.355 ms
    209.85.255.27 (209.85.255.27)  23.169 ms  14.651 ms
11  209.85.254.128 (209.85.254.128)  15.650 ms
    lga25s62-in-f4.1e100.net (172.217.12.164)  23.891 ms
    209.85.254.238 (209.85.254.238)  16.257 ms
```

In this case, the call goes through the home gateway ('fios_quantum_gateway')
before going to a Verizon gateway ('b4301.nwrknj-lcr-22.verizon-gni.net' where
'nj' could very well mean New Jersey) before going to larger regional then national
gateways before finally reaching the Google server at '172.217.12.164'.

### Subnets and Gateways

While they only process messages sent to them, NICs listen to all internet traffic
transmitted on the networks they're assigned to (they have to check everything and
determine which messages to pay attention to).

In order for these NICs not to be overwhelmed by IP traffic, networks are divided
into `subnets` and `gateways` determine whether traffic should stay within a subnet
or be routed to the wider internet.

That's another reason why internet communication is based on IP addresses instead
of MAC addresses - MAC addresses within a various subnet can vary widely but all the
IP addresses assigned to them will fall in the same range.

## HTTP

HTTP stands for `Hypertext Transfer Protocol` which is a protocol for sending messages
to and from servers. A 'client' starts by sending one message (request) to the server
then the server sends a corresponding message (response) back.

HTTP (and HTTPS, the encrypted version of HTTP) is the major protocol used
by browsers. It's also a very popular protocol for communication between servers.

### Client and Server

In the case of a web browser searching Google, the web browser is acting
as the client asking Google for search results and Google is acting
as the server sending the search results back to the browser.

```
(Client)
Browser
  --     HTTP Client Request to 'GET' Search Results      -->
                                                              (Server)
                                                              Google
  <-- HTTP Server Response With Search Results (HTML Page) --
(Client)
Browser
```

Note the use of the word 'GET' here, which is a type of HTTP request 'method' which
(not surprisingly) gets information from a server. Whenever you type a URL into
a browser's address bar, the browser attempts to 'GET' information from a server.

If a browser finds references to other resources
(like images, CSS, and JavaScript) while downloading a web page, it will make
other HTTP requests to get those resources. (Note that when the internet is slow,
this is why the text will appear on an HTML page first before the images and
styling appear.)

#### Exercise - Make Basic HTTP Call from Command Line
In general, servers don't care what kind of client is making the request,
the server will just service the request based on typical information found
in the HTTP request. Whether the client is a browser or the command line
or something else, the server should give the same response. (There is an optional
`User-Agent` HTTP `request header` that the client can use to state what type
of client it is (like 'User-Agent: Chrome'), but servers usually ignore this header.)

The `curl` command is a command prompt (terminal) command for making HTTP
(and HTTPS, the encrypted version of HTTP) client requests. Open a command prompt
and enter `curl <URL>` where `<URL>` is the a web site that you frequently use,
like `curl https://www.google.com`, and study the HTML that is returned from the
server.

Then open the developer tools in Chrome -

  - On Mac, hold down both `command` and `option` then press `i`
  - On Windows, hold down both `control` and `shift` then press `i`

Go to the same URL in Chrome then click the 'Network' tab in Chrome developer tools.
Click the top entry under the 'Name' column then click its associated 'Response' tab.
The response HTML here should be similar or the same to what was received by
the `curl` command.

Note that, for a site like Google, the server may consider
things like cookies and `User-Agent` header then generate a response that's slightly
different than the `curl` command. However, `curl` has options to include cookies
and headers so, if it specified everything that a browser submitted, the response
to the `curl` command would be identical to the response received by the browser.

The overall goal here is to show that whether using the browser, `curl`,
or something else, servers treat all HTTP requests by what was sent, not
who sent it.

#### Exercise - Study HTTP Calls Made During Page Load
Continuing on the last exercise, open Chrome and turn on its developer tools,
then go to a web site. Click the 'Network' tab in Chrome developer tools
then click the 'Preview' tab.
Click the top entry under the 'Name' column (this is the URL you entered).
If this entry (HTML page) doesn't reference anything else (like images, CSS,
and JavaScript), then there won't be any entries below it, but most every
popular web page will.

Moving downward, click the each entry in the 'Name' column and check what appears
in the 'Preview' pane - recognizable JavaScript, CSS, or image should appear
in many cases. For at least one image, right-click over it's 'Name' entry,
select 'Copy', then click 'Copy address link' . Then paste this URL into another
browser tab (preferably with Chrome developer tools on too)
and view the image on its own - if Chrome developer tools are on then just one
entry should appear in the 'Name' column because, unlike an HTML page,
the image doesn't need to make any additional calls to fully represent itself.

#### Server Can Make Client Requests Too

Note that a server itself can make client requests to other servers. If the browser
submits 'weather' in a search request to Google, Google may in turn
(now acting as a client) make an HTTP request to the National Weather Service
to get the current weather forecast before sending it back the browser.

```
(Client)
Browser
  -- Search 'weather' -->
                       (Server, About to Make Client Request)
                       Google
                         -- Get weather forecast -->
                                                  (Server)
                                                  National Weather Service
                         <--   Weather forecast   --
                       (Server)
                       Google
  <-- Weather HTML Page --
(Client)
Browser
```

### URL

The `URL (Uniform Resource Locator)` is a String with summary information
as to (a) which server the client wants to contact, (b) where on the server
the client wants to contact, and (c) some (or all) of the information
that the client wants to send. Note that there is usually other information beyond
the URL that composes the overall HTTP request (and response).

URLs can be simple like `https://www.google.com` but can also be very lengthy
and follow this form (documented on Wikipedia) -
```
            userinfo          host        port
        ┌───────┴───────┐ ┌────┴────────┐ ┌┴┐
 http://john.doe:password@www.example.com:123/forum/questions/?tag=networking&order=newest#top
 └─┬─┘ └───────────┬────────────────────────┘└─┬─────────────┘└────────┬──────────────────┘└┬─┘
 scheme         authority                      path                  query             fragment
```

#### Scheme
Scheme is the protocol used to obtain information. While this value _can_ be
many things (like 'ftp'), it's almost always either 'http' or 'https' .

#### User Info
'userinfo' can specify a user's name/password combination but this is hardly
every used to authenticate a user. (The 'Authorization' request header
is now very popular for authentication.) If 'userinfo' isn't specified, then
the '@' character that follows it shouldn't be included.

#### Host
This is the DNS name of the site (like 'www.google.com').

#### Port
Servers can open ports to listen to incoming connections. Ports are assigned
a number and can range from 0 to 65535. In general, specific protocols (schemes)
user certain ports by default - the default port for 'http' is 80, while it's
443 for 'https' . In the typical case, specifying the port number isn't necessary
because the 'scheme' value already defines it - https://www.google.com:443 is
equivalent to https://www.google.com .

If the port isn't specified, the ':' character preceding it shouldn't be included.

#### Path
This is the area on a server that should be contacted. It's like the path
of a file within a file system.

#### Query
Like a function can take input variables, a URL can use request parameters
to submit variables in an HTTP request.

Query parameters are listed in '<name>=<value>' pair format with the '&' character
separating each pair.

If no parameters are specified, the '?' character preceding it shouldn't be included.

The '<name>' and '<value>' fields must be encoded as follows -

  - Each space (' ') character should be converted to a '+' character
  - Each other special character (not letter or number) should be replaced with
  the following string -
    - Start with the '%' character followed by its two-digit 'ASCII' code
      - One ASCII Code Table Reference - http://www.asciitable.com/
        - Study the 'Hex' (for hexadecimal) column of this table
    - Note - Sometimes now even the ' ' character follows this convention
    by using '%20' instead of '+'

##### Exercise - Go Straight to Google Search Results

(As of February 2020,) Users can skip the Google home page and just get results
directly from https://www.google.com/search?q=<query> . Using the query
'<name>=<value>' encoding rules specified immediately above, customize this URL
and go straight to the results page.

For example, searching for 'best songs by Hall & Oates' converts to
'best+songs+by+Hall+%26+Oates' which means that the URL should be
https://www.google.com/search?q=best+songs+by+Hall+%26+Oates .

#### Fragment
This is where the browser should scroll to after receiving a page. When this isn't
specified, the browser just scrolls to the top-left-most area of the page.

As an example of its usage, https://html.com/anchors-links/#The_Anchor_Element
will scroll the browser to 'The Anchor Element' section after the page loads. 

If the anchor isn't specified, the '#' character preceding it shouldn't be included.

### HTTP Request

A full single HTTP call consists of one HTTP request from a client to a server
followed by one HTTP response from the server back to the client.

Here are the parts of an HTTP request.

#### Request URL

This is the URL discussed above.

#### Request Method

The method specifies what you want to do at the URL.

In databases, there are four major 'CRUD' operations - Create, Read, Update,
and Delete. With just these four operations, any data can be read and changed.

There are a number of HTTP methods but these ones are the most important
for web development and align with CRUD operations.

  - GET - Get content from a server (e.g. news article, picture). This is the same
  as a Read CRUD operation. For casual web browsing, the vast majority
  of HTTP client requests are GET calls.
  - POST - Create new content on a server. This is a Create CRUD operation.
    - Note that a POST call is often used to execute an action (like submit an order).
  - DELETE - Delete existing content on a server. This is a Delete CRUD operation.
  - PUT - Update existing content on a server. This is an Update CRUD operation.
    - PATCH - Sometimes the content to be updated is very big and instead of
    sending _All_ of the content to a server with just a minor change using a PUT,
    a PATCH allows the caller to send just the change. For instance, an object
    representing a person (e.g. physical characteristics, relatives, job history)
    could be very large but you just want to update the person's data-of-birth.
    In this case, just use a PATCH with the small change (new data-of-birth)
    instead of sending the (very large) person object with a PUT.

Browsers mostly use GET and POST calls. Server-to-server communication is more likely
to also use DELETE, PUT, and PATCH calls.

##### Exercise - Confirm GET Method Used Most of the Time

Open the Google browser, turn on Developer Tools, click the 'Network' tab,
make sure a 'Method' column appears in the table (if it isn't, right-click over
one of the other columns and select 'Method'), then go to a popular web site.
Notice how 'GET' is the method used in each HTTP call (row) the vast majority
of the time.

#### Request Headers

Metadata is data about data. Request headers are key-value pairs telling the server
what kind of data the request is sending and what it expects in the response.

Here are common HTTP request headers.

  - Accept - Tells the server what type of content the client wants from the server.
  Values like 'text/html' and 'application/json' tell the server that the client
  wants HTML and JSON, respectively.
    - Example - `Accept: text/html`
    - These designations are known as `mime types` and popular ones can be found
    at https://en.wikipedia.org/wiki/Media_type#Common_examples .
  - Authorization - Tells the server who you are. Servers obviously often want
  to know who is making the call (`authorization`) and verify that the person
  is authorized to make the call (`access control`). For sensitive information
  (like medical records) and transactions (like money transfers), servers won't
  let just anyone do anything.
    - OAuth2 is a very popular authorization protocol.
    - Example (OAuth2) - `Authorization: Bearer abd90df5f27a7b170cd775abf89d632b350b7c1c9d53e08b340cd9832ce52c2c`
  - Content-Length - If a request body is being sent, this states how big it is.
    - Example - `Content-Length: 348`
  - Content-Type - If a request body is being sent, this states what it is.
  This is the mirror-opposite of the 'Accept' header.
    - Example - `Content-Type: application/json`
  - Cookie - Servers can send information back to the browser which the browser
  is supposed to send back to the server on future requests. This information is
  referred to as a cookie. For instance, if the user sent a previous request
  to a horoscope application that the user had 'Pisces' for a zodiac sign
  (`Cookie: ZodiacSign=Pisces`), then whenever the user went back to that application
  the forecast for Pisces would show up without the user having to reenter his/her
  Zodiac sign again.
    - Note that for more serious applications, servers often send back
    a `session cookie` which is frequently just an alphanumeric string which maps
    to the state of a session (like what's in a user's shopping cart) back
    on the server.
    - Example (Session Cookie) - `Cookie: SESSIONID=298zf09hf012fh2`
      - Here, '298zf09hf012fh2' doesn't mean anything to the browser,
      but the server (like Amazon) could map '298zf09hf012fh2' to a user's shopping
      cart (e.g. 5 books, 1 CD, and a shovel). As the user adds things to the
      shopping cart, the '298zf09hf012fh2' cookie value doesn't change but what
      it maps to in the server's memory does change.
  - User-Agent - This tells the server what actual client is being used, like
  the browser type.
    - Example - `User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36`

##### Exercise - Try to Get Cryptocurrency Account without Authorization

Go to `https://api.coinbase.com/v2/user` either in a browser or with the `curl`
command, but don't send an `Authorization` header (by default, this header
isn't sent). This is equivalent to walking into a bank without any identification.

Here's the `curl` command. If no request method is specified, a GET is assumed.

`curl -v https://api.coinbase.com/v2/user`

Notice that the response contains '401' which is a code for 'Not Authorized'
and the response body (what the server sent back) is as follows.

`{"errors":[{"id":"invalid_token","message":"The access token is invalid"}]}`

##### Exercise - Study Request Headers

Open the Google browser, turn on Developer Tools, click the 'Network' tab,
then go to a popular web site.
Click each row and click the 'Headers' tab for each row, then scroll down
to the 'Request Headers' section and study the request headers sent
with each request.


#### Request Body

HTTP requests can also end with content of any size, like for a file upload
or a large text submission. This section of the HTTP request is called
the request body and is defined by the `Content-Type` and `Content-Length`
HTTP request headers.

While the URL can contain enough information to describe a request,
it has two shortcomings.

  1) Browsers have a maximum limit on URL length (like around 4096 characters).
  2) URLs get stored in logging systems and it's imperative that confidential
  information not be included in a URL.
    - For instance, for an HTTP call that changes a user's password,
    the new password should be sent in the request body, not in the URL.

POST calls generally send information in the request body.

GET calls don't normally send a request body (the URL should contain all
the information about what the client wants to get).

##### Exercise - Simple HTML Post Form

Create an HTML web page (with filename ending in '.html') with the following content.

```
<html>
  <body>
    <h1>Submit Your Favorite Palindrome</h1>
    <form method="POST" action="https://postman-echo.com/post">
      <textarea type="text" name="palindrome">Able was I ere I saw Elba</textarea>
      <input type="submit" name="submit" value="Submit your palindrome" />
    </form>
  </body>
</html>
```

Open this page while also turning on Google Developer Tools. Click the
'Submit your palindrome' button, then click the entry in the 'Network' tab,
then click the 'Headers' tab. Scroll down to the 'Form Data' section and click
'view source' and notice that the content is as follows (and that it doesn't
appear in the URL and is 66 characters in length).

`palindrome=Able+was+I+ere+I+saw+Elba&submit=Submit+your+palindrome`

Scroll up to the 'Request Headers' section and note headers `Content-Length: 66`
and `Content-Type: application/x-www-form-urlencoded`
('application/x-www-form-urlencoded' means that parameters are encoded
just as they would be if they were in a URL - like `&` is used to separate
parameters and `+` is used to replace the ` ` character).

##### Exercise - Setting and Sending Cookies

1) In Chrome with Google Developer Tools turned on,
go to https://postman-echo.com/cookies . Note how no 'favoriteCookie'
value is sent in the 'cookie' request header.
2) Go to https://postman-echo.com/cookies/set?favoriteColor=green .
Note how the response contains `set-cookie: favoriteColor=green; Path=/` .
This sets a cookie with name 'favoriteColor' gets 'green' for a value.
This cookie will be sent in future requests to all ('Path=/') locations
of https://postman-echo.com .
3) Go back to https://postman-echo.com/cookies and notice how 'favoriteColor=green;'
is part of the value of the 'cookie' request header.

### HTTP Response

Here are the parts of an HTTP response.

#### Response Code

The server sends back a number ranging from 100 to 499 with its response indicating
how successful the server was at processing the client's request. For typical
browser client requests (especially GET calls), 200 (with the official description
of 'OK') is the most common response code and it means that the server was
successful in processing the client's request. Beyond GETting content, 200 is
a common response code for POST actions (like submitting an order).

##### Exercise - Verify 200 Is a Very Common Response Code

Open Chrome Developer Tools then go to a popular web site. Study the 'Status'
column under the 'Network' tab and notice that 200 is the most common value.

##### 100-199 Information Response Codes

These aren't used much.

##### 200-299 Success Response Codes

Codes from 200-299 indicate success.

###### 200 OK

Again, this is the most common response. For GET calls, the response body
(referenced below) contains the information (like an HTML page) that
the client (browser) was trying to GET.

###### 201 Created

For calls (typically POST calls) that create something (like a new user account),
this response code can be sent back.

###### 202 Accepted

For calls that have been accepted for processing, but can't be processed immediately,
this response code can be sent back.

For instance, a POST call is made to upload an application form on a Sunday evening.
The application is a request to reserve space in a public park for a picnic.
The town council reviews this type of application on Wednesdays. Therefore,
the server can't immediately determine whether this request is ultimately successful.
Therefore, the server can accept the request by saving the application into
a database and return this response code.

###### 204 No Content

Some calls, like DELETE calls, create a situation where there's nothing to return
back to the client. This response code is used for this situation.

##### 300-399 Redirect Response Codes

Codes from 300-399 indicate that the server isn't sending back content, usually
because the server is instructing the client (browser) to go to another URL.
For redirects, the server will send back a 'Location' response header indicating
where the browser should go next.

###### Exercise - Use the Wrong Protocol to Contact Google

As discussed above, HTTPS is the secure (encrypted) version of HTTP.
Many web sites prefer that client requests use HTTPS and will forward HTTP requests
to the HTTPS version of the URL.

Open a browser with Google Developer Tools turned on and the 'Network' tab selected.
Go to 'http://www.google.com' (HTTP) and notice that the browser ends up at
'https://www.google.com' (HTTPS). Study the first entry in the 'Network' tab
and notice that a 307 ('Temporary Redirect') HTTP status code was returned.
Also notice that the response contains a 'Location' header with
'https://www.google.com' for a value.

##### 400-499 Client Error Response Codes

Codes from 400-499 indicate that the server has included that the client's
HTTP request was somehow invalid ("It's the client's fault").

###### 400 Bad Request

This means that the client send invalid information. For instance for a banking
application, if someone attempts to withdraw 'Alligator' dollars, then the server
would (rightly) conclude that the submission was bad request.

###### 401 Unauthorized
The client has attempted to do something without proper identification.
This is like walking into a bank and trying to withdraw money from a bank account
without showing any identification (the bank would reject you).

###### 403 Forbidden
The client has properly authenticated itself (like with an OAuth2 token in the
'Authorization' request header), but the client isn't authorized to do
the action it requests. This is like walking into a bank with a valid driver's
license and asking to withdrawal money from another person's account.
The server doesn't disagree with the client's identification but the server
concludes that the client doesn't have the right to perform the requested action.

###### 404 Not Found
The client has made a request for something that isn't on the server.

####### Exercise - Go to a URL that a Server Doesn't Support

With Google Developer Tools open with the 'Network' tab selected, go to
https://www.google.com/NoContentHere and confirm that an 404 appears under
the 'Status' bar of the first row.

##### 500-599 Server Error Response Codes

Codes from 500-599 indicate that the server has encountered an unexpected
problem ("It's the servers's fault"). These codes usually result from problems
like a bug in the software or failure to contact a backend system.

###### 500 Internal Server Error
The server encountered an unexpected problem.

#### Response Headers
Just as an HTTP request can send headers, headers can be included in the response too.

##### Set-Cookie
Sets a cookie on the browser.

##### Content-Length
Specifies the size (in bytes) of the content in the response body.

##### Content-Type
Specifies the (mime) type of the content in the response body.

##### Location
This is often used for redirecting the browser. It can also be used to indicate
the location of a newly-created entity (like in a response to a POST call
to create a bank account, the 'Location' header value could be something like
'https://somebank/youraccount/1269835740' ).

#### Response Body
This is the main content returned to the client.

### Browser HTTP Communication

Browsers use HTTP communicate with servers.

#### Normal Communication

##### Address Bar

Browsers normally communicate with servers by downloading whatever is entered
into the address bar. If an HTML page is downloaded and it references other
things (like images, CSS, JavaScript, and other HTML pages ('iframes')), then
subsequent HTTP calls will be made to get those things too.

URLs entered into the browser address bar use the GET method.

###### Exercise - Favicons

When a browser goes to a new web site, it can (and often does) check whether
an image for that site is available. This image is often placed aside a site's
title in its tab in the browser. The downloaded HTML page can specify
the location of the image or the browser can just make an extra call
to the '/favicon.ico' location of the web site to try to get to this image.

Go to https://www.google.com/favicon.ico and confirm that it's the image
that appears in the tab when just going to https://www.google.com .

##### Hyperlinks
Clicking a hyperlink is generally just the same as entering in the hyperlink's URL
into the browser address bar. Likewise, it too uses a GET method.

Hyperlinks can also trigger JavaScript instead of going to a new web page.

##### Forms
HTML form construct a URL to send based on the user's input into the form.
Unlike the address bar and hyperlinks, forms have the option of submitting requests
using either a GET or a POST method.

#### AJAX Communication

AJAX stands for Asynchronous JavaScript and XML, but (in most cases)
what it's really just JavaScript making JSON-based HTTP calls.

_This is how a web page is able to constantly update itself without completely
reloading._

jQuery and other libraries make these calls possible.

Here is an example.

```
<html>
  <head>
    <script src="https://code.jquery.com/jquery-3.4.1.min.js" ></script>
    <script>
      //in jQuery, the '$' character represents the library
      //  the 'ready' function is a special (and cross-browser compatible)
      //  function that runs as soon as the web page is 'loaded enough'
      //  to allow DOM manipulation so that the user gets the finalized
      //  look of the web page as quickly as possible
      $(document).ready(function() {

        setTimeout(
          function() {
            $.get(
              {
                url: "https://jsonplaceholder.typicode.com/todos/1",
                success: function(data, status) {
                  console.log(JSON.stringify(data));
                  $("#title").val(data.title);
                }
              }
            );
          },
          3000);
      });
    </script>
  </head>
  <body>
    Title - <input type="text" id="title" />
  </body>
</html>
```

The `https://jsonplaceholder.typicode.com/todos/1` URL responds with a JSON object
as follows.

```
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

Here are key observations.

  - _script src=".../jquery-3.4.1.min.js"_ - This is a very popular (though less
  popular lately) JavaScript library called jQuery. It creates a variable `$`
  which makes it much easier to make AJAX HTTP calls and interact with the web page.
  - _$(document).ready(...)_ - Wait for the page to load and then execute whatever's
  inside the `ready` function. Note - when web pages load, anytime the page encounters
  JavaScript, the JavaScript must first be processed before the page continues loading.
  The 'ready' function allows the page to load before executing an action.
  - _setTimeout(...)_ - This executes a function after the submitted number
  of milliseconds (3000 in this case, which equals 3 seconds).
  - _$.get(...)_ - jQuery makes an HTTP GET call to the `url` value and then
  executes the function in the `success` value once a successful
  (usually HTTP 200 status code) response is received. Note - For JavaScript on a
  web page, the double quotes for a JSON key value are optional, so `url` is the same
  as `"url"` and `success` is the same as `"success"`.
  - _JSON.stringify(data)_ - Converts variable `data` from a JSON object to a string.
  For some browsers, strings print out in a more easy-to-understand way than JSON.
  - _console.log(...)_ - Prints a message to the `Console` tab of Chrome Developer
  Tools (or analogous debug console in another browser's developer tools).
  - _$("#title").val(data.title)_ - jQuery gets (`$("#title")`) the HTML element
  for the DOM object have `title` value for its `id` attribute (which in this case
  is a text box). jQuery then sets (`val(data.title)`) the value of this object
  to be the `title` field's value of the object returned by the AJAX call.

##### Exercise - Type into the Google Search Box

Go to https://www.google.com and start typing into the search box. Notice
how the URL in the address bar (it's still https://www.google.com ) does not change
even as you type your entry in and Google provides suggestions. Google is making
AJAX calls as you type to get those suggestions. It would be a much worse user
experience for Google to completely reload the browser as you typed to download
those suggestions. AJAX calls enable a much smoother web-browsing experience.

##### CORS
CORS stands for Cross-Origin Resource Sharing and it's a way of sharing JavaScript
and allowing AJAX calls between different web domains. For security reasons,
browsers normally prevent a web site from one domain (like 'www.google.com')
to make AJAX calls to another domain (like 'www.yahoo.com').

CORS is an approach the browser takes where it first asks the other domain if
AJAX calls from the original domain are allowed. If so, the AJAX call goes through,
but otherwise it's blocked.

##### Sample Vendor APIs

Popular web sites publish AJAX-based JSON APIs that allow a web application
to dynamically interact with these web sites. Here are some examples.

  - Twitter - https://developer.twitter.com/en/docs/api-reference-index
  - Facebook - https://developers.facebook.com/docs/graph-api/reference/user/
