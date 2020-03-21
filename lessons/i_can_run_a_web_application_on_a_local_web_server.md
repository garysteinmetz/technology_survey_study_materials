
# I Can Run a Web Application on a Local Web Server

## Servers

Servers ... serve things. Clients ask servers for the things.

In the context of the internet and specifically the HTTP protocol,
the client (like a web browser) makes requests to servers and servers respond
with responses.

Whether something acts as a client or a server really depends on the situation.
A web browser is always a client because it's always making requests. Servers
are obviously servers when responding to clients (like browsers), but servers
act as clients when those servers call other servers to get information.
Servers acting as both servers and clients are called `middle-tier servers`
(because they are in the middle!).

So, for instance, if a browser calls a bank's web server and that server in turn
calls a backend database holding bank account information, that web server (A)
is a server to the browser but (B) is a client to the backend database.

## Server-Side JavaScript (Node.js)

Use of JavaScript within a web browser is well known, but it can also be used
to run a server. `Node.js` runs JavaScript outside of the browser and often
runs JavaScript server programs.

### Download Node.js

Go to https://nodejs.org/en/download/ and download the 'Binary' (not the 'Installer').
For Windows, that will be 'Windows Binary (.zip)' (64-bit). For Mac, that will be
'macOS Binary (.tar.gz)' (64-bit).

Unzip the download onto your desktop. The directory name will be something like
'node-v12.16.1-darwin-x64' .

The 'Installer' is actually better for longer-term development, but mildly harder
to uninstall, with the 'Binary' you just delete the directory to uninstall it.

#### Run a Simple Node.js Program

Open a text editor and save file having name ending in '.js' (like 'sample11.js')
with the following content.

```
console.log('Hello World!');
```

Now, from the command line, run this program by typing the location of the Node.js
executable file (`node` which is in the 'bin' subdirectory of the Node.js directory)
followed by the name of the Node.js file you just created. Here's an example.

```
~/Desktop/node-v12.16.1-darwin-x64/bin/node sample11.js
```

It should print the following (just like it does in the 'Console' tab of Chrome
Developer Tools in a Chrome browser).

```
Hello World!
```

### NPM

#### Cowboy Coding

_How are software projects organized in a familiar way that keep them manageable
and approachable by new team members?_

When your working on a project by yourself, there are no rules or expectations
from others as to how you should organize your software project. You can do whatever
you want! Coding your project however you like without respect to established
standards and frameworks is called `cowboy coding`.

But the reality of software is that it's often very complex and economically
important that (A) new team members can be productive quickly and (B) projects
can easily interact with other libraries, tools, and frameworks to make progress
sooner (not `reinvent the wheel`).

Projects are expected to have specific layouts that are ubiquitously recognizable.
For JavaScript, that specific layout is defined by the `NPM` (Node Package Manager)
tool.

_Software development is often associated with creativity and independence
in popular culture, but the reality of typical software development is that it's
most often disciplined and regimented._

#### Exercise - Create a NPM Project

From the desktop, create a subdirectory (with name like 'sampleNode1')
and using the command line go into it.

The `npm` tool is in the same directory as the `node` program. Run `npm` followed
by the word `init` to initialize the project structure. Here's an example.

```
~/Desktop/node-v12.16.1-darwin-x64/bin/npm init
```

Keep pressing the enter or return key to accept the default value for all of the
different options (like 'package name', 'entry point', and 'license').

All of these steps did was create a single file ('package.json') which describes
your project. This file describes the project and provides a standardized way
of listing its characteristics (like what libraries it uses, thought it isn't
using any libraries right now). Here is an example of its contents.

```
{
  "name": "samplenode1",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

#### Exercise - Create a Hi World Program within This NPM Project

Notice the 'scripts' attribute in the 'package.json' file, it lists the possible
commands that can be run with NPM's `run` command. In this base 'package.json' file,
only the 'test' command is available and all it does is ... print and error message
stating that there are no tests to run!

```
~/Desktop/node-v12.16.1-darwin-x64/bin/npm run test
```

The output is 'Error: no test specified' - note that in this case `test` is
defined as `echo "Error: no test specified" && exit 1` which means that it will
print 'Error: no test specified' _and_ (`&&`) then stop (`exit 1` - 1 means exit
signaling to the command line that an error occurred (0 means no error occurred)).

In 'package.json' create a line above that 'test' entry as follows.

```
    "start": "node index.js",
```

Then create 'index.js' in the same directory with the following content.

```
console.log('Hi World!');
```

Then run the following command which should output ... 'Hi World!'

## Java

_Note - For most aspects of web development (e.g. programming languages, build tools,
project management software, libraries), there are multiple competing solutions
and software engineers are often expected to know more than one solution for a given
area (e.g. programming language), even on the same software project!_

Java has been in use since the late 1990s. A big complaint about it is that
it requires `too much ceremony` (too much typing and many formalities to get
anything done), but it's widely used (which also makes it easier to hire someone
with that skill set), many existing applications have been built with it (has a large
`installed base`), it has a large amount of tools and features, and all the 'ceremony'
allows a software project to be better managed as it gets bigger.

### Spring Boot
