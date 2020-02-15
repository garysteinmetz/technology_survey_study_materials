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

//



Web browsers are just like 'curl' command but they are much better able
to represent server responses in a human-friendly format and transform user
requests back to the server.

Port numbers

Chrome tools

AJAX call

CORS

//Next
  - Static Content Versus Dynamic Content
  - CRUD Operation
  - HTTP (Response Codes, Request Parameters, Request/Response Body, Request/Response Headers, Request Method)
  - REST Standards Not Enforced
  - Form Submission
  - Forms Versus Ajax
  - Vendor APIs


Show examples of different web service APIs (Twitter, Coinbase)

Redirect example with http://www.google.com

https://docs.postman-echo.com/?version=latest
