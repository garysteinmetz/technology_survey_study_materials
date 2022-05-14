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

## Use Gimp to Create Image Files

Gimp is a tool for creating and editing image files, especially PNG files.

PNG files are standard graphical files used on web pages. Each `pixel` (smallest
square of consistent color which, along with all other pixels, compose the image)
can be composed of distinct concentrations of the three primary colors of light -
red, green (not yellow!), and blue.

PNG also supports the `alpha channel` feature, which allows a pixel to be partially
or completely invisible. This is important when developing games and general
graphical content because (A) graphical images tend to be rectangular and most
objects aren't rectangular and (B) when one image is on top of another the top
image's invisible pixels shouldn't overwrite the pixels of the image below it.

### Exercise - Create an Image with Transparent Pixels Using Gimp

1) Open Gimp
2) In the top menu, select 'File' then 'New'
3) In the 'Create a New Image' window, set the 'Width' and 'Height' values to 200,
then click the 'OK' button
4) In the top menu, select 'Layer', then 'Transparency', then click 'Add Alpha Channel'
5) Click the large black-circle-on-white-square in the top-right, then in the
top-left click the erase tool (which is below the 'A' and above the band-aid images),
then click and swipe over the entire image (an image like a checkerboard should
appear under it, this checkerboard is the way Gimp and other tools represent
an area as being transparent)
6) In the top-left, click the pencil then click the red rectangle below it to change
the color written by it
7) In the 'Change Foreground Color' window, enter a 'hexadecimal' code into the
'HTML notation' field for the color you want to draw with, then click the 'OK'
button (codes can be obtained from sites like
https://www.rapidtables.com/web/color/RGB_Color.html#color-chart under 'Hex')
8) Draw on the image and switch colors as desired, to change paintbrush size
click the desired paintbrush shape in the top-right
9) To fill an area, click the paint can next to the 'A' image in the top-left
then click the area to fill on the image
10) Save the image, in the top menu click the 'File' then 'Export' (not 'Save'!)
to save the image to the local file system

Gimp has many features for creating, editing, and transforming images. Consider
playing around with the tool and reviewing online resources (including
YouTube videos) to learn more about it.

### Exercise - Create a Web Page Where One Image Partially Covers Another

Using Gimp, create two 200-pixel-by-200-pixel images with non-overlapping
transparent areas then save them to your Desktop, one named '1.png' and the
other named '2.png' . Then create an HTML file (with a name like 'overlap.html')
on the Desktop with this content.

```
<html>
  <head>
    <style>
      img.over {
        position: absolute;
        left: 0px;
        top: 0px;
        z-index: 1;
      }
      img.under {
        position: absolute;
        left: 0px;
        top: 0px;
        z-index: -1;
      }
    </style>
  </head>
  <body>
    <img src="1.png" class="over" />
    <img src="2.png" class="under" />
  </body>
</html>
```

Open the HTML file in a browser and notice how all the content of '1.png'
is shown and, where it overlaps with '2.png', the content of '2.png' isn't shown.


## Exercise - Create Scene Effects

Create two PNG files for this exercise, one called 'scene1.png' and the other named
'scene2.png', and place them into the 'dist/assets' subdirectory of the project.
Each image should have a width of 800 pixels and a height of 600 pixels.

To resize an image in Gimp, in the top menu select the 'Image' option then
the 'Canvas Size' option. To zoom in and zoom out on the image, select an option
from the top menu under 'View' then 'Zoom' . (The 'Fit Image in Window' is useful.)

### What to Do When the Paintbrush Doesn't Work

Gimp can sometimes get into a state where you try to paint but nothing happen.
A 'layer' in the image can get 'locked' which prevents modification. This can happen,
for instance, when adding text to an image.

Based on suggestions at https://docs.gimp.org/2.10/en/gimp-getting-unstuck.html ,
here are actions to unlock the layer which should allow you to continue painting.
If text was added, that 'layer' should be 'merged' into the entire canvas by
selecting 'Layer' from the top menu then selecting the 'Merge Down' option.
A common solution (to get back to normal) is to choose 'Select' from the top menu
then select the 'All' option.

### Update Main Page in Project, Reload Page, Click Image Several Times

Overwrite the 'src/game.ts' file in the project with the following contents.
Once the server is started, go to http://localhost:10001/ , open developer tools
in the browser, then (with delays between each) click the image 6 times.

```
import 'phaser';

let screen_width = 800;
let screen_height = 600;

export default class Demo extends Phaser.Scene
{
    constructor ()
    {
        super('s1');
    }

    image1: Phaser.GameObjects.Image;
    clickCount = 0;

    preload ()
    {
        this.load.image('scene1', 'assets/scene1.png');
    }

    create ()
    {
        this.image1 = this.add.image(screen_width/2, screen_height/2, 'scene1');
        this.image1.setInteractive();
        this.image1.on(Phaser.Input.Events.POINTER_DOWN,
            () => {
                this.clickCount++;
                //
                if (this.clickCount === 2) {
                    console.log("Start Effect - Resize, Shrink By Half");
                    this.image1.setScale(0.5);
                } else if (this.clickCount === 3) {
                    console.log("Start Effect - Rotate, Flip Image Over");
                    this.image1.setRotation(Phaser.Math.DegToRad(180));
                } else if (this.clickCount === 4) {
                    console.log("Start Effect - Set Alpha, Make Half Invisible");
                    this.image1.setAlpha(0.5);
                } else if (this.clickCount === 5) {
                    console.log("Start Effect - Set Horizontal, Move Image Right");
                    this.image1.x = this.image1.x + 100;
                } else if (this.clickCount === 6) {
                    console.log("Start Effect - Change Scene, Display Next Scene");
                    let scene2 = this.scene.add('s2', new AnotherScene(), false);
                    this.scene.switch('s2');
                } else {
                    console.log("First Click - Do Nothing");
                }
            });
    }
}

class AnotherScene extends Phaser.Scene {
    //
    constructor ()
    {
        super('s2');
    }

    image2: Phaser.GameObjects.Image;

    preload ()
    {
        this.load.image('scene2', 'assets/scene2.png');
    }

    create ()
    {
        //
        this.image2 = this.add.image(screen_width/2, screen_height/2, 'scene2');
        console.log("Scene 2 has been loaded");
    }
}

const config = {
    type: Phaser.AUTO,
    backgroundColor: '#125555',
    width: screen_width,
    height: screen_height,
    scene: Demo
};

const game = new Phaser.Game(config);

```

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


## Exercise - Basketball Game

Base Project - https://github.com/photonstorm/phaser3-typescript-project-template

```
git clone https://github.com/photonstorm/phaser3-typescript-project-template.git
```

Override 'src/game.ts' file with contents in code block below

Run these 'npm' commands -

```
npm install
npm run watch
```

Open Browser - http://localhost:10001/

Upload to Public server (recommended - rename 'dist/index.html' file) -

```
aws s3 sync --acl public-read --exclude ".*" ./dist s3://content.chhcsfun.com/content
```

### 'src/game.ts' Contents

```
import 'phaser';
import { Physics } from 'phaser';

//https://photonstorm.github.io/phaser3-docs/
export default class BasketballGame extends Phaser.Scene
{
    keys: Phaser.Types.Input.Keyboard.CursorKeys;
    basketball: Phaser.GameObjects.Sprite;
    net: Phaser.GameObjects.Sprite;
    scoreBoard: Phaser.GameObjects.Text;
    score: number = 0;

    constructor ()
    {
        super('basketballGame');
    }

    preload ()
    {
        this.load.image(
            'basketball',
            'https://img.icons8.com/emoji/48/000000/basketball-emoji.png'
        );
        this.load.image(
            'net',
            'https://img.icons8.com/color/48/000000/basketball-net.png'
        );
        //Entering 'online sound effect generator' into a search engine lists sites like these
        //  - https://sfxr.me/
        //  - https://www.leshylabs.com/apps/sfMaker/
        //
        //Note - Uncomment the line below to load a sound, uncomment line in 'create' function to play it
        //  Copy the sound file into the 'dist' directory of this project
        //  Use the correct name for that sound file immediately below instead of using "sound.wav"
        //this.load.audio("sound1", "sound.wav");
    }

    create ()
    {
        this.scoreBoard = this.add.text(
            scoreBoardOffset, scoreBoardOffset, this.score.toString());

        this.basketball = this.add.sprite(
            basketballOffset, basketballOffset, "basketball");
        this.basketball.displayWidth = spriteSide;
        this.basketball.displayHeight = spriteSide;

        this.net = this.add.sprite(netOffset, netOffset, "net");
        this.net.flipX = true;
        this.net.displayWidth = spriteSide;
        this.net.displayHeight = spriteSide;

        this.keys = this.input.keyboard.createCursorKeys();

        this.physics.add.existing(this.basketball);
        this.physics.add.existing(this.net);
        this.physics.add.collider(this.basketball, this.net,
            (a, b) => {
                //Note - Uncomment the line below to play a sound (must be loaded above)
                //this.sound.play("sound1");
                this.score = this.score + 1;
                this.scoreBoard.text = this.score.toString();
                this.basketball.setY(basketballOffset);
                this.basketball.setX(basketballOffset);
            });
    }
    update ()
    {
        if (this.keys.down.isDown) {
            this.basketball.setY(this.basketball.y + movementOffset);
            if (this.basketball.y > canvasHeight) {
                this.basketball.setY(0);
            }
        }
        if (this.keys.up.isDown) {
            this.basketball.setY(this.basketball.y - movementOffset);
            if (this.basketball.y < 0) {
                this.basketball.setY(canvasHeight);
            }
        }
        if (this.keys.right.isDown) {
            this.basketball.setX(this.basketball.x + movementOffset);
            if (this.basketball.x > canvasWidth) {
                this.basketball.setX(0);
            }
        }
        if (this.keys.left.isDown) {
            this.basketball.setX(this.basketball.x - movementOffset);
            if (this.basketball.x < 0) {
                this.basketball.setX(canvasWidth);
            }
        }
    }
}

const canvasWidth = 400;
const canvasHeight = 400;

const scoreBoardOffset = 0;
const basketballOffset = 100;
const netOffset = 250;

const movementOffset = 2;

const spriteSide = 75;

const config = {
    type: Phaser.CANVAS,
    backgroundColor: '#125555',
    width: canvasWidth,
    height: canvasHeight,
    scene: BasketballGame,
    //Note - the following setting is required to use 'this.physics'
    physics: {
        default: "arcade"
    }
};

const game = new Phaser.Game(config);

```

## Exercise - Haunted Treasure Game

Use the same setup as the basketball game, but update the contents as follows.

### 'src/game.ts' Contents

```
import 'phaser';
import { Physics } from 'phaser';

//https://photonstorm.github.io/phaser3-docs/
export default class HauntedTreasureGame extends Phaser.Scene
{
    keys: Phaser.Types.Input.Keyboard.CursorKeys;
    adventurer: Phaser.Types.Physics.Arcade.SpriteWithDynamicBody;
    ghost: Phaser.Types.Physics.Arcade.SpriteWithDynamicBody;
    treasureChest: Phaser.Types.Physics.Arcade.SpriteWithDynamicBody;
    scoreBoard: Phaser.GameObjects.Text;
    highScoreBoard: Phaser.GameObjects.Text;
    score: number = 0;
    highScore: number = 0;
    background: Phaser.GameObjects.Image;

    constructor ()
    {
        super('hauntedTreasureGame');
    }

    preload ()
    {
        this.load.image(
            'adventurer',
            'https://img.icons8.com/external-vitaliy-gorbachev-flat-vitaly-gorbachev/58/000000/external-explorer-jungle-vitaliy-gorbachev-flat-vitaly-gorbachev-1.png'
        );
        this.load.image(
            'ghost',
            'https://img.icons8.com/dusk/64/000000/ghost--v1.png'
        );
        this.load.image(
            'treasureChest',
            'https://img.icons8.com/external-justicon-flat-justicon/64/000000/external-treasure-pirates-justicon-flat-justicon.png'
        );
        this.load.image(
            'background',
            'https://img.icons8.com/external-justicon-lineal-justicon/64/000000/external-haunted-house-halloween-justicon-lineal-justicon.png');
        //    'https://img.icons8.com/external-icongeek26-linear-colour-icongeek26/64/000000/external-desert-desert-icongeek26-linear-colour-icongeek26-1.png');
        //this.load.audio("sound1", "sound.wav");
    }

    create ()
    {
        this.background = this.add.image(canvasWidth/2, canvasHeight/2, 'background');
        this.background.setDisplaySize(canvasWidth, canvasHeight);
        //
        this.scoreBoard = this.add.text(
            scoreBoardOffset, scoreBoardOffset, ("Score: " + this.score));
        this.highScoreBoard = this.add.text(
            highScoreBoardLeftOffset, highScoreBoardTopOffset,
            ("High Score: " + this.highScore));
        //
        this.adventurer = this.physics.add.sprite(
            adventurerOffset, adventurerOffset, "adventurer");
        this.adventurer.displayWidth = spriteSide;
        this.adventurer.displayHeight = spriteSide;
        this.adventurer.setVelocity(0, 0);
        //
        this.treasureChest = this.physics.add.sprite(
            treasureChestOffset, treasureChestOffset, "treasureChest");
        this.treasureChest.displayWidth = spriteSide;
        this.treasureChest.displayHeight = spriteSide;
        //
        //
        this.ghost = this.physics.add.sprite(ghostOffset, ghostOffset, "ghost");
        this.ghost.flipX = true;
        this.ghost.displayWidth = ghostSide;
        this.ghost.displayHeight = ghostSide;
        this.updateGhostMovement();

        this.keys = this.input.keyboard.createCursorKeys();

        //this.physics.add.existing(this.adventurer);
        //this.physics.add.existing(this.ghost);
        this.physics.add.collider(this.adventurer, this.ghost, null,
            (a, b) => {
                //this.sound.play("sound1");
                if (this.highScore < this.score) {
                    this.highScore = this.score;
                }
                this.resetPlayers();
                this.resetGame();
                this.updateScoreBoards();
                return true;
            }, this);
        this.physics.add.collider(this.adventurer, this.treasureChest, null,
            (a, b) => {
                //this.sound.play("sound1");
                this.score = this.score + 1;
                this.resetPlayers();
                this.updateScoreBoards();
                ghostSide = ghostSide + ghostSideIncrement;
                this.ghost.displayWidth = ghostSide;
                this.ghost.displayHeight = ghostSide;
                ghostMovementOffset = ghostMovementOffset + ghostMovementIncrement;
                return true;
            }, this);
        setInterval(
            () => {
                this.updateGhostMovement();
            },
            2000
        );
    }
    update ()
    {
        if (this.keys.down.isDown) {
            this.adventurer.setY(this.adventurer.y + adventurerMovementOffset);
        }
        if (this.keys.up.isDown) {
            this.adventurer.setY(this.adventurer.y - adventurerMovementOffset);
        }
        if (this.keys.right.isDown) {
            this.adventurer.setX(this.adventurer.x + adventurerMovementOffset);
        }
        if (this.keys.left.isDown) {
            this.adventurer.setX(this.adventurer.x - adventurerMovementOffset);
        }
        this.wrapBoundary(this.adventurer);
        this.wrapBoundary(this.ghost);
        //for some reason, this sprite starts to follow ghost
        //  after a while, this command prevents that
        this.adventurer.setVelocity(0, 0);
    }
    wrapBoundary (sprite: Phaser.Types.Physics.Arcade.SpriteWithDynamicBody)
    {
        //
        if (sprite.y > canvasHeight) {
            sprite.setY(0);
        }
        if (sprite.y < 0) {
            sprite.setY(canvasHeight);
        }
        if (sprite.x > canvasWidth) {
            sprite.setX(0);
        }
        if (sprite.x < 0) {
            sprite.setX(canvasWidth);
        }
    }
    resetPlayers()
    {
        this.adventurer.setY(adventurerOffset);
        this.adventurer.setX(adventurerOffset);
        this.ghost.setY(ghostOffset);
        this.ghost.setX(ghostOffset);
    }
    resetGame()
    {
        this.score = 0;
        ghostMovementOffset = baseGhostMovementOffset;
        ghostSide = spriteSide;
        this.ghost.displayWidth = ghostSide;
        this.ghost.displayHeight = ghostSide;
    }
    updateScoreBoards()
    {
        this.scoreBoard.text = ("Score: " + this.score);
        this.highScoreBoard.text = ("High Score: " + this.highScore);
    }
    updateGhostMovement() {
        const leftPolarity = Phaser.Math.RND.between(0, 1) === 1 ? 1 : -1;
        const topPolarity = Phaser.Math.RND.between(0, 1) === 1 ? 1 : -1;
        this.ghost.setVelocity(
            leftPolarity*Phaser.Math.RND.between(1, ghostMovementOffset),
            topPolarity*Phaser.Math.RND.between(1, ghostMovementOffset));
    }
}

const canvasWidth = 400;
const canvasHeight = 400;

const scoreBoardOffset = 0;
const highScoreBoardLeftOffset = 200;
const highScoreBoardTopOffset = 0;
const adventurerOffset = 100;
const ghostOffset = 250;
const ghostSideIncrement = 5;
const treasureChestOffset = 250;

const adventurerMovementOffset = 2;
const baseGhostMovementOffset = 5;
const ghostMovementIncrement = 5;
let ghostMovementOffset = baseGhostMovementOffset;

const spriteSide = 75;
let ghostSide = spriteSide;
const backgroundColor = '#303030';

const config = {
    type: Phaser.CANVAS,
    backgroundColor: backgroundColor,
    width: canvasWidth,
    height: canvasHeight,
    scene: HauntedTreasureGame,
    //Note - the following setting is required to use 'this.physics'
    physics: {
        default: "arcade"
    }
};

const game = new Phaser.Game(config);
```

## Exercise - Combine Sprite Sheets and Promises

### Create Sprite Sheet

#### Create a Multi-Layer Image with Transparency Enabled

Using Gimp, create a multi-layer image with transparency (i.e. alpha channel enabled).
The dimensions of this image should be 200 pixels wide by 200 pixel high.
Each layer of the image should contain a frame of whatever type
(e.g. animal, character, weapons) sprite sheet is being developed.

#### Assemble and Export Image as a Sprite Sheet

Do the following.

  - In the menu, select `Filters > Combine > Filmstrip`
  - In the 'Selection' tab, do the following
    - Check 'Fit height to images' checkbox
    - Uncheck 'At top' and 'At bottom' checkboxes
    - Click the colored rectangle next to `Color` label in the `Filmstrip` section
      - In the `Select Film Color` popup window, enter `fffffe`* for `HTML notation` field,
      then click `OK` button
  - In the 'Advanced' tab, do the following
    - Slide the `Image height` slider all the way to the right (resulting value of `1.000`)
    - Slide all other sliders to the left (resulting value of `0.000` for each)
  - Click the `OK` button

* That's a code for an almost completely white color that probably wasn't used in any layer.

Now do the following to clear the background of the resulting sprite sheet.

  - In the menu, select `Layer > Transparency > Add Alpha Channel`
  - In the menu, select `Layer > Transparency > Color to Alpha`
    - In the `Color to Alpha` popup window, do the following
      - Click the colored rectangle next to `Color` label
      - In the `Select Film Color` popup window, enter `fffffe`* for `HTML notation` field,
      then click `OK` button
  - Click the `OK` button

Now export this image as a PNG file.

  - In the menu, select `File > Export`
  - In the `Name` field, enter `sampleSpriteSheet1.png`
  - Select the `Desktop` directory
  - Click the `Export` button
  - In the `Export Image as PNG` popup, do the following
    - Uncheck the `Save background color` and `Save color values from transparent pixels` checkboxes
    - Click the `Export` button

### Create Web Page

```
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/phaser@3.55.2/dist/phaser.min.js"></script>
        <script>
            var loadedSpriteSheets = [];
            //z-index (depth), sprite sheet, frames, object, creation time, state
            var nameSpriteStartTimeMs;
            var frameAssembly = {
                "id": "name",
                "spriteSheet": "Untitled.png",
                "depth": 1,
                "motionSequence": [
                    {
                        "frame": 0,
                        "durationMs": 700
                    },
                    {
                        "frame": 1,
                        "durationMs": 200
                    },
                    {
                        "frame": 2,
                        "durationMs": 400
                    },
                    {
                        "frame": 3,
                        "durationMs": 100
                    }
                ]
            };
            var game;
            var nameSprite;
            var battleOn;
            const config = {
                type: Phaser.CANVAS,
                parent: "phaser-target",
                backgroundColor: '#125555',
                width: 300,
                height: 300,
                scene: {
                    preload: preload,
                    create: create,
                    update: update
                }
            };
            $(document).ready(
                () => {
                    //console.log(0);
                    game = new Phaser.Game(config);
                }
            );
            function preload() {
                //console.log(1 + " - " + Object.keys(game.scene.game));
                //this.load.image(frameAssembly.id, frameAssembly.spriteSheet);
                this.load.spritesheet(frameAssembly.id, frameAssembly.spriteSheet, {frameWidth: 200, frameHeight: 200});
                //
                battleOn = true;
            }
            function create() {
                //console.log(2);
                //this.add.sprite(150, 150, 'ghost', 'ghost');
                nameSprite = this.add.sprite(150, 150, frameAssembly.id, frameAssembly.id, 0);
                nameSprite.setFrame(frameAssembly.motionSequence[0].frame);
                nameSpriteStartTimeMs = Date.now();
            }
            var alreadyUpdated = false;
            function update() {
                console.log("ZZZ game.load.image - " + this.load.spritesheet);
                var currentTimeMs = Date.now();
                var elapsedTimeMs = (currentTimeMs - nameSpriteStartTimeMs);
                var totalMotionSequenceTimeMs = 0;
                frameAssembly.motionSequence.forEach(
                    (a) => {
                        totalMotionSequenceTimeMs += a.durationMs;
                    }
                );
                var frameOffsetMs = elapsedTimeMs%totalMotionSequenceTimeMs;
                var selectedFrame = 0;
                var accumulatedMs = 0;
                frameAssembly.motionSequence.forEach(
                    (a) => {
                        accumulatedMs += a.durationMs;
                        if (accumulatedMs < frameOffsetMs) {
                            selectedFrame++;
                        }
                    }
                );
                nameSprite.setFrame(frameAssembly.motionSequence[selectedFrame].frame);
                //if (!alreadyUpdated) {
                //    alreadyUpdated = true;
                //    updateOnce();
                //}
            }
            function loadSpriteSheet(spriteSheetName, spriteSheetUrl, actionAfterImageLoads) {
                if (loadedSpriteSheets.includes()) {
                    game.load.spriteSheet(
                        spriteSheetName, spriteSheetUrl, {frameWidth: 200, frameHeight: 200}
                    );
                }
            }
            /*
            function updateOnce() {
                executeWithMinimumDelay(
                    new Promise((resolve, reject) => {console.log("Wait 5 seconds"); resolve(5000);}),
                    100,
                    (result) => {
                        nameSprite.setFrame(1);
                        executeWithMinimumDelay(
                            new Promise((resolve, reject) => {resolve();}),
                            100,
                            (result) => {
                                nameSprite.setFrame(2);
                                executeWithMinimumDelay(
                                    new Promise((resolve, reject) => {resolve();}),
                                    100,
                                    (result) => {
                                        nameSprite.setFrame(3);
                                        nameSprite.destroy();
                                        //canvas, anims, scene
                                        console.log("ZZZ game.scene - " + Object.keys(game.scene.game.anims));
                                        //game.scene.cameras.main.fadeOut(5000, 0, 255, 0);
                                    }
                                );
                            }
                        );
                        //console.log("Result2 -  " + result);
                        //playAudio("data:audio/wav;base64,UklGRtEaAABXQVZFZm10IBAAAAABAAEARKwAAESsAAABAAgAZGF0Ya0aAAAAPUFFSU1RVVldYWVpbXF1eX2BhYmNkZWZnaGkqKywtLi8wMTHxMC8uLSwrKikoJyYlJCMiISAfHh0cGxoZWFdWVVRTUlFQT05Oj5CRkpOUVVZXWFlaW1xdXl9gYWJjZCUmJygpKissLS4vL/DxsO/u7ezr6uno6CcmJSQjIiEgHx4dHFtaWVhXVlVUU1KRkI+Ojs+QkZKTlJWWl5iZmltcXV5fYGFiYyQlJicoKSoq6+zt7u/w8XCvrq2s6+rp6Ofm5eUkIyIhIB8eHVxbWllYV1aVlJOSkZCPzs7P0NHS09SVlpeYmZqbnF1eX2BhYiMkJSYnJ+jp6uvs7a6vsLFwb66trKuqqajn5uXk4+MiISAfHl1cW1pZWJeWlZST0tHQz88PEBESEtPU1dbXmJmam5ydXl9gYWIjJCUmJufo6eqrrK2ur3BxMG9ubWxrqqmop6bl5OPjIiEgHx5dXFtaWZiXlpXU09LSERAPD1BREhMUFNXW19jZmpucnV5fYGEiIyQlJebn6Omqq6xtbm9wMPAvLi1sa2ppqKempeTj4uIhIB8eXVxbWpmYl9bV1NQTEhEQT0+QUVJTVBUWFtfY2dqbnJ2eX2BhIiMkJOXm56ipqqtsbW4vMDCv7u4tLCtqaWhnpqWk4+LiISAfHl1cW5qZmNfW1hUUE1JRUE+PkJGSU1RVFhcYGNna25ydnl9gYSIjI+Tl5qeoqWprbC0uLu/wb67t7OwrKiloZ2alpKPi4eEgHx5dXJuamdjX1xYVFFNSUZCPz9DRkpOUVVZXGBkZ2tucnZ5fYGEiIyPk5aanqGlqayws7e7vsG+urazr6yopKGdmZaSj4uHhIB9eXVybmpnY2BcWFVRTkpHQz9AQ0dLTlJVWV1gZGhrb3J2eX2BhIiLj5OWmp2hpaisr7O2ur3Avbm2sq+rp6SgnZmWko6Lh4SAfXl1cm5rZ2RgXFlVUk5LR0RAQURIS09SVlpdYWRoa29ydnp9gYSIi4+SlpmdoaSoq6+ytrm9v7y5tbKuq6ejoJyZlZKOi4eEgH15dnJua2dkYF1ZVlJPS0hEQUFFSExPU1ZaXmFlaGxvc3Z6fYGEiIuPkpaZnaCkp6uusrW5vL68uLWxrqqno6CcmZWSjouHhIB9eXZyb2toZGFdWlZTT0xJRUJCRklNUFNXWl5hZWhsb3N2en2BhIiLjpKVmZygo6eqrrG0uLu+u7e0sK2qpqOfnJiVkY6Kh4SAfXl2cm9raGVhXlpXU1BNSUZCQ0ZKTVFUV1teYmVpbG9zdnp9gYSHi46SlZmcn6Omqq2wtLe7vbq3s7Csqaain5uYlZGOioeDgH15dnNvbGhlYl5bV1RRTUpHQ0RHSk5RVVhbX2JmaWxwc3Z6fYGEh4uOkZWYnJ+ipqmssLO2ury5trOvrKilop6bmJSRjoqHg4B9eXZzb2xpZWJfW1hVUU5LR0RESEtOUlVYXF9jZmltcHN3en2BhIeLjpGVmJufoqWprK+ytrm7ubWyr6uopaGem5eUkY2Kh4OAfXl2c3BsaWZiX1xYVVJPS0hFRUhMT1JWWVxgY2ZpbXBzd3p9gYSHio6RlJibnqGlqKuvsrW4u7i1sa6rp6ShnpqXlJCNioeDgH16dnNwbGlmY19cWVZST0xJRUZJTFBTVlldYGNnam1wdHd6fYGEh4qOkZSXm56hpKerrrG0uLq3tLGtqqekoJ2al5OQjYqHg4B9enZzcG1pZmNgXVlWU1BNSUZHSk1QVFdaXWBkZ2ptcHR3en2BhIeKjZGUl5qdoaSnqq2wtLe5trOwraqmo6CdmpaTkI2KhoOAfXp3c3BtamdjYF1aV1RQTUpHR0tOUVRXWl5hZGdqbnF0d3p9gYSHio2Qk5eanaCjpqqtsLO2uLazr6yppqOgnJmWk5CNiYaDgH16d3NwbWpnZGFeWldUUU5LSEhLTlJVWFteYWRna25xdHd6fYGEh4qNkJOWmZ2go6aprK+ytbi1sq+sqKWin5yZlpOQjImGg4B9end0cW1qZ2RhXltYVVJPTEhJTE9SVVhbX2JlaGtucXR3en2BhIeKjZCTlpmcn6KlqKuvsrW3tLGuq6ilop+cmZWSj4yJhoOAfXp3dHFua2hlYl5bWFVST0xJSk1QU1ZZXF9iZWhrbnF0d3p9gISHio2Qk5aZnJ+ipairrrG0trSwraqnpKGem5iVko+MiYaDgH16d3RxbmtoZWJfXFlWU1BNSkpNUFNWWVxfYmVoa25xdHd6fYCDhomMj5KVmJueoaSnqq2ws7WzsK2qp6ShnpuYlZKPjImGg4B9end0cW5raGViX1xZV1RRTktLTlFUV1pdYGNmaWxvcnV4e36Ag4aJjI+SlZibnqGkp6qtsLK0sq+sqaajoJ2amJWSj4yJhoOAfXp3dHFubGlmY2BdWldUUU5LTE9SVVhbXWBjZmlsb3J1eHt+gIOGiYyPkpWYm52go6aprK+ytLGuq6mmo6CdmpeUkY6MiYaDgH16d3Ryb2xpZmNgXVtYVVJPTE1QUlVYW15hZGdpbG9ydXh7foCDhomMj5KUl5qdoKOmqKuusbOxrquopaKfnZqXlJGOi4mGg4B9end1cm9saWZkYV5bWFVTUE1NUFNWWVxeYWRnam1vcnV4e36Ag4aJjI+RlJeanZ+ipairrbCysK2qp6Win5yZlpSRjouIhoOAfXp4dXJvbGpnZGFeXFlWU1FOTlFUV1lcX2JlZ2ptcHJ1eHt+gIOGiYyOkZSXmZyfoqSnqq2vsa+sqqekoZ6cmZaTkY6LiIaDgH16eHVyb21qZ2RiX1xZV1RRT09SVFdaXV9iZWhqbXBzdXh7foCDhomLjpGUlpmcnqGkp6msr7GurKmmo6Gem5iWk5COi4iFg4B9e3h1cnBtamhlYl9dWldVUk9QUlVYW11gY2Voa21wc3Z4e36Ag4aIi46Rk5aZm56ho6apq66wrquopqOgnZuYlZOQjYuIhYOAfXt4dXNwbWtoZWNgXVtYVVNQUFNWWFteYGNmaGtucHN2eHt+gIOGiIuOkJOWmJudoKOlqKutr62qqKWioJ2amJWSkI2LiIWDgH17eHVzcG5raGZjYF5bWVZTUVFUVllcXmFkZmlrbnFzdnl7foCDhoiLjZCTlZianaCipaeqra6sqqekop+dmpeVkpCNioiFg4B9e3h2c3Bua2lmZGFeXFlXVFJSVFdaXF9hZGdpbG5xc3Z5e36Ag4WIi42QkpWXmp2foqSnqayuq6mmpKGfnJmXlJKPjYqIhYKAfXt4dnNxbmxpZ2RhX1xaV1VSU1VYWl1fYmRnamxvcXR2eXt+gIOFiIqNj5KUl5qcn6GkpqmrrauopqOhnpyZl5SSj4yKh4WCgH17eHZzcW5saWdkYl9dW1hWU1NWWFtdYGJlZ2psb3F0dnl7foCDhYiKjY+SlJeZnJ6go6Woqqyqp6WjoJ6bmZaUkY+MioeFgoB9e3l2dHFvbGpnZWJgXltZVlRUV1lcXmBjZWhqbW9ydHd5e36Ag4WIioyPkZSWmZudoKKlp6qrqaekop+dm5iWk5GOjIqHhYKAfnt5dnRxb21qaGVjYV5cWVdVVVdaXF9hY2Zoa21vcnR3eXt+gIOFh4qMj5GTlpibnZ+ipKapqqmmpKGfnZqYlZORjoyJh4WCgH57eXZ0cm9ta2hmY2FfXFpYVVZYWl1fYmRmaWttcHJ0d3l8foCDhYeKjI6Rk5WYmpyfoaOmqKqopaOhnpyal5WTkI6MiYeFgoB+e3l3dHJwbWtpZmRiX11bWFZWWVtdYGJkZ2lrbnBydXd5fH6Ag4WHiYyOkJOVl5qcnqCjpaepp6WioJ6bmZeVkpCOi4mHhIKAfnt5d3RycG5raWdkYmBeW1lXV1lcXmBjZWdpbG5wc3V3eXx+gIOFh4mMjpCSlZeZm56goqSnqKakoqCdm5mWlJKQjYuJh4SCgH57eXd1cnBubGlnZWNhXlxaWFhaXF9hY2VoamxucXN1d3p8foCChYeJi46QkpSWmZudn6Gkpqemo6GfnZqYlpSSj42LiYeEgoB+e3l3dXNwbmxqaGZjYV9dW1hZW11fYWRmaGpsb3FzdXd6fH6AgoWHiYuNj5KUlpianJ+ho6WnpaOgnpyamJaTkY+Ni4mGhIKAfnx5d3VzcW9samhmZGJgXVtZWVxeYGJkZmlrbW9xc3V4enx+gIKEh4mLjY+Rk5aYmpyeoKKkpqSioJ6cmZeVk5GPjYqIhoSCgH58end1c3FvbWtpZ2RiYF5cWlpcXmFjZWdpa21vcXR2eHp8foCChIaJi42PkZOVl5mbnaCipKWjoZ+dm5mXlZORjoyKiIaEgoB+fHp4dXNxb21raWdlY2FfXVtbXV9hY2VnaWxucHJ0dnh6fH6AgoSGiIqMj5GTlZeZm52foaOko6GfnJqYlpSSkI6MioiGhIKAfnx6eHZ0cnBubGpoZWNhX11bXF5gYmRmaGpsbnBydHZ4enx+gIKEhoiKjI6QkpSWmJqcnqCipKKgnpyamJaUkpCOjIqIhoSCgH58enh2dHJwbmxqaGZkYmBeXFxeYGJkZmhqbG5wcnR2eHp8foCChIaIioyOkJKUlpianJ6goaOhn52bmZeVk5GPjoyKiIaEgoB+fHp4dnRycG5samlnZWNhX11dX2FjZWdpa21vcXN1dnh6fH6AgoSGiIqMjpCRk5WXmZudn6GioJ+dm5mXlZORj42LiYeGhIKAfnx6eHZ0c3FvbWtpZ2VjYWBeXmBiZGZnaWttb3FzdXd5enx+gIKEhoiKi42PkZOVl5manJ6goaCenJqYlpSTkY+Ni4mHhYSCgH58enh3dXNxb21ramhmZGJgXl9hYmRmaGpsbm9xc3V3eXt8foCChIaHiYuNj5GSlJaYmpydn6GfnZuZmJaUkpCOjYuJh4WDgoB+fHp5d3VzcW9ubGpoZmVjYV9fYWNlZ2lqbG5wcnN1d3l7fH6AgoSFh4mLjY6QkpSWl5mbnZ+gnpybmZeVk5KQjoyLiYeFg4KAfnx6eXd1c3JwbmxraWdlY2JgYGJkZmdpa21ucHJ0dXd5e31+gIKEhYeJi4yOkJKTlZeZmpyen56cmpiXlZORj46MiomHhYOCgH58e3l3dXRycG5ta2loZmRiYWFjZGdpa21ucHJ0dnh6fH6AgYOFh4mLjY+QkpSWmJqcnp6cmpiWlJKRj42LiYeFg4KAfnx6eHZ1c3FvbWtpaGZkYmFjZWdpa2xucHJ0dnh6e31/gYOFhoiKjI6QkZOVl5mbnJ2cmpiWlJORj42LiYeGhIKAfn17eXd1c3JwbmxqaWdlY2JjZWdpa2xucHJ0dnd5e31/gIKEhoiJi42PkZKUlpiam52cmpiWlJORj42LioiGhIKBf317eXh2dHJxb21raWhmZGNkZWdpa2xucHJ0dXd5e3x+gIKDhYeJi4yOkJKTlZeZmpybmpiWlJORj42MioiGhIOBf358enh3dXNxcG5samlnZWRkZmdpa2xucHJzdXd5enx+gIGDhYaIioyNj5GSlJaXmZubmZiWlJKRj42MioiHhYOBgH58e3l3dnRycG9ta2poZmVkZmdpa21ucHJzdXd4enx9f4GChIaHiYuMjpCRk5WWmJqbmZeWlJKRj42MioiHhYOCgH59e3l4dnVzcXBubGtpZ2ZlZmhpa21ucHJzdXZ4ent9f4CChIWHiIqMjY+RkpSVl5mamZeWlJKRj42MiomHhYSCgH99fHp4d3V0cnBvbWxqaGdlZmhpa21ucHJzdXZ4ent9foCCg4WGiImLjY6QkZOVlpiZmZeVlJKRj42MiomHhoSCgX9+fHt5d3Z0c3Fwbm1raWhmZ2hqa21ucHFzdXZ4eXt8foCBg4SGh4mKjI2PkJKUlZeYmJeVlJKRj46MiomHhoSDgYB+fXt6eHd1c3Jwb21samlnZ2hqa21ucHFzdXZ4eXt8fn+BgoSFh4iKi42OkJGTlJaXmJeVlJKQj42MiomIhoWDgoB/fXx6eXd2dHNxcG5ta2poZ2lqbG1vcHJzdHZ3eXp8fX+AgoOFhoiJioyNj5CSk5WWl5aVk5KQj42Mi4mIhoWDgoB/fXx7eXh2dXNycW9ubGtpaGlqbG1vcHJzdHZ3eXp8fX6AgYOEhoeIiouNjo+RkpSVlpaVk5KQj42Mi4mIhoWEgoF/fn17enh3dnRzcXBvbWxqaWlrbG1vcHJzdHZ3eXp7fX6AgYKEhYaIiYuMjY+QkZOUlZaUk5GQj42Mi4mIhoWEgoGAfn18enl4dnVzcnFvbm1ramprbG5vcHJzdHZ3eHp7fH5/gYKDhYaHiYqLjY6PkJKTlJWUk5GQj42Mi4mIh4WEg4GAf318e3l4d3V0c3Jwb25sa2prbW5vcXJzdHZ3eHp7fH5/gIGDhIWHiImKjI2OkJGSk5SUkpGQjo2Mi4mIh4WEg4KAf358e3p5d3Z1dHJxcG9tbGtsbW5vcXJzdHZ3eHp7fH1/gIGChIWGh4mKi4yOj5CRkpSTkpGPjo2MiomIh4aEg4KBf359fHp5eHd2dHNycW9ubWxsbW5wcXJzdXZ3eHl7fH1+gIGCg4SGh4iJioyNjo+QkpOTkpCPjo2MiomIh4aEg4KBgH59fHt6eXd2dXRzcXBvbm1sbm9wcXJzdXZ3eHl7fH1+f4CCg4SFhoeJiouMjY6PkZKSkZCPjo2LiomIh4aFg4KBgH9+fHt6eXh3dnVzcnFwb25tbm9wcXJ0dXZ3eHl6fH1+f4CBgoOFhoeIiYqLjI2PkJGSkZCPjoyLiomIh4aFhIKBgH9+fXx7enh3dnV0c3JxcG9ubm9wcnN0dXZ3eHl6e31+f4CBgoOEhYaHiImLjI2Oj5CRkY+OjYyLiomIh4aFhIOBgH9+fXx7enl4d3Z1dHNycXBvb3BxcnN0dXZ3eHl6e3x9foCBgoOEhYaHiImKi4yNjo+QkI+OjYyLiomIh4aFhIOCgYB/fn18e3p5eHZ1dHNycXBvb3BxcnN0dXZ3eHl6e3x9fn+AgYKDhIWGh4iJiouMjY6PkI+OjYyLiomIh4aFhIOCgYB/fn18e3p5eHd2dXRzcnFwcHFycnN0dXZ3eHl6e3x9fn+AgYKDhIWGh4iJiYqLjI2Oj46NjIuKiYmIh4aFhIOCgYB/fn18e3p6eXh3dnV0c3JxcHFyc3R1dnd3eHl6e3x9fn+AgYKCg4SFhoeIiYqLi4yNjo6NjIuKiYiHh4aFhIOCgYB/fn59fHt6eXh3d3Z1dHNycXFyc3R1dnd4eXl6e3x9fn+AgIGCg4SFhoaHiImKi4yMjY2MjIuKiYiHhoaFhIOCgYCAf359fHt7enl4d3Z2dXRzcnJzdHR1dnd4eXl6e3x9fn5/gIGCg4OEhYaHiIiJiouMjI2Mi4qKiYiHhoWFhIOCgYGAf359fXx7enl5eHd2dXV0c3NzdHV2dnd4eXp6e3x9fn5/gIGBgoOEhYWGh4iIiYqLjIyMi4qJiIiHhoWFhIOCgoGAf35+fXx7e3p5eHh3dnV1dHN0dHV2d3d4eXp6e3x9fX5/gICBgoODhIWGhoeIiImKi4uLioqJiIeHhoWEhIOCgoGAf39+fX18e3p6eXh4d3Z1dXR0dXZ2d3h4eXp7e3x9fX5/gICBgoKDhISFhoaHiIiJiouLiomJiIeGhoWEhIOCgoGAgH9+fn18fHt6enl4eHd2dnV1dXZ3d3h5eXp7e3x9fX5/f4CBgYKDg4SFhYaGh4iIiYqKiYmIh4eGhoWEhIOCgoGAgH9+fn19fHt7enl5eHh3dnZ1dnZ3eHh5enp7e3x9fX5/f4CAgYKCg4OEhYWGhoeIiImJiYiIh4aGhYWEg4OCgoGAgH9/fn19fHx7e3p5eXh4d3d2dnd4eHl5enp7fHx9fX5/f4CAgYGCgoOEhIWFhoaHiIiJiIiHh4aGhYSEg4OCgoGBgH9/fn59fXx8e3t6eXl4eHd3d3d4eXl6ent7fHx9fX5+f4CAgYGCgoODhISFhYaGh4eIiIeHhoaFhYSEg4OCgoGBgIB/f35+fX18fHt7enp5eXh4d3h4eXl6ent7fHx9fX5+f3+AgIGBgoKDg4SEhYWGhoeHh4eGhoWFhISDg4KCgoGBgIB/f35+fX18fHx7e3p6eXl4eHh5eXp6e3t8fH19fX5+f3+AgIGBgYKCg4OEhIWFhYaGh4aGhYWEhISDg4KCgYGBgIB/f35+fn19fHx8e3t6enp5eXl5enp7e3x8fH19fn5+f3+AgICBgYKCgoODhISEhYWFhoaFhYSEhIODg4KCgYGBgIB/f39+fn59fXx8fHt7e3p6enp6ent7e3x8fX19fn5+f3+AgICBgYGCgoKDg4OEhISFhYWFhISEg4ODgoKCgYGBgICAf39/fn5+fX19fHx8e3t7enp7e3t8fHx9fX1+fn5+f39/gICAgYGBgoKCg4ODg4SEhISEhISDg4OCgoKBgYGAgICAf39/fn5+fn19fXx8fHx7e3t7e3x8fH19fX1+fn5/f39/gICAgIGBgYKCgoKDg4ODhISEg4ODg4KCgoGBgYGAgICAf39/f35+fn59fX19fHx8fHx8fHx8fX19fX5+fn5/f39/gICAgICBgYGBgoKCgoKDg4ODg4OCgoKCgYGBgYGAgICAf39/f39+fn5+fn19fX19fHx8fX19fX1+fn5+fn9/f39/gICAgICAgYGBgYGBgoKCgoKCgoKCgoGBgYGBgYCAgICAgH9/f39/f35+fn5+fn19fX19fX19fn5+fn5+f39/f39/f4CAgICAgICBgYGBgYGBgoKCgoGBgYGBgYGAgICAgICAgH9/f39/f39/fn5+fn5+fn5+fn5+fn5+fn9/f39/f39/f4CAgICAgICAgICBgYGBgYGBgYGBgYGAgICAgICAgICAgH9/f39/f39/f39/f39/fn5+fn5/f39/f39/f39/f39/f4CAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgH9/f39/f39/f39/f39/f39/f39/f39/f39/f39/f39/f4CAgICAgICAgICAgICAgICAgICAgICAgICAgICA");
                        //playAudio("data:audio/wav;base64,UklGRtEaAABXQVZFZm10IBAAAAABAAEARKwAAESsAAABAAgAZGF0Ya0aAAAAPUFFSU1RVVldYWVpbXF1eX2BhYmNkZWZnaGkqKywtLi8wMTHxMC8uLSwrKikoJyYlJCMiISAfHh0cGxoZWFdWVVRTUlFQT05Oj5CRkpOUVVZXWFlaW1xdXl9gYWJjZCUmJygpKissLS4vL/DxsO/u7ezr6uno6CcmJSQjIiEgHx4dHFtaWVhXVlVUU1KRkI+Ojs+QkZKTlJWWl5iZmltcXV5fYGFiYyQlJicoKSoq6+zt7u/w8XCvrq2s6+rp6Ofm5eUkIyIhIB8eHVxbWllYV1aVlJOSkZCPzs7P0NHS09SVlpeYmZqbnF1eX2BhYiMkJSYnJ+jp6uvs7a6vsLFwb66trKuqqajn5uXk4+MiISAfHl1cW1pZWJeWlZST0tHQz88PEBESEtPU1dbXmJmam5ydXl9gYWIjJCUmJufo6eqrrK2ur3BxMG9ubWxrqqmop6bl5OPjIiEgHx5dXFtaWZiXlpXU09LSERAPD1BREhMUFNXW19jZmpucnV5fYGEiIyQlJebn6Omqq6xtbm9wMPAvLi1sa2ppqKempeTj4uIhIB8eXVxbWpmYl9bV1NQTEhEQT0+QUVJTVBUWFtfY2dqbnJ2eX2BhIiMkJOXm56ipqqtsbW4vMDCv7u4tLCtqaWhnpqWk4+LiISAfHl1cW5qZmNfW1hUUE1JRUE+PkJGSU1RVFhcYGNna25ydnl9gYSIjI+Tl5qeoqWprbC0uLu/wb67t7OwrKiloZ2alpKPi4eEgHx5dXJuamdjX1xYVFFNSUZCPz9DRkpOUVVZXGBkZ2tucnZ5fYGEiIyPk5aanqGlqayws7e7vsG+urazr6yopKGdmZaSj4uHhIB9eXVybmpnY2BcWFVRTkpHQz9AQ0dLTlJVWV1gZGhrb3J2eX2BhIiLj5OWmp2hpaisr7O2ur3Avbm2sq+rp6SgnZmWko6Lh4SAfXl1cm5rZ2RgXFlVUk5LR0RAQURIS09SVlpdYWRoa29ydnp9gYSIi4+SlpmdoaSoq6+ytrm9v7y5tbKuq6ejoJyZlZKOi4eEgH15dnJua2dkYF1ZVlJPS0hEQUFFSExPU1ZaXmFlaGxvc3Z6fYGEiIuPkpaZnaCkp6uusrW5vL68uLWxrqqno6CcmZWSjouHhIB9eXZyb2toZGFdWlZTT0xJRUJCRklNUFNXWl5hZWhsb3N2en2BhIiLjpKVmZygo6eqrrG0uLu+u7e0sK2qpqOfnJiVkY6Kh4SAfXl2cm9raGVhXlpXU1BNSUZCQ0ZKTVFUV1teYmVpbG9zdnp9gYSHi46SlZmcn6Omqq2wtLe7vbq3s7Csqaain5uYlZGOioeDgH15dnNvbGhlYl5bV1RRTUpHQ0RHSk5RVVhbX2JmaWxwc3Z6fYGEh4uOkZWYnJ+ipqmssLO2ury5trOvrKilop6bmJSRjoqHg4B9eXZzb2xpZWJfW1hVUU5LR0RESEtOUlVYXF9jZmltcHN3en2BhIeLjpGVmJufoqWprK+ytrm7ubWyr6uopaGem5eUkY2Kh4OAfXl2c3BsaWZiX1xYVVJPS0hFRUhMT1JWWVxgY2ZpbXBzd3p9gYSHio6RlJibnqGlqKuvsrW4u7i1sa6rp6ShnpqXlJCNioeDgH16dnNwbGlmY19cWVZST0xJRUZJTFBTVlldYGNnam1wdHd6fYGEh4qOkZSXm56hpKerrrG0uLq3tLGtqqekoJ2al5OQjYqHg4B9enZzcG1pZmNgXVlWU1BNSUZHSk1QVFdaXWBkZ2ptcHR3en2BhIeKjZGUl5qdoaSnqq2wtLe5trOwraqmo6CdmpaTkI2KhoOAfXp3c3BtamdjYF1aV1RQTUpHR0tOUVRXWl5hZGdqbnF0d3p9gYSHio2Qk5eanaCjpqqtsLO2uLazr6yppqOgnJmWk5CNiYaDgH16d3NwbWpnZGFeWldUUU5LSEhLTlJVWFteYWRna25xdHd6fYGEh4qNkJOWmZ2go6aprK+ytbi1sq+sqKWin5yZlpOQjImGg4B9end0cW1qZ2RhXltYVVJPTEhJTE9SVVhbX2JlaGtucXR3en2BhIeKjZCTlpmcn6KlqKuvsrW3tLGuq6ilop+cmZWSj4yJhoOAfXp3dHFua2hlYl5bWFVST0xJSk1QU1ZZXF9iZWhrbnF0d3p9gISHio2Qk5aZnJ+ipairrrG0trSwraqnpKGem5iVko+MiYaDgH16d3RxbmtoZWJfXFlWU1BNSkpNUFNWWVxfYmVoa25xdHd6fYCDhomMj5KVmJueoaSnqq2ws7WzsK2qp6ShnpuYlZKPjImGg4B9end0cW5raGViX1xZV1RRTktLTlFUV1pdYGNmaWxvcnV4e36Ag4aJjI+SlZibnqGkp6qtsLK0sq+sqaajoJ2amJWSj4yJhoOAfXp3dHFubGlmY2BdWldUUU5LTE9SVVhbXWBjZmlsb3J1eHt+gIOGiYyPkpWYm52go6aprK+ytLGuq6mmo6CdmpeUkY6MiYaDgH16d3Ryb2xpZmNgXVtYVVJPTE1QUlVYW15hZGdpbG9ydXh7foCDhomMj5KUl5qdoKOmqKuusbOxrquopaKfnZqXlJGOi4mGg4B9end1cm9saWZkYV5bWFVTUE1NUFNWWVxeYWRnam1vcnV4e36Ag4aJjI+RlJeanZ+ipairrbCysK2qp6Win5yZlpSRjouIhoOAfXp4dXJvbGpnZGFeXFlWU1FOTlFUV1lcX2JlZ2ptcHJ1eHt+gIOGiYyOkZSXmZyfoqSnqq2vsa+sqqekoZ6cmZaTkY6LiIaDgH16eHVyb21qZ2RiX1xZV1RRT09SVFdaXV9iZWhqbXBzdXh7foCDhomLjpGUlpmcnqGkp6msr7GurKmmo6Gem5iWk5COi4iFg4B9e3h1cnBtamhlYl9dWldVUk9QUlVYW11gY2Voa21wc3Z4e36Ag4aIi46Rk5aZm56ho6apq66wrquopqOgnZuYlZOQjYuIhYOAfXt4dXNwbWtoZWNgXVtYVVNQUFNWWFteYGNmaGtucHN2eHt+gIOGiIuOkJOWmJudoKOlqKutr62qqKWioJ2amJWSkI2LiIWDgH17eHVzcG5raGZjYF5bWVZTUVFUVllcXmFkZmlrbnFzdnl7foCDhoiLjZCTlZianaCipaeqra6sqqekop+dmpeVkpCNioiFg4B9e3h2c3Bua2lmZGFeXFlXVFJSVFdaXF9hZGdpbG5xc3Z5e36Ag4WIi42QkpWXmp2foqSnqayuq6mmpKGfnJmXlJKPjYqIhYKAfXt4dnNxbmxpZ2RhX1xaV1VSU1VYWl1fYmRnamxvcXR2eXt+gIOFiIqNj5KUl5qcn6GkpqmrrauopqOhnpyZl5SSj4yKh4WCgH17eHZzcW5saWdkYl9dW1hWU1NWWFtdYGJlZ2psb3F0dnl7foCDhYiKjY+SlJeZnJ6go6Woqqyqp6WjoJ6bmZaUkY+MioeFgoB9e3l2dHFvbGpnZWJgXltZVlRUV1lcXmBjZWhqbW9ydHd5e36Ag4WIioyPkZSWmZudoKKlp6qrqaekop+dm5iWk5GOjIqHhYKAfnt5dnRxb21qaGVjYV5cWVdVVVdaXF9hY2Zoa21vcnR3eXt+gIOFh4qMj5GTlpibnZ+ipKapqqmmpKGfnZqYlZORjoyJh4WCgH57eXZ0cm9ta2hmY2FfXFpYVVZYWl1fYmRmaWttcHJ0d3l8foCDhYeKjI6Rk5WYmpyfoaOmqKqopaOhnpyal5WTkI6MiYeFgoB+e3l3dHJwbWtpZmRiX11bWFZWWVtdYGJkZ2lrbnBydXd5fH6Ag4WHiYyOkJOVl5qcnqCjpaepp6WioJ6bmZeVkpCOi4mHhIKAfnt5d3RycG5raWdkYmBeW1lXV1lcXmBjZWdpbG5wc3V3eXx+gIOFh4mMjpCSlZeZm56goqSnqKakoqCdm5mWlJKQjYuJh4SCgH57eXd1cnBubGlnZWNhXlxaWFhaXF9hY2VoamxucXN1d3p8foCChYeJi46QkpSWmZudn6Gkpqemo6GfnZqYlpSSj42LiYeEgoB+e3l3dXNwbmxqaGZjYV9dW1hZW11fYWRmaGpsb3FzdXd6fH6AgoWHiYuNj5KUlpianJ+ho6WnpaOgnpyamJaTkY+Ni4mGhIKAfnx5d3VzcW9samhmZGJgXVtZWVxeYGJkZmlrbW9xc3V4enx+gIKEh4mLjY+Rk5aYmpyeoKKkpqSioJ6cmZeVk5GPjYqIhoSCgH58end1c3FvbWtpZ2RiYF5cWlpcXmFjZWdpa21vcXR2eHp8foCChIaJi42PkZOVl5mbnaCipKWjoZ+dm5mXlZORjoyKiIaEgoB+fHp4dXNxb21raWdlY2FfXVtbXV9hY2VnaWxucHJ0dnh6fH6AgoSGiIqMj5GTlZeZm52foaOko6GfnJqYlpSSkI6MioiGhIKAfnx6eHZ0cnBubGpoZWNhX11bXF5gYmRmaGpsbnBydHZ4enx+gIKEhoiKjI6QkpSWmJqcnqCipKKgnpyamJaUkpCOjIqIhoSCgH58enh2dHJwbmxqaGZkYmBeXFxeYGJkZmhqbG5wcnR2eHp8foCChIaIioyOkJKUlpianJ6goaOhn52bmZeVk5GPjoyKiIaEgoB+fHp4dnRycG5samlnZWNhX11dX2FjZWdpa21vcXN1dnh6fH6AgoSGiIqMjpCRk5WXmZudn6GioJ+dm5mXlZORj42LiYeGhIKAfnx6eHZ0c3FvbWtpZ2VjYWBeXmBiZGZnaWttb3FzdXd5enx+gIKEhoiKi42PkZOVl5manJ6goaCenJqYlpSTkY+Ni4mHhYSCgH58enh3dXNxb21ramhmZGJgXl9hYmRmaGpsbm9xc3V3eXt8foCChIaHiYuNj5GSlJaYmpydn6GfnZuZmJaUkpCOjYuJh4WDgoB+fHp5d3VzcW9ubGpoZmVjYV9fYWNlZ2lqbG5wcnN1d3l7fH6AgoSFh4mLjY6QkpSWl5mbnZ+gnpybmZeVk5KQjoyLiYeFg4KAfnx6eXd1c3JwbmxraWdlY2JgYGJkZmdpa21ucHJ0dXd5e31+gIKEhYeJi4yOkJKTlZeZmpyen56cmpiXlZORj46MiomHhYOCgH58e3l3dXRycG5ta2loZmRiYWFjZGdpa21ucHJ0dnh6fH6AgYOFh4mLjY+QkpSWmJqcnp6cmpiWlJKRj42LiYeFg4KAfnx6eHZ1c3FvbWtpaGZkYmFjZWdpa2xucHJ0dnh6e31/gYOFhoiKjI6QkZOVl5mbnJ2cmpiWlJORj42LiYeGhIKAfn17eXd1c3JwbmxqaWdlY2JjZWdpa2xucHJ0dnd5e31/gIKEhoiJi42PkZKUlpiam52cmpiWlJORj42LioiGhIKBf317eXh2dHJxb21raWhmZGNkZWdpa2xucHJ0dXd5e3x+gIKDhYeJi4yOkJKTlZeZmpybmpiWlJORj42MioiGhIOBf358enh3dXNxcG5samlnZWRkZmdpa2xucHJzdXd5enx+gIGDhYaIioyNj5GSlJaXmZubmZiWlJKRj42MioiHhYOBgH58e3l3dnRycG9ta2poZmVkZmdpa21ucHJzdXd4enx9f4GChIaHiYuMjpCRk5WWmJqbmZeWlJKRj42MioiHhYOCgH59e3l4dnVzcXBubGtpZ2ZlZmhpa21ucHJzdXZ4ent9f4CChIWHiIqMjY+RkpSVl5mamZeWlJKRj42MiomHhYSCgH99fHp4d3V0cnBvbWxqaGdlZmhpa21ucHJzdXZ4ent9foCCg4WGiImLjY6QkZOVlpiZmZeVlJKRj42MiomHhoSCgX9+fHt5d3Z0c3Fwbm1raWhmZ2hqa21ucHFzdXZ4eXt8foCBg4SGh4mKjI2PkJKUlZeYmJeVlJKRj46MiomHhoSDgYB+fXt6eHd1c3Jwb21samlnZ2hqa21ucHFzdXZ4eXt8fn+BgoSFh4iKi42OkJGTlJaXmJeVlJKQj42MiomIhoWDgoB/fXx6eXd2dHNxcG5ta2poZ2lqbG1vcHJzdHZ3eXp8fX+AgoOFhoiJioyNj5CSk5WWl5aVk5KQj42Mi4mIhoWDgoB/fXx7eXh2dXNycW9ubGtpaGlqbG1vcHJzdHZ3eXp8fX6AgYOEhoeIiouNjo+RkpSVlpaVk5KQj42Mi4mIhoWEgoF/fn17enh3dnRzcXBvbWxqaWlrbG1vcHJzdHZ3eXp7fX6AgYKEhYaIiYuMjY+QkZOUlZaUk5GQj42Mi4mIhoWEgoGAfn18enl4dnVzcnFvbm1ramprbG5vcHJzdHZ3eHp7fH5/gYKDhYaHiYqLjY6PkJKTlJWUk5GQj42Mi4mIh4WEg4GAf318e3l4d3V0c3Jwb25sa2prbW5vcXJzdHZ3eHp7fH5/gIGDhIWHiImKjI2OkJGSk5SUkpGQjo2Mi4mIh4WEg4KAf358e3p5d3Z1dHJxcG9tbGtsbW5vcXJzdHZ3eHp7fH1/gIGChIWGh4mKi4yOj5CRkpSTkpGPjo2MiomIh4aEg4KBf359fHp5eHd2dHNycW9ubWxsbW5wcXJzdXZ3eHl7fH1+gIGCg4SGh4iJioyNjo+QkpOTkpCPjo2MiomIh4aEg4KBgH59fHt6eXd2dXRzcXBvbm1sbm9wcXJzdXZ3eHl7fH1+f4CCg4SFhoeJiouMjY6PkZKSkZCPjo2LiomIh4aFg4KBgH9+fHt6eXh3dnVzcnFwb25tbm9wcXJ0dXZ3eHl6fH1+f4CBgoOFhoeIiYqLjI2PkJGSkZCPjoyLiomIh4aFhIKBgH9+fXx7enh3dnV0c3JxcG9ubm9wcnN0dXZ3eHl6e31+f4CBgoOEhYaHiImLjI2Oj5CRkY+OjYyLiomIh4aFhIOBgH9+fXx7enl4d3Z1dHNycXBvb3BxcnN0dXZ3eHl6e3x9foCBgoOEhYaHiImKi4yNjo+QkI+OjYyLiomIh4aFhIOCgYB/fn18e3p5eHZ1dHNycXBvb3BxcnN0dXZ3eHl6e3x9fn+AgYKDhIWGh4iJiouMjY6PkI+OjYyLiomIh4aFhIOCgYB/fn18e3p5eHd2dXRzcnFwcHFycnN0dXZ3eHl6e3x9fn+AgYKDhIWGh4iJiYqLjI2Oj46NjIuKiYmIh4aFhIOCgYB/fn18e3p6eXh3dnV0c3JxcHFyc3R1dnd3eHl6e3x9fn+AgYKCg4SFhoeIiYqLi4yNjo6NjIuKiYiHh4aFhIOCgYB/fn59fHt6eXh3d3Z1dHNycXFyc3R1dnd4eXl6e3x9fn+AgIGCg4SFhoaHiImKi4yMjY2MjIuKiYiHhoaFhIOCgYCAf359fHt7enl4d3Z2dXRzcnJzdHR1dnd4eXl6e3x9fn5/gIGCg4OEhYaHiIiJiouMjI2Mi4qKiYiHhoWFhIOCgYGAf359fXx7enl5eHd2dXV0c3NzdHV2dnd4eXp6e3x9fn5/gIGBgoOEhYWGh4iIiYqLjIyMi4qJiIiHhoWFhIOCgoGAf35+fXx7e3p5eHh3dnV1dHN0dHV2d3d4eXp6e3x9fX5/gICBgoODhIWGhoeIiImKi4uLioqJiIeHhoWEhIOCgoGAf39+fX18e3p6eXh4d3Z1dXR0dXZ2d3h4eXp7e3x9fX5/gICBgoKDhISFhoaHiIiJiouLiomJiIeGhoWEhIOCgoGAgH9+fn18fHt6enl4eHd2dnV1dXZ3d3h5eXp7e3x9fX5/f4CBgYKDg4SFhYaGh4iIiYqKiYmIh4eGhoWEhIOCgoGAgH9+fn19fHt7enl5eHh3dnZ1dnZ3eHh5enp7e3x9fX5/f4CAgYKCg4OEhYWGhoeIiImJiYiIh4aGhYWEg4OCgoGAgH9/fn19fHx7e3p5eXh4d3d2dnd4eHl5enp7fHx9fX5/f4CAgYGCgoOEhIWFhoaHiIiJiIiHh4aGhYSEg4OCgoGBgH9/fn59fXx8e3t6eXl4eHd3d3d4eXl6ent7fHx9fX5+f4CAgYGCgoODhISFhYaGh4eIiIeHhoaFhYSEg4OCgoGBgIB/f35+fX18fHt7enp5eXh4d3h4eXl6ent7fHx9fX5+f3+AgIGBgoKDg4SEhYWGhoeHh4eGhoWFhISDg4KCgoGBgIB/f35+fX18fHx7e3p6eXl4eHh5eXp6e3t8fH19fX5+f3+AgIGBgYKCg4OEhIWFhYaGh4aGhYWEhISDg4KCgYGBgIB/f35+fn19fHx8e3t6enp5eXl5enp7e3x8fH19fn5+f3+AgICBgYKCgoODhISEhYWFhoaFhYSEhIODg4KCgYGBgIB/f39+fn59fXx8fHt7e3p6enp6ent7e3x8fX19fn5+f3+AgICBgYGCgoKDg4OEhISFhYWFhISEg4ODgoKCgYGBgICAf39/fn5+fX19fHx8e3t7enp7e3t8fHx9fX1+fn5+f39/gICAgYGBgoKCg4ODg4SEhISEhISDg4OCgoKBgYGAgICAf39/fn5+fn19fXx8fHx7e3t7e3x8fH19fX1+fn5/f39/gICAgIGBgYKCgoKDg4ODhISEg4ODg4KCgoGBgYGAgICAf39/f35+fn59fX19fHx8fHx8fHx8fX19fX5+fn5/f39/gICAgICBgYGBgoKCgoKDg4ODg4OCgoKCgYGBgYGAgICAf39/f39+fn5+fn19fX19fHx8fX19fX1+fn5+fn9/f39/gICAgICAgYGBgYGBgoKCgoKCgoKCgoGBgYGBgYCAgICAgH9/f39/f35+fn5+fn19fX19fX19fn5+fn5+f39/f39/f4CAgICAgICBgYGBgYGBgoKCgoGBgYGBgYGAgICAgICAgH9/f39/f39/fn5+fn5+fn5+fn5+fn5+fn9/f39/f39/f4CAgICAgICAgICBgYGBgYGBgYGBgYGAgICAgICAgICAgH9/f39/f39/f39/f39/fn5+fn5/f39/f39/f39/f39/f4CAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgH9/f39/f39/f39/f39/f39/f39/f39/f39/f39/f39/f4CAgICAgICAgICAgICAgICAgICAgICAgICAgICA");
                    }
                );
            }
            */

            function playAudio(url) {
                var audio = new Audio(url);
                audio.play();
            }
            function executeWithMinimumDelay(activity, minimumDelay, postActivity) {
                var minimumDelay = new Promise(
                    (resolve, reject) => {
                        setTimeout(() => {resolve()}, minimumDelay);
                    }
                );
                Promise.all([activity, minimumDelay]).then(
                    (result) => {
                        if (postActivity) {
                            postActivity(result[0]);
                        }
                    }
                )
            }
        </script>
        <script>
            var monster_list = {
            }
            var weapon_list = {
                "madPancake": {
                    "spriteSheet": "madPancakeSpriteSheet.png",
                    "occurrence": [],
                    "treasure": {
                        "min": 0,
                        "max": 3
                    },
                    "idleMotion": {
                        "motionSequence": [
                            {
                                "frame": 0,
                                "durationMs": 100
                            }
                        ]
                    }
                }
            }
            var item_list = {

            }
            //console.log("Hello, again!");
        </script>
    </head>
    <body>
        Hello!
        <div>
            <div id="phaser-target" />
        </div>
        Goodbye!
        <br />
        <img src="Untitled.png" />
    </body>
</html>
```

### Run and Test Web Page Locally

Go to the directory where the sprite sheet image and the web (HTML) page are,
then run the following command to start a local web server.

```
python -m SimpleHTTPServer 9090
```

Open a browser and go to `http://localhost:9090/sampleSpriteSheet1.html` .

#### Why Does a Web Server Need to Be Run?

Even though the sprite sheet image and the web (HTML) page are in the same directory,
the Phaser JS library tries to load image files (like the sprite sheet) by making
an HTTP call. This call will fail with a CORS error unless the web page is hosted
on a web server.