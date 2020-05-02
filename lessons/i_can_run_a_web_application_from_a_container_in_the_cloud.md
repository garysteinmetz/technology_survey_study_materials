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
`rm` command.

`cat` displays the contents of a file.

`echo` just prints what is typed to the console.

echo
tail
vi
history
find
grep
ps (with &)
kill
export
top
mv
cp
ifconfig
curl
apk add --update curl
| and & and >

create a boot Jar

running the boot Jar

'fat Jar'

run a Docker image locally

https://hub.docker.com/r/adoptopenjdk/openjdk11/

docker pull adoptopenjdk/openjdk11:jdk-11.0.7_10-alpine

https://hub.docker.com/editions/community/docker-ce-desktop-mac
https://docs.spring.io/spring-boot/docs/current/maven-plugin/

shell script to build and run

./mvnw help:describe -Dplugin=org.springframework.boot:spring-boot-maven-plugin -Ddetail=true

clean spring-boot:repackage

./mvnw clean package spring-boot:repackage

docker container rm $(docker container ls –aq)

environment variables as feature flags

basic unix

generate certificate

billing