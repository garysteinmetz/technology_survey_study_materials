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

//Next
  - Static Content Versus Dynamic Content
  - CRUD Operation
  - HTTP (Response Codes, Request Parameters, Request/Response Body, Request/Response Headers, Request Method)
  - REST Standards Not Enforced
  - Form Submission
  - Forms Versus Ajax
  - Vendor APIs


Show examples of different web service APIs (Twitter, Coinbase)
