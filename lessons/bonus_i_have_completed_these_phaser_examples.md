# Bonus: I Have Completed These Phaser Examples

## Official 'Hello World' Example

  - Copy the HTML example in the text area
    at https://phaser.io/tutorials/getting-started-phaser3/part5
    and save it to a local file
  - Open this file in a browser and watch 'PHAS3R' icon bounce in field on screen
  - (Optionally) Upload it to your GitHub Pages project and view it there
  - Change (numeric) values in fields like 'width', 'height', 'speed', and 'y',
    then reload the page
  - Go to the full URLs of images like 'logo'
    (http://labs.phaser.io/assets/sprites/phaser3-logo.png)

## Fork Phaser 3 TypeScript Project

TypeScript is a computer language that gets transformed ('compiled') into native
JavaScript. Like 'typed' languages like Java but unlike JavaScript, TypeScript
forces the programmer to declare what types of entities are being dealt with
and marks mismatch errors (like telling an Elephant object to fly) before the
program can be run. A typed language like TypeScript frequently has the advantage
of informing the developer what can be done with different types of entities
during the development process (there can be much less trial-and-error).

Trying to create a modern web project all by oneself ('from scratch') is _not_
easy and can be especially discouraging. It's often better to reuse
(leverage - not 'reinventing the wheel') the work done by others so
that you can concentrate on unique features ('value added') of your project.

By performing a search on the term 'phaser project typescript template' lists
the following TypeScript-based Phaser template project authored by the creator
of Phaser.

  - https://github.com/photonstorm/phaser3-typescript-project-template

### 'Fork' the Phaser 3 TypeScript

In GitHub, 'Forking' a project means to completely create a project in your own
repository that is identical to the original project. This isn't the Git 'clone'
command where a local copy of a repository is made, this is the creation of a
completely new repository whose initial state (files and branches) is identical
to the original repository.

Just as branching creates a distinct copy of code within a Git project, forking
creates a distinct copy between projects.

Fork the project with these steps.

  - Make sure you are logged into GitHub
  - Go to https://github.com/photonstorm/phaser3-typescript-project-template
  - Click the 'Fork' button
    - This will create a project
    https://github.com/<your_username>/phaser3-typescript-project-template
    in your account

### Clone Project Locally

Clone the project locally with these steps.
  - Click the 'Code' button and copy the URL of the project you just created
  - Open a command prompt, go to the Desktop, then use the 'git clone' command
  to copy this repository onto your Desktop
  - Enter 'cd phaser3-typescript-project-template'

### Establish Reference to Original Project

Establish a reference to the original project.
  - As outlined at
  https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/fork-a-repo
  set up your project to by synchronized with the original project using
  the following commands.
    - git remote add upstream https://github.com/photonstorm/phaser3-typescript-project-template.git
      - Entering 'git remote -v' now lists this upstream project

### Periodically Synchronize with Original Project

Whenever there are changes to the original project,
they can be brought in ('sync-ed') to this project.
  - As outlined at
  https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/syncing-a-fork
  run these commands to apply the latest changes from that project into this one.
    - git fetch --all
    - git merge upstream/master

### Install VS Code

VS (Visual Studio) Code is a popular way ('IDE' for Integrated Development Environment)
of managing and editing the files in a UI project for development. Developers quite
often (maybe almost always) prefer to use an IDE instead of using a traditional
text editor (like Notepad or TextEdit) to create and edit files.

Install VS Code by going to https://code.visualstudio.com/Download and clicking
the button corresponding to the operating system (like Windows or Mac)
of your computer.

### Install Node.js

In addition to JavaScript being run within browsers, it can be outside of browsers,
including on a web server ('server-side' JavaScript). Node.js is the application
that can run JavaScript outside of a browser.

Download and install Node.js by going to https://nodejs.org/en/download/ and
clicking the 'Installer' corresponding to the operating system
(like Windows or Mac) of your computer.

Once installed, command 'node -v' will print the version that got installed
and verify that the installation was successful.

### Download Project Libraries

From the 'phaser3-typescript-project-template' project directory, download
the libraries needed by this project (found under the 'dependencies' and
'devDependencies' keys in the 'package.json' file in the same directory)
with this command.

  - npm install

### Run Project Locally

Also in the 'package.json' under the 'scripts' key, there is a list of commands
that can be run with 'npm run' to do things with the project. The 'README.md' file
in same directory states that 'npm run watch' will start a local server for this
project. Run this command.

  - npm run watch
    - A browser tab at http://localhost:10001/ should eventually open
    for this project.

Note that this command, like command 'npm run build', will create files in the
'dist' subdirectory that can be viewed locally or uploaded to a web server
(like GitHub Pages) and the application will do the same thing as it does
on http://localhost:10001/ . The 'watch' command differs from the 'build'
command in that the 'watch' command also actively runs (and incorporates file
changes after it starts) a web server at http://localhost:10001/ .

### Load Project into VS Code

Open VS Code, select 'File' then 'New Window', then click 'Open folder' link,
then select the 'phaser3-typescript-project-template' directory.

### Make a Small Edit and View Change

In VS Code, click the 'src' directory in the 'Explorer' (left side), then click
'game.ts' . Immediately below the following line.

  - const logo = this.add.image(400, 70, 'logo');

Enter the following line. This will place center of another copy of the 'logo' image
(defined in the 'preload' section of the same file) onto the top-left corner
of the rectangle where this application is rendered on the web page.

  - const logo2 = this.add.image(0, 0, 'logo');

Save this file and reload http://localhost:10001/ . Notice how the lower-right
portion of another copy of the 'PHAZ3R' logo now appear in the upper-left
part of the screen.

### View Documentation for Code

In the 'game.ts' file in VS Code, hold down the 'Control' (Windows)
or 'Command' (Mac) button then click the 'image' word in this command.

  - const logo2 = this.add.image(0, 0, 'logo');

This will open another file (called 'phaser.d.ts') that explains what the
'image' function does. IDEs are text editors but have powerful tools that
aid the developer.
