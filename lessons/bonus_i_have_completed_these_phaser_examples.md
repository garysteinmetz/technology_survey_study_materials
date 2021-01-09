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

## Important Phaser Resources

  - https://examples.ourcade.co/phaser3-typescript
  - https://ourcade.co/books/infinite-runner-phaser3/ (get TypeScript version)
  - https://ourcade.co/
  - https://www.youtube.com/channel/UCJyrgLkI9LcwzUhZXxrwpyA
  - https://gamedevacademy.org/phaser-progressive-web-apps-tutorial/
  - https://phaser.io/tutorials/getting-started-phaser3/part5

## Incremental Upkeep of Local TypeScript Phaser Project

These steps will incorporate the latest changes from your project on GitHub
and the one that you inherited ('forked') from.

If you are the only one working on the project and all the work is done on the
same computer, you may only need to run these steps rarely if ever,
but it's good to follow these steps as good practice to confirm that you've
incorporated the latest changes as they become available.

  - Open a command prompt enter the following commands
    - cd Desktop
    - cd phaser3-typescript-project-template
    - git fetch --all
    - git merge upstream/master
    - git merge origin/master
    - git push origin master

Note that the 'git merge upstream/master' command might cause a 'merge conflict'
(a clash between your local files and one from the original project which
you inherited from). If this happens, run the following command first then reissue
the 'git merge origin/master' command and continue.

  - git reset --hard

If the 'git merge origin/master' command keeps causing merge conflicts,
just ignore running it (skip it).

Finally, run the following command to ensure that the latest versions of JavaScript
libraries are installed.

  - npm install

## Running Local Server

  - Open a command prompt enter the following commands
    - cd Desktop
    - cd phaser3-typescript-project-template
    - npm run watch

As documented in the 'package.json' file, the 'watch' command will compile
(really 'transpile' since this is TypeScript) and also watch for new edits
to the project which it quickly incorporates (re-compiles) project code changes
that are saved. This command (in 'package.json') references
the 'rollup.config.dev.js' file in the same directory which includes a 'serve'
command which starts a local server on port 10001 (URL http://localhost:10001/ ).

Whenever you save a change to your project, wait about 15 seconds for the 'watch'
command to compile ('transpile') the change, then refresh the browser to review it.

## Stopping Local Server

After finishing development work, press Control-C (hold down the 'Control' button
then press the 'c' character) to stop the server. Rerun the 'npm run watch' command
to restart the server.

## Exercise - Update the Images of the Default Application

### Setup - How to Create Images

Go to https://jspaint.app/ or use the local Windows 'Paint' program to create
two images - the 'head' side of a coin and the 'tail' side of a coin.

#### Set Dimension Boundaries and (Optionally) Make the Background Transparent

In the menu, click 'Image' then 'Attributes' then do the following.

  - For 'Units', select 'Pixels'
  - For 'Width', enter the desired width (like 100) in pixels
    - Review next subsection to get specific pixel recommendations for each image
  - For 'Height', enter the desired height (like 100) in pixels
  - (Optional) To make sure that the unpainted parts of the image don't cover
  up what's behind it, select 'Transparent' under 'Transparency'

Once this is done, click the 'Okay' button.

  - If you selected the 'Transparency' button, clear the existing (white) background
  by selecting 'Image' then 'Clear Image' . The image should now look somewhat like
  a checkerboard (this is the representation of a transparent background,
  but it (the unpainted parts) will be 'see through' once rendered on a web page).

##### Image Pixel Dimension Recommendations

  - dist/assets/phaser3-logo.png
    - Width - 412
    - Height - 93

  - dist/assets/libs.png
    - Width - 800
    - Height - 600
      - Note - The content for this image should appear below
      (approximately) y-coordinate 425, all area above this should be transparent

##### Importance of Transparency

For a PNG image, pixels marked as transparent are invisible and whatever is behind
it when rendered on a web page will be displayed instead (for a plain web page,
the default background color is white).

When the server is running, notice how the 'PHAZ3R' letters are Not changed
by the swirling colors. Likewise, the stylized red 'R' letter, 'rollup.js' text,
and 'TypeScript' text are also unaffected by the swirling colors.

### Step 1 - Create Images

  - Using https://jspaint.app/ or another graphical application, create images
  with the same dimensions (and transparency) as 'dist/assets/phaser3-logo.png'
  and 'dist/assets/libs.png'
  - Save these images into the 'dist/assets' subdirectory of the project
  - In the 'src/game.ts' file of the project, update the second parameter
  of each of the two 'this.load.image()' statements to reference these new images
  - (If not running already) Run the local server and verify your work
  by going to web page http://localhost:10001/

### Step 2 - Commit and Push Changes to GitHub

Using the 'add', 'commit', and 'push' commands of Git, commit and push these
changes to your repository in GitHub.

### Step 3 - Copy 'dist/' Subdirectory Contents to Your GitHub Pages Repository

First, issue the following commands in your GitHub Pages repository to ensure
that you're on the 'main' branch with the latest source code.

  - git checkout main
  - git fetch --all
  - git pull origin main

Copy the contents of the 'dist/' subdirectory into your GitHub pages repository.

  - Note - The copied contents should be copied directory into the base directory
  of this repository, not into a 'dist/' subdirectory
    - For instance, 'dist/index.html' in the Phaser project should just be
    'index.html' in the GitHub Pages project

Then commit and push these changes in your GitHub pages project.
Now, open a browser and go to your GitHub pages base address to review your
work that has now been published to the internet.

  - https://<your_github_username>.github.io

## If Applicable, Change the 'master' Branch to the 'main' Branch

Towards the end of 2020, it became increasingly popular to rename the 'master'
branch of a repository to the 'main' branch. Here are the steps for doing that.

Reference - https://stevenmortimer.com/5-steps-to-change-github-default-branch-from-master-to-main/

  1) Locally copy the 'master' branch to the 'main' branch with this command
    - git branch -m master main
  2) Upload this new 'main' branch to the remote repository with this command
    - git push -u origin main
  3) Update the local repository to state that 'main' is the default remote branch with this command
    - git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main
  4) Follow the steps at this link to state that 'main' is the default branch on the remote server
    - https://docs.github.com/en/github/administering-a-repository/setting-the-default-branch
  5) Delete the 'master' branch both on the local server and the remote server with this command
    - git push origin --delete master

As you make these changes, consider doing one or more of the following to verify
that both the local and remote repositories have changed.

  - `git status`
    - This will list the current branch that's checked out into the local file system
  - `git branch -a`
    - This will list all branches in the local repository
  - Using a browser, view your repository on GitHub and the branches it contains

//

https://stackoverflow.com/questions/46559795/how-to-use-js-cookie-in-a-typescript-project
https://www.npmjs.com/package/js-cookie

//

TypeScript versus JavaScript
Transpiling (Babel)
How TypeScript becomes JavaScript which can run in a browser
Switch from 'master' branch to 'main' branch
Sprites and scenes
Deploying to GitHub Pages
Cookies
Gimp (with transparency)
Import Images (including ones from another web site)
Phaser Component Lifecycle
Effects with sprites and scenes
Events with sprites
Classes including - Phaser.Math, tile image, spritesheet, 'anims' function
Cursor keys
