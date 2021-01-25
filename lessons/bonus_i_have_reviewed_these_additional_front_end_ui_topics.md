
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

Cookies can be set both within the web page (meta tag and JavaScript)
and also in the server's HTTP response which delivers the HTML
that the browser uses to render the web page.

#### Incognito Mode

##### Browser Fingerprinting


## Internationalization

## Content Management Systems

## Web Frameworks

SPA - web page doesn't reload as the user uses it

Vue
