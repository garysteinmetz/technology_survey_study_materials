# Bonus: I Have Completed These Server Examples

## Fun with Docker

### Install Docker

Follow the instructions
[here](i_can_run_a_web_application_from_a_container_in_the_cloud.md#installing-docker)
under the 'Installing Docker' section.

### FunBox

Funbox is a Docker image on a Linux system with a lot of fun
text-oriented commands. More information can be found at
https://github.com/wernight/docker-funbox .

Run that image with the following command.

```
docker run --rm -it wernight/funbox
```

Then enter the number of the program that you want to run. Some of the
examples don't work right. Depending on program selecting, quit by
pressing 'q', the escape button, the space bar, or something else
(including holding down the control button while pressing 'c').

Click a number corresponding to an option, which include 'aafire',
'asciiquarium', 'cmatrix', 'nyancat', 'xaos', and 'cacaview' .

Many of these programs can be run in freeform so that you can customize
text in your own way. Run this command to get into the Linux command line.

```
docker run -it wernight/funbox /bin/bash
```

Then take a command that was in the original menu and run it with
additional parameters ('arguments'). Here are some examples.

  - `figlet "Gary"`
  - `cacaview ./usr/share/icons/Adwaita/32x32/emotes/face-worried.png`
    - Use `find . | grep png` to get a list of PNG image files
  
Issue the `exit` command to leave the Linux command line.

#### Stop Docker Containers

Docker images are run as 'containers' . Once you are done running them,
it's important to stop them so that they aren't taking memory and
processing power on your machine.

Use command `docker ps -aq` to list all containers - this lists the
'hexadecimal' code for each container. For each code, run the following
commands to stop the container then remove it.

  - docker stop <hexadecimal_code>

Then run command `docker ps -a` and if any containers are still listed
remove them one-by-one with this command.

  - docker rm <hexadecimal_code>

#### Remove Unused Docker Images

Entering `docker images` will list all Docker images. Remove all unused
Docker images with the following command. (Unused means that there is
no active container running that image.)

  - `docker rmi $(docker images -a -q)`

### Zork

Text-based adventure games are games that where the user interacts by
entering in commands (e.g. types words). If there are graphics,
they generally don't move and the user isn't pressured to enter a command
in quickly.

These games were especially popular in the early 1980s and they made
money for gaming companies. They are still played today and represent
a valid genre of gaming.

A text-based adventure can involve just about any scenario -
like fighting mythical monsters, solving a crime, escaping a spaceship.

`Zork` is one of the best-known games of this genre. And there's a
Docker image for it!

#### Zork Docker Image and Play

There is a Docker image which includes the game Zork at
https://github.com/clockworksoul/docker-zork1 . Install and run
the image with the following command.

  - `docker run -it -v ~/saves/zork1:/save clockworksoul/zork1`

#### Playing and Winning Zork

A command list can be found at https://zork.fandom.com/wiki/Command_List .

A good workthrough of Zork can be found at
https://gamefaqs.gamespot.com/pc/564446-zork-i/faqs/20848 .

## Packet Sniffing

### What Is Packet Sniffing?

`Packet sniffers` are programs that listen to and output network traffic.
Depending on the configuration of your machine (this can get more
complicated), the packet sniffer either listens to 'packets'
of network traffic being sent to and from (A) the machine or (B) all
machines on the local network (like a wireless LAN - local area network).
They can be used both for good reasons (like troubleshooting)
and bad reasons (like snooping on the activity of another computer).

### Terms

Here are important terms for this exercise.

- `HTTP` - This is the basic internet protocol for web communication.
HTTP transmissions frequently contain words readily readable in English.
- `HTTPS` - This is the secure version of HTTP. Unlike HTTP,
the transmissions are encrypted so a packet sniffer won't show English
words, but the client and the server involved in the transmission will
be able to decrypt the transmissions which will include English words.
- `curl` - This is a command-line program which can make HTTP/HTTPS
client calls just as a web browser does, but without a user interface.
This program supports all of the components of an HTTP call including
request headers, URLs, request body. response code, response headers,
and response body. It also supports all method types including
`GET`, `POST`, `PUT`, `DELETE`, and `PATCH`.
- `HTTP/2` - This is the next generation of the HTTP protocol
which includes a restructuring of how HTTP communications are sent.
It's not used in this exercise because it's hard to find a public website
that supports both HTTP/2 and non-secure HTTP.
- `--net` - This is an option when starting a Docker container
(with `docker run`) in order to set its 'network namespace', including
the option of being in the same one as another container that has
already started. This is important because Docker containers are generally
isolated from each other in that each doesn't receive the network packets
sent to other containers, which means that a packet sniffer won't pick
up those packets. But this option allows one container to receive
the packets of another (similar to peer computers on a LAN).
- `tcpdump` - This is a Unix/Linux packet sniffer.
- `apk` - This is a Linux program for installing other programs
(like 'tcpdump').
- `alpine` - This is one type of Linux operating system.

### Setup

Goal - Launch one Docker container which will run 'curl' commands
and the launch another Docker container which will act as the packet
sniffer (with the 'tcpdump' command).

#### 'curl' Machine

Open a command prompt and run the following command.

```
docker run -it alpine:3.12.4 /bin/ash
```

Install the 'curl' program on this system with this command.

```
apk add curl
```

Now make a simple HTTP 'GET' call using 'curl' as follows.

```
curl http://jsonplaceholder.typicode.com/posts/1
```

It should return the following.

```
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

Put the URL above into a browser and confirm that the response is the same.

#### 'tcpdump' Machine

Open a second command prompt and get the Docker container ID of the
'curl' machine with the following command.

```
docker ps -a
```

Record the ID under the 'CONTAINER ID' column for the row having
'IMAGE' of 'alpine:3.12.4' and 'STATUS' containing the word 'Up' .

Now start a container with the following command but replace
'<CONTAINER_ID>' with the value you just recorded.

```
docker run -it --net container:<CONTAINER_ID> alpine:3.12.4 /bin/ash
```

Install the 'tcpdump' program on this system with this command.

```
apk add tcpdump
```

Run 'tcpdump' with the '-X' option to represent the output as hexadecimal
and ASCII (human-readable).

```
tcpdump -X
```

Now on the 'curl' machine rerun this command and confirm that the
HTTP request/response appear with some English words (like 'GET'
and 'OK'). Use the '-v' (verbose) option to get all components of the
HTTP request/response.

```
curl -v http://jsonplaceholder.typicode.com/posts/1
```

Notice that common HTTP headers can be found in the request and response
- like 'Host', 'Accept', 'Content-Length'

Review the output on the 'tcpdump' machine and confirm that it has
packet-sniffed the HTTP request/response of the 'curl' machine. Do this
by finding the words 'GET' and 'HTTP' (they should be found somewhere
in the top-half of the output).

### Secure 'GET' Call

The above instructions confirmed the packet sniffing of an insecure
(plain text) HTTP call. Now use 'https' instead of 'http' in the 'curl'
command. Notice that the output on the 'curl' machine is largely the same
but the network transmissions (request and response) are encrypted
so the output will largely be scrambled on the 'tcpdump' machine.
(Uppercase) 'OK' and 'GET' probably don't appear but
'jsonplaceholder.typicode.com' (the server hostname) still does appear.

```
curl -v https://jsonplaceholder.typicode.com/posts/1
```

### 'POST' Call

#### HTML Form

### 'PUT' Call

### 'DELETE' Call

### 'PATCH' Call


https://www.tcpdump.org/manpages/tcpdump.1.html

compare HTTP to HTTPS

https://sites.google.com/site/jimmyxu101/testing/use-tcpdump-to-monitor-http-traffic

https://www.thegeekdiary.com/how-to-configure-interface-in-promiscuous-mode-in-centos-rhel/#:~:text=Promiscuous%20mode%20or%20promisc%20mode,program%20like%20Wireshark%2C%20and%20tcpdump.
https://stackoverflow.com/questions/40130356/docker-containers-network-interface-in-promiscuous-mode

docker run -it --privileged alpine:3.12.4 /bin/ash
ip link set eth0 promisc on

docker run -it --net container:590dd0e31d3c nicolaka/netshoot
Welcome to Netshoot! (github.com/nicolaka/netshoot)                                                                   
docker run -it --net container:590dd0e31d3c --privileged alpine:3.12.4 /bin/ash
tcpdump -X

'curl' with and without '-v' option
HTTPS protocol
HTTP/2

```
docker run -it alpine:3.12.4 /bin/ash

apk add curl

apk add tcpdump

apk add wireshark

tcpdump -A -s 0 'tcp port 80 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)' &

ps -aef

/ # curl -v http://jsonplaceholder.typicode.com/posts/1 > output1.txt
```

## Route Custom Domain to GitHub Pages Site

https://docs.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site

## AWS Lightsail

### Billing

### Cloudwatch

### Access Permissions

https://ihusyn.wordpress.com/2019/11/01/how-to-install-java-11-on-amazon-linux/

https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-using-service-linked-roles
'Lightsail does not allow you to edit the AWSServiceRoleForLightsail service-linked role.'

https://www.titanwolf.org/Network/q/33361d67-a8a7-4f91-84a7-13bf588a15e5/y

https://docs.aws.amazon.com/corretto/latest/corretto-8-ug/amazon-linux-install.html

https://aws.amazon.com/premiumsupport/knowledge-center/ec2-install-extras-library-software/

java-1.8.0-openjdk.x86_64
yum list available | more
sudo yum install java-1.8.0-openjdk.x86_64
sudo yum -y install java-1.8.0-openjdk-devel.x86_64

https://aboullaite.me/switching-between-java-versions-on-ubuntu-linux/
sudo update-alternatives --config java
sudo update-alternatives --set java /usr/lib/jvm/jre-1.8.0-openjdk.x86_64/bin/java

AmazonLightsailInstanceRole

https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-using-service-linked-roles

https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.html

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_access_key

https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.html

```
$ aws dynamodb list-tables

An error occurred (AccessDeniedException) when calling the ListTables operation: User: arn:
aws:sts::895453431615:assumed-role/AmazonLightsailInstanceRole/i-06d8d267e33c9648a is not a
uthorized to perform: dynamodb:ListTables on resource: arn:aws:dynamodb:us-east-1:895453431
615:table/*
```

```
$ aws cognito-identity list-identity-pools --max-results 5

An error occurred (AccessDeniedException) when calling the ListIdentityPools operation: Use
r: arn:aws:sts::895453431615:assumed-role/AmazonLightsailInstanceRole/i-06d8d267e33c9648a i
s not authorized to perform: cognito-identity:ListIdentityPools on resource: arn:aws:cognit
o-identity:us-east-1:895453431615:identitypool/
```

```
$ aws s3 ls

An error occurred (AccessDenied) when calling the ListBuckets operation: Access Denied
```

```
$ aws ecr describe-repositories

An error occurred (AccessDeniedException) when calling the DescribeRepositories operation: 
User: arn:aws:sts::895453431615:assumed-role/AmazonLightsailInstanceRole/i-06d8d267e33c9648
a is not authorized to perform: ecr:DescribeRepositories on resource: arn:aws:ecr:us-east-1
:895453431615:repository/*
```

### SSH Usage
Generating key from the command line

web-based access

### Session Affinity and Redis Caching

### Infrastructure as Code