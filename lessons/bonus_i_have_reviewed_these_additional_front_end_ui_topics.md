
# Bonus: I Have Reviewed These Additional Front-End UI Topics

In software, it generally isn't good enough to get just
a basic web application to work (sometimes this is called
the 'happy path'). Covering additional features, like
having a high index on a search engine, retaining customer settings,
creating a better user experience for those with disabilities,
and supporting non-native (e.g. non-English) language experiences,
are critical to truly qualifying an application as being ready
for general public and commercial use.

## Mobile Application Development

Of course, end users don't just use a web browser to interact
with servers.

While command-line tools and software API calls can also be used
by a (technically advanced) end user to communicate with a server,
they generally use mobile applications in addition to using
web browsers.

A mobile application is an application that is downloaded
and installed as software to the cell phone.

While a company will often support _both_ web and mobile versions
for its major software application, it will support at least one.

Mobile applications have key advantages over regular web applications
in that they can more easily integrate with features of a cell
phone, like its location (GPS) and camera.

### Native Mobile Apps

Developers of native mobile apps use platform-specific languages -
like Objective C and Swift for iPhones and (historically) Java
for Android - to build them.

### Hybrid Mobile Apps

Hybrid mobile applications are mobile applications that are
created with standard web technologies - like HTML, CSS, and
JavaScript. Like native mobile apps, they can easily integrate
with cell phone features.

They have the advantages and disadvantage of using "one size
fits all" technologies (HTML, CSS, and JavaScript). Advantages
include using the same technologies and maybe the same source code
repository for all flavors of the application. Disadvantages include
trying to 'shoehorn' the application to accommodate all client types
(i.e. Android, iPhone, browser) and not taking advantage of the
better stylized UI experience available to native mobile apps.

`Apache Cordova` is software used for converting web apps into
mobile apps.

## Web Page Optimization

Web developers, content managers, and product managers spend a lot
of time to ensure that (A) the web application can easily be
discovered in a web search and (B) the web application efficiently
(quickly) renders and updates.

### SEO

Search engine optimization (SEO) is the attempt to improve
the likelihood that a web site will be listed at the top of a search.
Improving a web application's listing in search results is a great
way to increase the popularity of a web application.

While search engines (like Google) don't reveal all the details
of how they curate search results, here are well-known methods
for attempting to improve the searchability of a web application.

1) Explicitly include words in the URL that accurately represent
the purpose of the web page. For a department store,
getting a higher profile for a 'buy books' search is probably easier
for the URL like `https://somestore.com/books` than
`https://somestore.com/asdabdaosbdoa`
2) Correctly describing the purpose of the web page in its HTML,
including in 'title' and 'meta' tags
3) Having quick load times, employing a responsive web design,
and avoid inclusion of annoying ads

#### 'robots.txt'

The 'robots.txt' file informs a search engine which files
on a web site should not be scanned
(e.g. `https://www.google.com/robots.txt`) by a search engine.

#### 'sitemap.xml'

The 'sitemap.xml' file informs a search engine which file
on a web site are important and should be given priority
(e.g. `https://www.ford.com/sitemap.xml` and
`https://www.bbc.com/sitemap.xml`).

### Page-Load Times

There are (free) products, like `http://yslow.org/`, which can
be used to investigate ways to improve a page's speed. Here are
common recommendations.

1) Condense images into one composite image and then use CSS
to determine which sub-image is selected from the composite image
for a specific component on the HTML page. When the web page reduces
the number of server calls it needs to get things (like images),
the web page renders more quickly.
2) Reduce the size of the files downloaded by the HTML page,
especially JavaScript files. For instance, 'var bankBalance'
can be renamed 'var bb' .
3) Put JavaScript at the bottom of a web page. When JavaScript
is encountered, the web page will stop processing the web page
until the JavaScript is executed. Displaying the full page first
allows the user view it without more delays.

### Accessibility

### Cookies

Cookies are pieces of information stored in a browser when a web page
is visited. Normally, when a browser returns to a web site, the browser
has no memory of the past visit, but cookies allow a browser (and a server)
to know that it has been to the same web site before.

There are two types of cookies - session cookies and persistent cookies.
Session cookies last last long as the browser is open and are useful
for storing things like a login session. Persistent cookies have a fixed
time assigned to them (quite often several days or longer in the future)
and are useful for saving user settings on a web page without a formal login.

Cookies can be set both within the web page (meta tag and JavaScript)
and also in the server's HTTP response which delivers the HTML
that the browser uses to render the web page.

#### Exercise - Server-Generated Persistent Cookie

Create a file named 'server.js' with the contents below. Then start the server
with command `node server.js` . Then open a browser, go to `http://localhost:2080`,
then repeatedly click the 'Check Cookie Status' button for about 25 seconds and note how
the cookie expires after 20 seconds.

##### 'server.js'

```
var webpage = `
<html>
  <head>
    <script src="https://cdn.jsdelivr.net/npm/js-cookie@rc/dist/js.cookie.min.js"></script>
    <script>
      var pageLoadTime = new Date();
      function checkCookieStatus() {
        document.getElementById('pageLoadTime').value = pageLoadTime;
        document.getElementById('currentTime').value = new Date();
        var yumCookieValue = Cookies.get('yumCookie');
        if (yumCookieValue) {
          document.getElementById('yumCookieStatus').value =
            "'yumCookie' has a value of '" + yumCookieValue + "'";
        } else {
          document.getElementById('yumCookieStatus').value = "'yumCookie' cookie has expired";
        }
      }
    </script>
  </head>
  <body>
    <input type="button" value="Check Cookie Status" onclick="checkCookieStatus()"/>
    <br />
    The cookie should expire 20 seconds after page load time
    <br />
    Page Load Time - <input type="text" size="50" id="pageLoadTime" />
    <br />
    Current Time - <input type="text" size="50" id="currentTime" />
    <br />
    Status of 'yumCookie' Cookie - <input type="text" size="50" id="yumCookieStatus" />
  </body>
</html>
`;

var http = require('http');
http.createServer(function(request, response) {
  response.writeHead(200, {
    'Set-Cookie': 'yumCookie=tasty; Max-Age=20',
    'Content-Type': 'text/html'
  });
  response.end(webpage);
}).listen(2080);
```

#### Exercise - Client-Generated Session Cookie

Create a file named 'client.js' with the contents below. Then start the server
with command `node client.js` . Then open a browser, go to `http://localhost:3080`,
then click the 'Eat a Cookie' button once and note how the 'Cookies Left' value
drops to '7' . Then open another browser tab and note that '7' is still the value
on that version of the web page - the 'state' (value) of the 'cookieJar' cookie is
known by the new browser tab even though it didn't directly interact with the
original browser tab.

Note that if you click the 'Eat a Cookie' button in one tab then switch to the other
tab and click the same button, the correct cookie count will then appear on the
other tab.

To reset the cookie count back to 8, completely shutdown the browser software
(this will close all tabs) then restart it and go back to the page.

_It's important to note that a client sends any unexpired cookies back to the server
whenever it calls the server._ In this example, repeat calls from the browser
print a "Great, you already have a cookie jar" message on the server's console.

Also note that it's the browser that determines whether cookies are sent. If the
server is rebooted, but the browser had cookies for the server before reboot,
then the browser will send those same cookies back to the server if the browser
contacts the server after it has been rebooted.

##### 'client.js'

```
var webpage = `
<html>
  <head>
    <script src="https://cdn.jsdelivr.net/npm/js-cookie@rc/dist/js.cookie.min.js"></script>
    <script>
      if (!Cookies.get('cookieJar')) {
        Cookies.set('cookieJar', '8');
      }
      function eatCookie() {
        var cookiesRemaining = parseInt(Cookies.get('cookieJar'));
        cookiesRemaining = cookiesRemaining - 1;
        Cookies.set('cookieJar', cookiesRemaining);
        document.getElementById('cookiesInCookieJar').value = cookiesRemaining;
      }
    </script>
  </head>
  <body>
    <input type="button" value="Eat a Cookie" onclick="eatCookie()"/>
    <br />
    The number of cookies in the cookie jar does not get reset until browser software is restarted
    <br />
    But opening an 'Incognito' (Chrome) or 'Private' (Safari) browser window will reset
    the cookies for that browser tab
    <br />
    Cookies Left - <input type="text" size="50" id="cookiesInCookieJar" />
    <script>
      var cookiesLeft = Cookies.get('cookieJar');
      document.getElementById('cookiesInCookieJar').value = cookiesLeft;
    </script>
  </body>
</html>
`;

var http = require('http');
http.createServer(function(request, response) {
  if (request.headers.cookie) {
    console.log("Great, you already have a cookie jar - " + request.headers.cookie);
  }
  response.writeHead(200, {
    'Content-Type': 'text/html'
  });
  response.end(webpage);
}).listen(3080);
```

##### Incognito Mode

Browsers support tabs that are 'incognito' (or 'private'). These browser tabs don't inherit
the cookie settings of the main set of browser tabs.

Open an 'Incognito' (Chrome) or 'Private' (Safari) browser window and confirm that
'8' is the number of cookies in the cookie jar.

##### Browser Fingerprinting

Servers often use cookies to track whether the browser has previously accessed the server
(like whether the user has logged in at a previous web page on the site).

But even when a browser is in 'incognito' mode, a sophisticated server can reasonably guess
whether the same kind of browser (e.g. Chrome, IE) had been used on a computer recently.
The server does this by tracking things like originating IP address, request headers,
JavaScript settings (which can vary by browser installation), and timezone.

As an analogy, consider a bespectacled 6-foot man who walks into a convenience store carrying
a pink briefcase wearing a Fedora hat, polka-dotted tie, and wooden shoes. As the cashier,
you closely observe the man's face as your enter his credit card information to complete
his purchase.

The next day is your off day but your coworker who is working calls you to tell you
about someone with the same characteristics who just entered the store, but the coworker
doesn't describe the person's face (which in this case is the unique identifier, like a
cookie). In this situation, you probably the this man's credit card information.

###### Exercise - Browser Fingerprinting

Go to https://amiunique.org/fp , then go to the same page in an incognito tab.
Compare the same information between the tabs.

## Common Files in 'npm' Projects

These are some files frequently found in NPM projects. Note that
UI technologies rapidly evolve and new frameworks frequently
come out which quickly obsolete existing technologies.

### 'package.json'

This is the _main_ file defining the project. It usually contains
the project's name and description, it may contain as 'scripts'
section which list the commands that can be run in the form
'npm run <command>' - command commands include building a JavaScript
file for production ('real world') cases, running (unit) tests
against the source code, and running a local server (to verify
changes on one's own computer).

### 'node_modules'

This isn't actually a file, but a directory that gets populated
by the libraries listed under the 'dependencies' and 'devDependencies'
(and even others like 'peerDependencies') sections of the
`package.json` file when running the `npm install` command.
Developers often this command first before continuing work to get
the latest versions of libraries.

Files in this directory should _not_ be stored in source control.

### Polyfills

Polyfills aren't required in a project but are often present.
Sometimes browser type A will support a new feature (like native 'Promises')
while browser type B doesn't, but the programmer wants to create
an application that assumes the new feature exists. Pollyfills are
JavaScript files that are bundled into the application that activate
to support a normally unsupported feature of the browser.

### 'tsconfig.json'

'tsconfig.json' is a file that determines _how_ TypeScript,
a computer language that unlike JavaScript supports type casting
(e.g. 'var bankBalance = "giraffe"' is (rightly) prohibited)
and object-oriented features.

### Babel

Babel is a tool that's like the reverse of a polyfill, it converts
newer JavaScript features to more basic but widely supported JavaScript.
As an analogy, Babel converts '5*3' to '5 + 5 + 5' for browsers that
don't support multiplication.

### LESS and Sass

LESS and Sass are somewhat like Babel, but for CSS. These tools add
features that CSS should support to CSS files that are then processed
by these tools to create final CSS files.

### Mocha and Jasmine

Mocha and Jasmine are (unit) testing frameworks for individually
testing different sections of JavaScript. Running these tests helps
ensure that the JavaScript written works correctly before it's
published.

Reference - https://mochajs.org/
Reference - https://jasmine.github.io/2.1/introduction

#### Chai

Chai is an add-on framework where much of each test is framed as
a natural language statement (e.g. "The 'add' function will return 10
when 4 and 6 are submitted to it"). It generates a user-friendly
report that's easy to interpret.

Reference - https://www.chaijs.com/guide/styles/

### Webpack

Webpack (and other tools like it) is responsible for assembling
('building') the various components of a project into ready-to-use
outputs.

Reference - https://webpack.js.org/configuration/

## Internationalization

Web sites commonly support languages beyond English.

### It All Comes Down to Bytes

A byte is a number from 0 to 255, inclusive. Servers send a sequence ('stream')
of bytes to a client (e.g. browser) when the client requests information
(like loading a web page into a browser).

For web browsers, each of these bytes is like syllables in a word.

### The Meaning of 'Hi'

If you were walking down a street in New York City and
someone spoke a word that sounded like 'hi', you could be confident
that someone was greeting you or another person. But what instead if
you were walking down a street in Tokyo?

The Japanese word for the English word 'yes' sounds very much like 'hi',
but you'd be confident that someone was saying 'yes' .

Likewise, browsers can conclude (guess) the character set (like the Latin
alphabet used for English) by understanding context - if a browser in
the United States calls an English-language web site (like the BBC), the
browser could likely conclude that the Latin alphabet is being used unless
the server explicitly stated that another character set (like simplified
Chinese) was being used.

For instance, if someone on a street in Japan said 'I speak English. Hi.',
you could be confident that the 'Hi.' was a greeting, not 'yes'. Likewise,
web pages and servers can explicitly state which language character set
is being used.

#### Exercise - Listen to the Japanese Word for 'Yes' Be Spoken

Go to `https://translate.google.com/`, select 'English' as the source
language, 'Japanese' as the translation language, and enter 'Yes' as the
word to translate. Then click the volume icon for the translated word.

### Character Sets

Just like the sound of 'hi' can mean one word or another _or even_
just one syllable of a multi-syllabic word, bytes can represent one
character or another _or even_ just one byte of a multi-byte character
in an HTML file.

The _character set_ assigned to a web page determines how individual
bytes and groupings of bytes are converted into the characters
(like '<', '/', 'a', '5', '?') which together constitute an HTML page.

#### Popular Character Sets

They are many different character sets, but here are some of the most
popular.

  - ASCII - This character set was the first major one to be introduced.
  The traditional part of this character set only has character assignments
  for byte values 0 through 127. Most traditional characters on an American
  keyboard (like 'a', 'Z', and '%') have corresponding numbers in ASCII.
  - ISO-8859-1 - Extends ASCII by assigning values 128 to 255 with other
  characters, many of them non-English alphabet letters found in other
  European languages (like 'ñ' from the Spanish alphabet).
  - UTF-8 - This is the main character set for internet text communication.
  As of 2021, this is the most popular character encoding for major web
  sites and the default character set for important internet standards
  (like URLs). Each character uses between one and four bytes, with ASCII
  characters keeping their original values and only using a single byte each.
  All of the alphabets ('scripts') of the major world languages, including
  Chinese, are supported.
  - GB2312 - This is the official character set of the Chinese government.

##### Exercise - Create HTML Pages in ISO-8859-1 and UTF-8

This exercise can only be done on a Mac or Linux system.

The `printf` command is a way of formatting a string. With it, numbers
and others strings can be inserted into a template string. Here's an example
using decimal ('floating point') formatting which prints the first four
decimals ('%.4f') of Pi (rounded up - so 3.1416) followed by a new line ('\n')
- this will print 'Pi is approximately 3.1416' .

```
printf "Pi is approximately %.4f\n" "3.141592653589793"
```

The '>' character can be used at the end of a command to redirect output
from the console (terminal) to a file. If the file exists already, it will be
overwritten.

The `charset` attribute of the HTML `meta` tag can inform the browser which
character set is being used on an HTML page.

Create file 'happynewyear.html' with the following command then open the file
with a browser. These UTF-8 (hexadecimal) codes correspond to three symbols
('glyphs') in simplified Chinese to state 'happy new year'. The '\x' directive
of 'printf' inserts a byte into the string (and two hexadecimal digits
correspond to one byte).

  - e8bf87
  - e5a5bd
  - e5b9b4

```
printf "<html><head><meta charset=\"utf-8\" /></head><body>\xe8\xbf\x87\xe5\xa5\xbd\xe5\xb9\xb4</body></html>" > happynewyear.html
```

Create and open file 'confusednewyear.html' with the following command which
substitutes out 'utf-8' for 'iso-8859-1', which doesn't support simplified
Chinese characters.

```
printf "<html><head><meta charset=\"iso-8859-1\" /></head><body>\xe8\xbf\x87\xe5\xa5\xbd\xe5\xb9\xb4</body></html>" > confusednewyear.html
```



Character encodings extend beyond internet communication
echo ${LANG}
iconv -l

https://www.google.cn - character encoding
https://www.w3schools.com/html/html_charset.asp

'printf' unix command

https://www.w3.org/International/questions/qa-html-encoding-declarations

dingbats


### Character Encoding Set By Server

### Unicode


## Content Management Systems

Corporations generally don't allow individual projects to store media
content like images, videos, and CSS files. Likewise, they tend to issue
standard JavaScript files that development teams are supposed to use.

Corporation store these files in `Content Management Systems` (CMS)
which is like Git but more user-friendly, is meant to store media content,
and supports 'workflow' capabilities (e.g. both an author's manager
and someone from corporate branding have to approve an image before
it is published).

## Promises

## Web Frameworks

SPA - web page doesn't reload as the user uses it

Vue
