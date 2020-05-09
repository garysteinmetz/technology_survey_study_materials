# I Can Run a Web Application from a Container in the Cloud

## Docker

Docker allows you to simulate a machine within a machine. It's similar to other
`virtual machine` technology but isn't as resource-intensive.

Just as Java acts as an intermediary between compiled programs and your computer,
Docker acts as an intermediary between simulated operating systems (known as `containers`)
and your computers. `Images` (each one defined by a `Dockerfile`) acts as a blueprint
for the setup and starting state of each container.

Just as `Spring Boot` can create a `fat JAR` to represent all components needed to run
a single application in Java, an image contains all components needed to run
a virtual operating system on Docker.

Docker is a very important technology in cloud computing. Since using cloud technologies
means not directly interfacing with computer hardware, a Docker image instructs the cloud
how to start a virtual machine. Docker provides these major advantages.

  - `Consistent` - The container that results from the image will always be
  the same. By defining the image specification in a Dockerfile, much less (if anything)
  is left to chance in comparison to manual configuration. Dockerfiles can be reviewed
  and committed to source control just like any other source file (`configuration as code`).
  - `Standardized` - https://hub.docker.com/ contains an deep library with an extensive
  selection of common operating systems (like Debian and Alpine Linux) and applications
  (like Redis for common in-memory caching of session data, or R for data science).
  - `Easy to Replace` - Docker containers can be stopped and relaunch without restarting
  the physical computer. If a container starts acting incorrectly (like due to a memory leak),
  it's easy to stop it and start again.
  - `Scalable` - With the image's able to easily define a container, the image can create
  many more containers which can be important if (for instance) a web site is experiencing
  increased traffic. In this case, AWS can create more containers to support the traffic.

### Installing Docker

If Docker Toolbox (meant for older computers) is already installed on your system,
you can either just keep that or uninstall it and follow these instructions.

Go to the Docker website at https://hub.docker.com/search?q=&type=edition&offering=community
to download the 'community' (free) edition of Docker. Specifically, go to one of these URLs.

Note - For Windows, either 'Pro' or 'Enterprise' edition of Windows 10 or greater is required
to install this version of Docker, older or less capable versions (like 'Home') should be able
to run Docker Toolbox instead.

  - Windows - https://hub.docker.com/editions/community/docker-ce-desktop-windows
  - Mac - https://hub.docker.com/editions/community/docker-ce-desktop-mac

#### For Windows, Enable Virtualization
Some Windows systems won't run Docker unless the `virtualization`
capability is enabled in the `BIOS` (hardware-to-OS settings).

Enable virtualization with the following steps.

(Source - https://www.youtube.com/watch?v=g8-go0RFPjc
('How to access bios and enable intel virtualization technology
(VT-X/AMD-v) on Windows 10'))

1) In the lower-left corner of the Windows desktop, click the search icon,
enter 'bio' and select 'Change advanced startup options'
2) Click the 'Restart now' button
3) Click the 'Troubleshoot' icon
4) Click the 'Advanced options' icon
5) (Be careful here) Click the 'UEFI Firmware Settings' icon
6) Click the 'Restart' button
7) The computer will now restart
8) Press the 'F10' key
9) Press the right arrow to go to 'Security Configuration'
10) Press the down arrow to go to 'Virtualization Technology'
11) If not set already, set this value to '<Enabled>'
(press 'Enter', use arrows to select 'Enabled', then press 'Enter' again)
12) Press the right arrow to go to 'Exit'
13) Select the 'Exit Saving Changes' option, press 'Enter',
then press 'Enter' over the '[Yes]' option in the 'Exit Saving Changes?' menu

### Basic Docker Commands

For the following subsections, run the associate commands from the command line.

#### Get a Docker Image

Run the following command to get (but not run) the `hello-world` image from Docker Hub
(https://hub.docker.com/_/hello-world).

```
docker pull hello-world
```

Run the following command to list all downloaded images and notice that 'hello-world'
is listed under the 'REPOSITORY' column. Note the 'IMAGE ID' value for this image.

#### Run a Docker Container

Using 'IMAGE ID' value you recorded in the previous step ('bf756fb1ae65' will be used here
_but you need to replace that value with whatever value your recorded_), run the following.

```
docker run bf756fb1ae65
```

About 20 new lines of output will be displayed, one of which is 'Hello from Docker!'

#### Check the Status of a Docker Container

Run the following command to list which Docker containers are running or have run.

```
docker ps -a
```

Note that one of the entries contains the same 'IMAGE ID' that you recorded above.
Record the 'CONTAINER ID' for this entry.

#### Stop a Docker Container

Using the 'IMAGE ID' value you recorded in the previous step ('4b9a7a484712' will be used here
_but you need to replace that value with whatever value your recorded_), run the following.

```
docker stop 4b9a7a484712
```

Note that for this case ('hello-world'), the container was already stopped before running
this command, but if the container were a continuously-running web server that server would
stop. (Replace the `stop` keyword with `kill` to abruptly terminate a running container.)

#### Remove a Docker Container
Remove a stopped container with the 'rm' command, like here.

```
docker rm 4b9a7a484712
```

That container will no longer appear when 'docker ps -a' is run.

#### Remove a Docker Image

The 'rmi' command is used to remove Docker images.

```
docker rmi bf756fb1ae65
```

That container will no longer appear when 'docker images' is run.

### Unix

It's easy to download a Docker image for Unix which makes this a good time to review Unix.
Unix (more specifically, Linux) is used _most everywhere_ in the Internet.

Alpine Linux is a popular operating system for a Docker image because it's relatively small.

#### Pull Alpine Linux Docker Image

Download the Alpine Linux image into Docker with this command.

```
docker pull alpine
```

Again, use 'docker images' to record the 'IMAGE ID' of the image.

#### Go into Command Prompt of Container

Start the Alpine Linux container and run the command prompt using the 'sh' (shell) command.
'f70734b6a266' is used here for the 'IMAGE ID' but put the correct value.

```
docker run -it f70734b6a266 sh
```

You are now in a shell (command prompt) of this running Alpine Linux container and can run
Unix commands in it.

##### Unix - Users, Groups, and Permissions

To find out who you logged in as, run the following command.

```
whoami
```

This command should have printed `root` which is the most powerful user on a Unix system.
`root` can do _anything_. In fact, `root` is so powerful (and dangerous) that users rarely
operate in a shell as this user. To have the privileges of `root` when running a single command
without being `root`, users can use the `sudo` command which allows a user to run a command
with `root` privileges.

Files and directories assign `read, write, and execute privileges` to files. Such privileges
are assigned to owner, members of the owner's group, and everyone else.

List the files in a directory with the `ls` command, but the `ls -la` command also lists
the permissions of the file. Here's the output of that command from the current directory.

```
drwxr-xr-x    1 root     root          4096 Apr 23 06:25 usr
```

The 'd' means that 'usr' is a directory. The first 'root' means that user 'root' is the owner
and the second 'root' means that this file belongs to the 'root' group.

The 'rwx' means that the 'root' user can read, write, and execute the directory.
The first 'r-x' means that members of the 'root' group can only read or execute the directory.
The second 'r-x' means that anyone else can only read or execute the directory.

The `chmod` command changes the permissions on a file or directory.

##### Unix - Files and Directories

As mentioned, the `ls` command is used to list files. Here are other file commands.

`pwd` lists the current directory.

`cd` is used to change to another directory. Here are examples.
  - `cd /` - Go to the base directory of the operating system.
  - `cd ~` - Go to the user's home directory (which is '/root' for user 'root').
  - `cd .` - Go to the current directory (don't change directories).
  - `cd ..` - Go to the parent directory of this directory. (For user 'root', 'cd ~'
  followed by 'cd ..' will just take the user back to the '/' directory which is just
  equivalent to entering 'cd /').

Create a directory with the `mkdir` command and remove a file or a directory with the
`rm` command. Move files with the `mv` command.

`cat` displays the contents of a file. The '/root/.ash_history' file lists all of the recent
commands entered on the command line. `cat /root/.ash_history` lists out all of them.
By the way, the `history` command does the same thing.

`find` lists all of the files in a directory and subdirectories.
`find /` will list every file on the system (so long as the user has access to them).


##### Unix - 'Echo' Command, Environment Variables, and Appending Console Output to Files

`echo` just prints what is typed to the console. `echo Hello` will print 'Hello'
to the console.

_Environment variables are a set of string key-value pairs. They help configure
the system and (this is important) act as switches to vary the behavior of an application
or Docker image without otherwise changing the source code. For instance,
if an application is identical on a development server and a production server,
but they use separate backend databases, they could/would use identical source code
but could set a different environment variable for the URL of their respective databases._

Type the `export` command to list the environment variables. Notice how `HOME`
has a value of `/root` - that's how `cd ~` knows to go to that directory. That `HOME` value
is specific to each user.

`export` can also be used to set a value. `export FOOD=pizza` will set the `FOOD` environment
variable to `pizza` . In string declarations (encased in double quotes), the `${}` notation
can be used to substitute an environment variable value into the string. Here is an example.
```
/ # export FOOD=pizza
/ # echo "My favorite food is ${FOOD}"
My favorite food is pizza
/ # 
```

The `unset` command removes an environment variable.

`>` overrides the content of an existing file (or creates a new one) with console output.

```
/ # echo Hello > someFile.txt
/ # cat someFile.txt 
Hello
```

`>>` appends content to the end of a file (or creates a new one) with console output.

```
/ # echo Goodbye >> someFile.txt
/ # cat someFile.txt 
Hello
Goodbye
```

The `grep` command scans output and only prints those lines that match a pattern.
Patterns can include `regular expressions` .
The `|` (pipe) character is used to route output from one command to another in Unix.
This example outputs file content that is then piped to `grep` to examine. This technique
is very useful when looking at logs.

```
/ # cat someFile.txt | grep oo
Goodbye
```

##### Unix - Viewing and Editing File Contents
`head` outputs the first lines of a file.
```
/ # head -1 someFile.txt 
Hello
```

`tail` outputs the last lines of a file.
```
/ # tail -1 someFile.txt 
Goodbye
```

`vi` is a ubiquitous text editor for Unix. It is _very powerful_ but is also _very unintuitive_.
`vi` does not use a mouse and has three different modes of operation.

  - Command Mode - Do something with the file without directly typing in new text.
  - Insert Mode - Edit the exiting file character by character.
  - Last Edit Mode - Save the file, exit the file, or similar high-level action.

When `vi` first loads, it is in 'Command Mode' . To switch to 'Insert Mode' type either
'a' (append - place cursor after highlighted character)
or 'i' (insert - leave cursor where it is). To switch to 'Last Edit Mode' press ':' (colon).

To go back to 'Command Mode' from the other two modes, press 'esc' (escape).

In 'Command Mode', here are some of the other commands.

  - `/ <search_string>` searches for the next occurrence of a string after the cursor.
  Press enter after entering the command.
  - `Control-F` (forward) page down.
  - `Control-B` (back) page up.

In 'Last Edit Mode', here are some of the commands. Press enter after each command.
  - `w <filename>` saves the file with that name. Omit '<filename>' to just overwrite file.
  - `q` quit out of `vi` .
  - `set nu` list the file numbers.

##### Unix - Processes
Programs (processes) can be easily tracked in Unix. The `top` commands gives a good summary
of the processes including processor and memory usage (press 'q' to exit).

`ps -aef` also prints a table of processes including their process IDs ('PID') which is
useful for killing of processes that should be terminated (but haven't done so already).

Usually, when running a Unix command is runs in the foreground and you can't type
any new commands until the command's associated process ends (which can usually be done
by pressing `Control-C`). To make a process run in the background, append the `&` character
to the end of the command. Running a process in the background allows you to do other
things while the process is running.

The following example runs `vi` in the background (there is no real reason to ever
run `vi` in the background but it will simulate a stalled process), gets its 'PID' using
`ps`, and then kills that process using the `kill -9` command (the '-9' means to stop
the process without delay).

```
/ # vi &
/ # ps -aef
PID   USER     TIME  COMMAND
    1 root      0:00 sh
   28 root      0:00 vi
   29 root      0:00 ps -aef
[1]+  Stopped (tty output)       vi
/ # kill -9 28
/ # ps -aef
PID   USER     TIME  COMMAND
    1 root      0:00 sh
   30 root      0:00 ps -aef
[1]+  Killed                     vi
/ # 
```

##### Unix - Networking

Unix contains networking commands that are useful for things like figuring out
a machines (really network card) IP address. `ifconfig -a` will list network configurations.

The `/etc/hosts` file lists DNS overrides. Sometimes it's useful to substitute an actual
website (like 'www.google.com') with a mock website for testing purposes. Note that
this is the file where 'localhost' is formally assigned IP address '127.0.0.1'.

```
/ # cat /etc/hosts
127.0.0.1	localhost
::1	localhost ip6-localhost ip6-loopback
fe00::0	ip6-localnet
ff00::0	ip6-mcastprefix
ff02::1	ip6-allnodes
ff02::2	ip6-allrouters
172.17.0.2	f58bdbfa877f
```
The `apk` command is available on some Linux versions (like Alpine) to install new programs.
`curl` isn't preinstalled but can be added with this command.

```
/ # curl https://www.google.com
sh: curl: not found
/ # apk add --update curl
fetch http://dl-cdn.alpinelinux.org/alpine/v3.11/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.11/community/x86_64/APKINDEX.tar.gz
(1/4) Installing ca-certificates (20191127-r1)
(2/4) Installing nghttp2-libs (1.40.0-r0)
(3/4) Installing libcurl (7.67.0-r0)
(4/4) Installing curl (7.67.0-r0)
Executing busybox-1.31.1-r9.trigger
Executing ca-certificates-20191127-r1.trigger
OK: 7 MiB in 18 packages
/ # curl https://www.google.com
...Content from Google...
```

There are other commands like `ssh` (shell into another system) and `sftp` (transfer
files between systems) which are also quite useful.

##### Unix - Exit Shell

Type `exit` to leave a shell.


### Create Docker Image for Application

This section will be run on your system and not within a Unix Docker image, but it will
create a Unix Docker image.

Recall that for your Spring Boot application `./mvnw clean package spring-boot:repackage`
does the following.

  - './mvnw' - Runs Maven from the local directory
  - 'clean' - Cleans up (deletes) any previous Maven work for this project
  - 'package' - Builds the project
  - 'spring-boot:repackage' - Repackages the project into a 'fat JAR' (self-running app)
    - For the 'demo' project the resulting file is 'target/demo-0.0.1-SNAPSHOT.jar'

A `Dockerfile` defines a Docker image. Docker images can 'piggyback' off each other.

For the 'demo' project created in the previous exercise, the following `Dockerfile`
(with that filename) uses (`FROM`) an Alpine Linux system with Java 11 installed,
copies (`COPY`) the 'fat JAR' into it, and then runs (`CMD`) the demo application.

```
FROM adoptopenjdk/openjdk11:jdk-11.0.7_10-alpine
COPY target/demo-0.0.1-SNAPSHOT.jar .
CMD java -jar demo-0.0.1-SNAPSHOT.jar
```

Using that `Dockerfile`, build the Docker image with the following command.

```
docker build .
```

List the Docker images which should include the one you just built. Since the previous command
didn't 'tag' the image with a special name use the 'CREATED' time to figure out which one
it is and its associated 'IMAGE ID' value ('3c9891bf0e87' for the example here).

```
$ docker images
REPOSITORY                                           TAG                    IMAGE ID            CREATED              SIZE
<none>                                               <none>                 3c9891bf0e87        About a minute ago   361MB
```

Run the Docker image and map its 8080 port to your local system's ('localhost') 8080 port.
(Docker does not allow access to a container's port without the '--publish' flag).

```
docker run --publish 8080:8080 --detach 3c9891bf0e87
```

Now, the 'demo' app can again be run from your computer by going to http://localhost:8080/
in a browser. Note that this time it's running from a Docker container and not your local
command prompt.

This Docker image is now packaged and ready to ship to the cloud (like AWS).


docker container rm $(docker container ls –aq)

environment variables as feature flags

generate certificate

billing