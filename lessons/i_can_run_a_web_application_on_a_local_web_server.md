
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

1) _Skip this step if you are not using Windows. If you have trouble
with this section, just assume your Windows system is 64-bit and continue
to the next section._ Click the Windows (group of four squares) icon
on the lower-left of your desktop, click the gear icon for 'Settings',
on the left scroll down and click the 'About' link, look
under 'Device specifications' and determine whether 32-bit or 64-bit
appears under 'System type' .
2) Go to https://nodejs.org/en/download/ and download the 'Installer'
(not the 'Binary'). For Windows, that will be 'Windows Installer (.msi)'
(64-bit or 32-bit, depending on what you recorded in the previous step).
For Mac, that will be 'macOS Installer (.pkg)' (64-bit).
3) Run this downloaded file, accept all the default settings
(click the 'Next >' buttons), agree to the license terms, continue to accept
all the default settings, and if Windows prompts you to agree to install
the software click the 'Yes' button.

#### Run a Simple Node.js Program

Create a file having name ending in '.js' (like 'sample11.js').

For Windows, open the text editor for this file with the following steps.

1) Open a command prompt.
2) Type command `cd %HOMEPATH%\Desktop` .
3) Type command `notepad sample11.js` .

Place the following content in file, save it, then close the text editor.

```
console.log('Hello World!');
```

Now, from the command line, run this program by typing `node`
followed by the name of the Node.js file you just created.
Here's an example for Windows.

```
cd %HOMEPATH%\Desktop
node sample11.js
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
and using the command line go into it. Then run `npm init` to initialize
the project structure. In Windows, all this can be done with the following steps.

```
mkdir %HOMEPATH%\Desktop\sampleNode1
cd %HOMEPATH%\Desktop\sampleNode1
npm init
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

On Windows command line, this file can be viewed by entering either
`notepad package.json` or just `type package.json`.

#### Exercise - Create a Hi World Program within This NPM Project

Notice the 'scripts' attribute in the 'package.json' file, it lists the possible
commands that can be run with NPM's `run` command. In this base 'package.json' file,
only the 'test' command is available and all it does is ... print and error message
stating that there are no tests to run!

```
npm run test
```

The output is 'Error: no test specified' - note that in this case `test` is
defined as `echo "Error: no test specified" && exit 1` which means that it will
print `Error: no test specified` _and_ (`&&`) then stop (`exit 1` - 1 means exit
signaling to the command line that an error occurred (0 means no error occurred)).

Note that the `test` command here represents something important - well-organized
projects include additional code to test the application code that has been written!
`Mocha`, `Jasmine`, and `Karma` are popular Node.js test frameworks.
Tests come in different forms.

  - `Unit Tests` - Check select portions of code
  - `Live Tests` - Check the software application as it runs
  - `Load Tests` - Stress (apply many calls to) the software application as it runs

In 'package.json' create a line above that 'test' entry as follows.
(For Windows, this file can be opened with a text editor with command
`notepad package.json` .)

```
    "start": "node index.js",
```

Then create 'index.js' in the same directory with the following content.
(For Windows, this file can be opened with a text editor with command
`notepad index.js` .)

```
console.log('Hi World!');
```

Then run the command `npm run start` which should output ... 'Hi World!'

#### Exercise - Download Web Server Library

NPM has the `install` command which can be used to download libraries
and (optionally) formally declare in the 'package.json' file that the Node.js
('Node' for short) application uses the library.

`express` is a simple Node.js library used for hosting web servers. The following
command downloads that library into the standard library subdirectory ('node_modules')
and (using the `--save` option) formally declares that this project needs that library
in the 'package.json' file.

```
npm install express --save
```

The 'package.json' file will now have this entry.

```
  "dependencies": {
    "express": "^4.17.1"
  }
```

This means to download version '4.17.1' (or greater, because the optional
'^' character is present) of the 'express' library.

Note that there is an associated 'package-lock.json' file too. This locks the version
of libraries so that '^' character doesn't change the library version between what's
deployed, in a team developer's environment (like `stage`), and what's eventually
deployed to Production.

Why is it important to update the 'package.json' file? Because whenever another
person downloads the source code, that person can just type `npm install`
in the project's directory to download all the different libraries.

#### Exercise - Run a Local Web Server

Another section reviewed how a web page makes an `AJAX` call to change the
page's content after the page has loaded. In this exercise, you will do the same
with a web server running on your local computer.

##### Create 'index.html' File

Create file 'index.html' with the following content. (For Windows, this file
can be opened with a text editor with command `notepad index.html` .)

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
                url: "/todos/1",
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

This file will be the web page that the browser downloads. The `$.get()` command
in this file makes the `AJAX` call to `/todos/1` which will be defined
in the '1.json' file.

##### Create '1.json' File

Create file '1.json' with the following content. (For Windows, this file
can be opened with a text editor with command `notepad 1.json` .)

```
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

This file will return the JSON content here used by the 'index.html' file when
the 'index.html' file makes its JSON call.

##### Update 'index.js' File

Overwrite what's in 'index.js' with the following. (Again, that file can be opened
in Windows with the `notepad index.js` command.)

```
const path = require('path');
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => res.sendFile(path.join(__dirname + '/index.html')))

app.get('/todos/1', (req, res) => res.sendFile(path.join(__dirname + '/1.json')))

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

This file does the following things in the `Node.js` language.

1) `const path = require('path')` accesses a library for interacting with files.
2) `const express = require('express')` accesses a library for creating web servers.
3) `const app = express()` creates a web server instance.
4) `const port = 3000` is a variable stating which port the server will listen too.
5) The first `app.get()` command will send back the contents of the `index.html`
file when the browser goes to the `/` path.
6) The second `app.get()` command will send back the contents of the `1.json`
file when the browser goes (really makes an `AJAX` call) to `/todos/1`.
7) `app.listen()` will start the web server on port 3000 and print message
`Example app listening on port 3000!` to the console after the server starts.

##### Run the Web Server

From the command line, run `npm run start` to start this server.
Open a web browser and go to `http://localhost:3000/` . The page should load
and `delectus aut autem` should be displayed in the text box after a few seconds.

Even while the server is running, you can change the `delectus aut autem` contents
of the `1.json` file and reload the web page to get a different result
in the text box. That's because the
`(req, res) => res.send(fs.readFileSync('1.json'))` command is a function
that rereads the `1.json` file for each request.

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

### Download and Install Java
First, determine if Java is already installed. Run the command `java -version`
on the command line - if the Java version appears then it's already installed
and you can skip this section. Otherwise follow these steps to install Java.

1) Go to https://adoptopenjdk.net/ .
2) Under the '1. Choose a Version' column, choose 'OpenJDK 11 (LTS)' .
3) Under the '2. Choose a JVM' column, choose 'HotSpot' .
4) Click the 'Latest release' button.
5) Wait a while (like a few minutes) for the file to download.
6) Double-click the downloaded file and follow the installation instructions.

Once the installation is complete, open a new command prompt and enter
`java -version` to confirm that Java is installed (version 11 of Java
should be installed).

#### Run a Simple Java Program

Create a file having name ending in '.java' (like 'sample12.java').

For Windows, open the text editor for this file with the following steps.

1) Open a command prompt.
2) Type command `cd %HOMEPATH%\Desktop` .
3) Type command `notepad sample12.java` .

Place the following content in file, save it, then close the text editor.

```
public class sample12 {
  public static void main(String[] args) {
    System.out.println("Hello World!");
  }
}
```

Now, from the command line, compile this program by typing `javac sample12.java` .
Here's an example for Windows.

```
cd %HOMEPATH%\Desktop
javac sample12.java
```

That command will create file `sample12.class` which can now be run by Java.
The compilation process takes a human-friendly Java source file ('sample12.java')
and converts it into a computer-friendly Java binary file ('sample12.class').
JavaScript is an interpreted language which means that no compilation is necessary
but this also makes JavaScript slower. Java's compilation process makes Java
(generally) faster but can slow down the development process.

Run the 'sample12.class' file now with the following command.

```
cd %HOMEPATH%\Desktop
java -classpath . sample12
```

The '-classpath .' part tells Java where to look for the 'sample12.class' file
(look in the current directory). The file should print out the following
(just like the equivalent JavaScript program).

```
Hello World!
```

Notice how much more effort (or `ceremony`) it took to get the same result
in Java as in JavaScript. The complaint that Java has `too much ceremony`
is common, but Java has many advantages too like better organization,
many people proficient in the language, and powerful tools.

### Spring Boot

Spring Boot is a popular Java-based web application framework. It's based off of the Spring
framework which streamlines the integration of various frameworks (like database integration,
logging, converting HTTP response bodies to JSON, and many other things!).

#### Create Project

Create a project for your sample web application by doing the following.

1) Go to https://start.spring.io/ .
2) Leave the existing form values at their current settings.
3) Under 'Dependencies', click the 'Add' button, enter 'Web', and click the 'Spring Web' option.
4) Click the 'Generate' button.
5) The file 'demo.zip' will be downloaded to your system. Move this file to the Desktop.
6) Unzip this file to create the 'demo' directory on your Desktop.

#### Load Project into IDE

IDE stands for 'Integrated Development Environment' and it's a type of application software
developers use to interact with the source code files in a software project. It's a much more
organized and efficient than using basic tools like Notepad, TextEdit, and the command prompt!

IntelliJ is a very popular IDE for Java developers. Install it by following these steps.

1) Go to https://www.jetbrains.com/idea/download/ .
2) Under 'Community', click the 'Download' button.
3) Open the download and install IntelliJ.
4) Start IntelliJ.
5) Open the 'demo' project by clicking 'File' in the top menu, then click 'Open',
then select the the 'demo' directory on the Desktop.

#### Project Structure

Java uses `build frameworks` to compile source code (like how `javac` is used above,
but for the entire project) and assemble the overall project into the final application.
`Maven` and `Gradle` are popular frameworks. Since they are frameworks, they dictate _how_
one organizes the overall project and expect the project to have a certain directory structure
('these files go here, those files go there'). (Build tools like `Ant` don't impose rules
and leave it to the developer to explicitly construct a step-by-step approach to building
and assembling a project.)

Here are key structural aspects to a Maven-structured project.

  - 'pom.xml' - (Project Object Model) defines what type of project it is (like the 'groupId',
  'artifactId', 'version', and 'name' fields) which is essential for publishing the project
  for others to use (if you're creating a library), lists what other projects it depends on
  under the 'dependencies' section.
  - 'src/main/java' - This is where the main Java source code for the project goes. This is
  the application-specific code that gets executed when the program is run.
  - 'src/main/resources' - This is where supporting files (like properties files
  and HTML pages) go.
  - 'src/test/java' - This is where `unit tests` reside which test out and confirm
  the correctness of the source code in 'src/main/java' before the code there is built
  and assembled into the final application. (It's code to test code!)
  - 'target' - This is the directory where compiled Java class and other files go
  when the project is built and assembled. Using the 'clean' command (used below)
  deletes this directory and it's good (but not necessary) to using this command
  before starting a project. Files in the 'target' directory should _Not_ be stored
  in a source control system (like 'Git' - a 'target' entry should be included
  in the '.gitignore' file to prevent saving 'target' files into Git).

#### Recreate the Node.js Application

##### Create 'index.html' File

In the left bar, right-click over the 'src/main/resources/static' folder, select 'New',
select 'File', then enter 'index.html'. Copy the contents below into this file
and save it (either by selecting 'File' then 'Save' from the menu,
or pressing-and-holding-down the 'Control' (Windows) or 'Command' (Mac) key then pressing 's').

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
                url: "/todos/1.json",
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

##### Create 'todos/1.json' File

In the left bar, right-click over the 'src/main/resources/static' folder, select 'New',
select 'Directory', then enter 'todos'. Then create and save the '1.json' file
with the same contents as the '1.json' file from the Node.js above.

```
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

#### Run Project

Maven can be run on the command line, but it's much easier to just run it using IntelliJ.

The 'spring-boot:run' (which runs the server) command of Maven can be executed from within
IntelliJ using the following commands.

1) Click the 'Maven' (with italicized 'm' over it) tab on the upper-right side of IntelliJ.
This will open the 'Maven' pane on the right side.
2) Within the 'Maven' pane, click the italicized 'm' ('Execute Maven Goal').
3) In the 'Command line' field, enter 'clean spring-boot:run' then click 'Execute'. ('clean'
isn't necessary but it's 'good housekeeping' and 'spring-boot:run' is what actually runs
the project.)
4) Open a browser and go to http://localhost:8080/ to confirm that this application works
the same as the Node.js application above.
5) When finished, click the red square button in the lower-left to stop the application.

#### Maven Lifecycle Commands

Maven comes with predefined standard commands. Here are some of the popular ones.

  - clean - removes the 'target' (build work) directory.
  - test - runs the 'unit' tests in the 'src/test/java' directory. Unit tests are code
  that test other code.
  - package - runs most everything (including compilation, unit testing, and packaging)
  to create finished software, usually a web application or a library ('jar) that other
  applications can use.

The inclusion of 'spring-boot-starter-web' in the 'pom.xml' file makes additional commands
that can be run. The
`mvnw.cmd help:describe -Dplugin=org.springframework.boot:spring-boot-maven-plugin`
(remove the '.cmd' part if on Linux/Mac) lists these additional commands which include
the following.

  - spring-boot:run - Runs the web server.
  - spring-boot:repackage - Assembles all the projects into one (massive) file known
  as a 'fat JAR' (Java ARchive) which contains all of the compiled application code
  and All of the runtime libraries that the application depends on directly or indirectly.
  This command ('goal') should happen after the project is assembled (with 'package' goal)
  so the composite command to create a 'fat JAR' is
  `mvnw.cmd clean package spring-boot:repackage` . The resulting web app (which includes
  a web server) can be run with command `java -jar target\prime-0.0.1-SNAPSHOT.jar`.
  Now that the application is bundled into a single file, it can be easily included onto
  cloud resources (including a Docker image) to run in the cloud.

#### Inversion of Control and Dependency Injection

A critical architectural feature of Spring (including Spring Boot) is the dual concept
of `inversion of control` and `dependency injection`. These mean that specific functionality
'states what it wants' but doesn't actually go and explicitly get it. Instead it relies
on the Spring framework to handle all of the details. (Recommended ways and approaches
for writing software are known as `design patterns`.)

The `@Autowired` annotation keyword is a common way of implementing
this concept within functionality. For instance, if something processing web service calls
(known as a `Controller`) wants to interact with a backend database, that controller
would include a declaration like `@Autowired DatabaseInterface di` (where 'di' is the
variable name for the database interface).

The dual concept of 'inversion of control' and 'dependency injection' has these benefits.

1) Less Code - Source files aren't cluttered with initialization code. They just list what
they want (with `@Autowired` it's just one line of code) instead of several lines of code.
2) `Lously-Coupled` Components - In software engineering, it's a better approach to only
define the bare minimum of what something needs instead of expecting unnecessary and unneeded
details. For instance, for a car, it expects a tire to comply with certain standards
but the car explicitly doesn't state which kind of tire it's using.
3) Makes Unit Testing Easier - Injected (`@Autowired`) components can be mocked (simulated)
during unit testing. Unit tests should _Not_ interact with live systems, instead the unit tests
should simulate those systems with mocked objects that pretend to be those systems.

##### Content Generated on the Server Side

Spring Boot applications can (and often do) host callable web-service endpoints.
These endpoints can dynamically process a request (even a simple one, like adding two numbers)
and provide a response.

###### Exercise - Create a Session-Aware Web Service to Add Two Numbers

`Sessions` are ongoing conversations between a client and a server. The HTTP protocol
by itself doesn't manage sessions, but `Cookie` headers in the requests and responses
can inform both the client and the server that a session has started. What's contained
in the cookie is just a code that's unique to the session
(like '90DED3854451AA60BB03ED2B4639EBE2'). For Java web servers, the name of that cookie
holding that value has historically been something like 'JSESSIONID' .

When the client (browser) sends this code to the server, the server knows that it's the same
client calling again and the server maps that code to configurations (`state`)
saved for the client in the server's memory.

To demonstrate `inversion of control`, `web service endpoints`,
and `cookie-managed session state` follow these steps.

(SuperComputer)
Within the project, create class 'SuperComputer' in folder 'src/main/java/com/example/demo' .
In IntelliJ, this can be done by right-clicking that folder, selecting 'New', then 'Java Class',
then enter the name 'SuperComputer' , then clicking the 'OK' button.

The file should have this content.

```
package com.example.demo;

import org.springframework.stereotype.Service;

@Service
public class SuperComputer {
    public int addNumbers(int numberOne, int numberTwo) {
        return numberOne + numberTwo;
    }
}
```

Note the `@Service` annotation which notifies Spring Boot that this thing (`object`)
should be created when Spring Boot starts.

(DemoController)
`Controllers` contain one or more callable HTTP web service endpoints. Here you will
create an endpoint that will (A) add two numbers and (B) calculate the number of times
the same browser has visited the web page.

In the same folder, create 'DemoController' with the following content.

```
package com.example.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

import javax.servlet.http.HttpSession;

@Controller
public class DemoController {

    @Autowired
    SuperComputer superComputer;

    @GetMapping("/addNumbers")
    @ResponseBody
    public String addNumbers(
            @RequestParam(name = "numberOne") int numberOne,
            @RequestParam(name = "numberTwo") int numberTwo,
            HttpSession httpSession) {
        Integer numberOfVisits = getNumberOfVisits(httpSession);
        return "You have visit this web page " + numberOfVisits
                + " times and the answer to your question is "
                + superComputer.addNumbers(numberOne, numberTwo);
    }
    //
    private Integer getNumberOfVisits(HttpSession httpSession) {
        Integer numberOfVisits =
                ((Integer)httpSession.getAttribute("numberOfVisits"));
        if (numberOfVisits != null) {
            numberOfVisits = numberOfVisits + 1;
        } else {
            numberOfVisits = 1;
        }
        httpSession.setAttribute("numberOfVisits", numberOfVisits);
        return numberOfVisits;
    }
}
```

'addNumbers' takes two request parameters ('numberOne' and 'numberTwo'), sends those parameters
to the super computer `@Autowired SuperComputer superComputer`, then sends back a response
to the client (browser). It's important to note that 'DemoController' does not know anything
about the super computer - it only knows that the super computer can add two numbers.

'getNumberOfVisits' checks how many times the browser has visited the web site by looking
into the 'HttpSession' object, specifically the 'numberOfVisits' field. This function
adds one to that field indicating that the browser has again visited this application.

Start the application. Open a browser and its (Chrome's) developer tools. Go to
`http://localhost:8080/addNumbers?numberOne=1&numberTwo=2` and then go to 'Application' tab.
Select 'Cookies' then 'http://localhost:8080' under it and note that a 'JSESSIONID' cookie
has been assigned.

Refresh the page several times and note how the visit count keeps going up.

Now remove the 'JSESSIONID' cookie by right-clicking over it and selecting 'Delete' .
This drops the session - the server still has a mapping of the session but the client is
no longer passing the code for it. Refresh the page and notice how the visit count drops
back to 1 because the server created a new session for this browser. Refresh the page
again a few times and notice how the visit count increases just like it did before.

###### Exercise - Unit Testing

Create a unit test for the controller to increase your confidence that the controller will have
correctly once the server starts. Unit tests _don't_ interact (make calls to) other servers,
they just test that the targeted source code behaves as it should. This localized testing
becomes very important for larger software projects where it's very difficult to test
one small thing interacting in a very complex system.

In folder 'src/test/java/com/example/demo', create class 'DemoControllerTest' with these
contents.

```
package com.example.demo;

import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;

import javax.servlet.http.HttpSession;

import static org.mockito.ArgumentMatchers.eq;
import static org.mockito.Mockito.when;

public class DemoControllerTest {
    @Test
    public void testController() {
        //
        String expectedResponse = "You have visit this web page " + 6
                + " times and the answer to your question is " + 3;
        //
        SuperComputer superComputer = Mockito.mock(SuperComputer.class);
        HttpSession httpSession = Mockito.mock(HttpSession.class);
        //
        when(superComputer.addNumbers(eq(1), eq(2))).thenReturn(3);
        when(httpSession.getAttribute(eq("numberOfVisits"))).thenReturn(5);
        //
        DemoController demoController = new DemoController();
        demoController.superComputer = superComputer;
        //
        String response = demoController.addNumbers(1, 2, httpSession);
        Assertions.assertEquals(expectedResponse, response);
    }

}

```

The test could be run (with other unit tests if they were also present) by running the Maven
'test' command, but in IntelliJ it can be done by right-clicking over 'testController'
and selecting "Run 'DemoControllerTest'" which will then run the test and output
`Process finished with exit code 0` indicating that the test was a success (a 0 exit code
means that the process completed without error). The actual unit test is done by the
`Assertions.assertEquals` call which compares what was produced versus what was expected.
If you change any of the actual inputs or the expected behaviour of mocked components
(like `when(httpSession.getAttribute(eq("numberOfVisits"))).thenReturn(10);`),
the tests will fail with an error message like this.

```
org.opentest4j.AssertionFailedError: 
Expected :You have visit this web page 6 times and the answer to your question is 3
Actual   :You have visit this web page 11 times and the answer to your question is 3
```

Note here how `Mockito` is used to `mock` both the 'SuperComputer' and 'HttpSession' -
these objects aren't actually present but the `when` call simulates how they should act.

##### IntelliJ Advantages

IntelliJ might look fancy but it shares this in common with Notepad and TextEdit -
it's a text editor!

Command Completion
Find Usages
Localized Unit Test Run
GitHub Integration
Easy Access to Different Files

#### Actuator

As a framework, Spring Boot expects you to do things a certain way, but it also incorporates
a lot of powerful tools. The 'actuator' provides informative diagnostic information about
a running application. It can be turned on just by adding the following lines just under
the 'dependencies' section of the 'pom.xml' file.

```
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>
```

Once that is installed, URLs ('endpoints') like `http://localhost:8080/actuator/health`
will be available which can be used by runtime operations to assess the health of a running
system (the default response `{"status":"UP"}` means that the server is up-and-running okay).

#### Examples of Maven Directory Structure

Many or most Java projects use the traditional Maven directory structure
(or even something more fancy and modern!), including the library used for unit testing.

  - https://github.com/mockito/mockito
