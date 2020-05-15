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

_Note that Unix commands can be, and are quite often are, used in a Dockerfile._

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


### Databases

Databases ... store data.

The subject of databases is a vast one and this review of databases is not meant
to be comprehensive or representative.

Directly or indirectly, databases are central to most web applications. Without databases,
there would be no way of storing transactions and what the web application has actually
changed. It would be like a bank with a vault.

#### Types of Databases

Web applications generally use one of two different types of databases - SQL and NoSQL.

##### SQL

`SQL` stands for `Structured Query Language` and, in the context of NoSQL, the word
'structured' is important. Like XML, it expects data to be formatted in a certain way.
It's a standardized language for interacting with relational databases. SQL-compliant
databases are relational databases.

The expected format of data is known as a predefined `schema` (set of rules).

By applying rules and other supporting structure, it's easier to ensure that the data
are correct and consistent. Likewise, it's easier to bring different types of data
together (`join` them).

SQL is very good at coordinated changes between different data entities.
These coordinations are known as `transactions` - like subtract money from one bank account
and add it into another. There would be a problem if the logic errored-out after
the subtract but before the add.

In SQL, transactions follow the `ACID` principle - atomic, consistent, idempotent, durable.

For most database data, each data entry has a unique identifier. known as `primary key` .
Entries of a certain class (e.g. addresses, invoices) are stored in their own `table` .

SQL has been around since the 1970s and is structured more along the lines of powerful
(mainframe) computers.

##### NoSQL

Analogous to the structured-versus-unstructured approach between XML and JSON, `NoSQL`
is more unstructured like JSON.

NoSQL data is more flexible but that also means that, unlike SQL, it lacks structure.
Likewise, it's less likely to have the infrastructure to bring (`join`) different types
of data together. For advantages, it can better adapt to changing business needs
and (growing up during a time of distributed systems and cloud computing) it's better able
to use newer ways of querying data (like `MapReduce`).

###### Key-Value Database

A key-value database is like a relational database table with a `primary key` column
and a value column.

###### Document Database

Document databases can come in different forms, but one popular one is to store JSON-based
documents that be queried JSON-based query statements.

###### Graph Database

Graph databases consist of things (nodes) along with their relationship to other things (edges).
Such a database is better-suited for things like social networking.

###### In-Memory Database

Analytics

##### Other Kinds of Databases

There are other kinds of databases. Here are some of them.

###### Flat File
Flat files are actually traditional but they aren't normally used in web applications.

The files consist of a header row stating what each column represents. After the header row,
each row lists a new entry either separated by commas (`CSV` file or `comma-separated value`)
or `tab-delimited` file. Here's an example.

```
STUDENT_NAME,AGE,GRADE
Sally,16,B
Ahmad,17,A
Jane,16,A+
Chin,16,B-
```

Flat files are a great way of transferring data between unrelated systems which have
completely different internal architectures. Data is transferred between systems
using a `ETL` or `Extract, Transform, Load` process.

Flat files might seem to be boring and that's the point - they are solid and predictable
and leave less to chance.

###### Blockchain

Most databases are centrally-managed. All of the data is stored in one server or a cluster
of servers managed by one entity which is typically a company or government.
The entity has full control and responsibility over the data.

`Blockchain` is very different. Like `Git` (for source control), all users have their own
copies of the data and there is a periodic contest to update the data.
(For the `cryptocurrency` `Bitcoin`, this contest occurs very 10 minutes.)

Blockchain also goes by the name `distributed ledger` because it acts as a global accounting
ledger of the different transactions (payments) between parties.

AWS DynamoDB is a widely-used NoSQL database within AWS. 'NoSQL' means it lacks the structure
of traditional 'relational' databases (which use 'SQL'). The relationship between 'NoSQL' to
'SQL' is similar to the relationship between JSON (less structure) and XML (more structure).

Download 


#### Other Untraditional Databases

Flat files
Graph Databases
Blockchain

### SQL Databases - MySQL

`MySQL` is an `open source` (free to use and change the source code) database, unlike
commercial database like `Oracle`.

#### Exercise - Use MySQL

In this exercise, you will download and run a Docker image running MySQL.
Then you will interact with the relational database, create tables, insert data with rollback,
insert data with commit, delete data, update data, and view (`select`) data.

This exercise will simulate a banking application.

##### Download MySQL Image

Execute the following command.

```
docker pull mysql
```

Record the `IMAGE ID` value of this image (the value 'a7a67c95e831' will be used here).

##### Start the MySQL Server

Start the MySQL Docker container with the following command.
The '-e MYSQL_ALLOW_EMPTY_PASSWORD=yes' command-line switch sets the
'MYSQL_ALLOW_EMPTY_PASSWORD' environment variable to the value of 'yes' which instructs
the MySQL server to not require a username/password combination to log in which is bad
practice for a production system but acceptable for local development.

```
docker run -d -e MYSQL_ALLOW_EMPTY_PASSWORD=yes a7a67c95e831
```

##### Go into the MySQL Container

Docker has the 'exec' command that allows you to run a program inside the running container.
The '/bin/bash' command is a program in the Docker container that starts a command prompt.

```
docker exec -it a7a67c95e831 /bin/bash
```

Type 'mysql' to start a program that allows you to interact with the MySQL database.

```
# mysql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 8.0.20 MySQL Community Server - GPL

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

Show which databases are available to use with the `show databases;` command.
(Yes, multiple databases, different stores of data, are being run by this MySQL server.)

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.28 sec)

mysql> 
```

Use the 'mysql' database (second entry listed above) with the `use mysql;` command.

```
mysql> use mysql;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> 
```

Enter `show tables;` to list the tables (data entries ordered by kind) in the database.

Create a table called 'accounts' to containing just two columns - an 'id' column which
uniquely identifies each account and a 'name' column which identifies the name of the
person who owns the account (note that two accounts can have identical names!).

```
CREATE TABLE accounts (
    id MEDIUMINT NOT NULL AUTO_INCREMENT,
    name CHAR(30) NOT NULL,
    PRIMARY KEY (id)
);
```

The `show tables;` command now lists 'accounts' and `describe accounts;` will
describe the table.

The 'id' field is a medium-sized integer that can't be null and auto-increments
(for each new entry, it's assigned a new value that's one higher than the previous entry).

The 'name' field is a string value that can't be null and has a maximum length
of 30 characters.

Statements like `CREATE TABLE` are known as `DDL` for `Data Definition Language`.
DDL statements happen immediately and become visible to all other database users
instantaneously. (They can't be `rolled back` before others can access it, but other
statements like `DELETE TABLE` can change or delete a table.)

Now create a 'transactions' table which holds all of the transactions of the account.

```
CREATE TABLE transactions (
    amount DECIMAL(6,2) NOT NULL,
    account_id MEDIUMINT NOT NULL,
    FOREIGN KEY (account_id)
        REFERENCES accounts(id)
);
```

##### Insert Data into the Tables

Like the `HTTP` methods (`POST`, `GET`, `PUT`, and `DELETE`), SQL also has its set
of `CRUD` (Create, Read, Update, Delete) with the commands `INSERT`, `SELECT`, `UPDATE`,
and `DELETE` , respectively. Unlike `DDL` statements, these statements (known as
`DML` for `Data Manipulation Language`) are not necessarily immediately visible to others.
By default, MySQL has the `autocommit` flag set to 'on' which means that DML statements
will be visible to others. Turn this value off with the following command.

```
SET autocommit = 0;
```

Now `DML` statements won't be visible to others until an explicit `commit;` statement
is issued. This means that a group of statements that form a `transaction` will all
succeed or fail together (following the `ACID` principle).

First issue an `INSERT` statement into an account, but exit out of the `mysql` client
before issuing a `commit`. Use the `SELECT` statement ('*' means select everything)
to view the row you just added. Again, since no `commit` was issued, this 'INSERT'
won't be visible by others yet. Note how the 'id' field doesn't need to be specified
because the 'AUTO_INCREMENT' keyword was applied to that field.

```
mysql> INSERT INTO accounts(name) values ('Gary');
Query OK, 1 row affected (0.02 sec)

mysql> SELECT * FROM accounts;
+----+------+
| id | name |
+----+------+
|  1 | Gary |
+----+------+
1 row in set (0.00 sec)

mysql> 
```

Now type `exit;` to leave the `mysql` client. Then go back in by entering `mysql`
and then `use mysql;` (to again select that database). Again issue the `SET autocommit = 0;`
command to turn off autocommit.

Now enter the same command to create an account.

```
INSERT INTO accounts(name) values ('Gary');
```

Now again issue the `SELECT * FROM accounts;` statement and record the 'id' field value
(the statements below will assume this value is 2). Entries in the 'transactions' table
will reference this entry using it as the `foreign key` .

```
mysql> SELECT * FROM accounts;
+----+------+
| id | name |
+----+------+
|  2 | Gary |
+----+------+
1 row in set (0.00 sec)
```

Now issue two more `INSERT` statements to represent the deposit of $100 and a withdrawal
of $9 from that account. Then issue a `commit;` to complete the transaction and allow
others to see it.

```
mysql> INSERT INTO transactions(amount, account_id) VALUES (100, 2);
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO transactions(amount, account_id) VALUES (-9, 2);
Query OK, 1 row affected (0.01 sec)

mysql> commit;
Query OK, 0 rows affected (0.01 sec)
```

Again enter `exit;` to leave the MySQL client but then immediately return by entering
`mysql` from the command line. Again enter `use mysql;` to use that database and
then use a `SELECT` command involving both tables which are properly `joined`
with the 'account.id = transactions.account_id' clause. The 'accounts.id = 2' clause
ensures that only the account 'Gary' is the one chosen. The `SUM(amount)` adds up
all the amounts for 'Gary' in the 'transactions' table to get that accounts current
balance (of $91).

```
mysql> select SUM(amount) from accounts, transactions where accounts.id = transactions.account_id and accounts.id = 2;
+-------------+
| SUM(amount) |
+-------------+
|       91.00 |
+-------------+
1 row in set (0.01 sec)
```

Notice how the `commit;` command caused the transaction (entries) not to be lost.

Type 'exit;' to exit the 'mysql' client and the enter 'exit' to leave the MySQL Docker
container.


### NoSQL Databases - DynamoDB

DynamoDB is a key-value database supported in AWS. As will be shown, interaction is
much simpler than with SQL - lacking table joins, transactions involving multiple changes,
precise data definitions and constraints.

That doesn't mean that all NoSQL databases are simple. SQL defines feature-rich and
well-defined means of interacting with data. NoSQL just means 'no SQL' - the extensive ruleset
of SQL is not necessarily adhered to.

DynamoDB supports the four `CRUD` operations, but the read ('R') operation returns all
entries in the table. For reads, it's up to the client (usually a program) to interpret
the response (unlike SQL in which the 'where' clause filters what's returned).

#### Exercise - Use DynamoDB

In this exercise, you will download a Docker image for AWS DynamoDB, run it locally,
and execute commands against it.

#### Download AWS CLI and DynamoDB Docker Images

This exercise uses not one, but two Docker images.

  - AWS CLI - The AWS CLI (command-line interface) is a command line program for interacting
  with AWS. It (specifically, the `aws` command) allows you to perform most activities
  permitted in the AWS console (at https://aws.amazon.com ) user interface. You could
  download and install the AWS CLI onto your local system but it's more convenient
  (and more educational) to download the AWS CLI Docker image and use that.
  - AWS DynamoDB - This is the Docker image to run a local version of AWS DynamoDB.
  While it supports standard DynamoDB commands, you would _Not_ run this in Production
  because it lacks the security, scalability, and other features you'd want in a Production
  component.

Download ('pull') both images with these two commands.

```
docker pull amazon/aws-cli
docker pull amazon/dynamodb-local
```

The regular (non-Docker) AWS CLI can be downloaded and installed by following instructions at
https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html , but using Docker
here is actually easier for setup instructions (and is mostly OS-independent). If that
regular (non-Docker) AWS CLI where to be installed, the script program below
('runAws.sh' or 'runAws.bat', depending on your OS) wouldn't be needed and the `aws`
could be used instead after running the `aws configure` command to configure
the 'access key', 'secret key', and AWS region.

#### Start Local DynamoDB

Start the local DynamoDB container with the following command.

```
docker run -d --rm -p 8000:8000 amazon/dynamodb-local
```

  - `-d` instructs Docker to run the container 'in the background' (which means that you can
  continue typing other commands after the container has started running).
  - `--rm` automatically removes the container when it stops. Normally, Docker saves a stopped
  container just in case additional analysis is needed, but that's not necessary here.
  - `-p 8000:8000` instructs Docker to join port 8000 on the local computer ('localhost')
  to port 8000 of the container. Normally, Docker _does not_ allow a port in a container
  to be accessible outside of it. The `-p` option makes the port accessible.

Optionally run `docker ps -a` afterwards to confirm that the container is running.

This local DynamoDB actually hosts an interactive web page at
http://localhost:8000/shell/ but that won't be used for this exercise.

#### Create Script File to Simplify Interacting with the Local DynamoDB

To properly run the AWS CLI client _and_ execute the DynamoDB command requires a lengthy
command-line command. Much of this command (the prefix part) is the same no matter which
command is being run. Therefore, it's a good idea to place this prefix in a shell script
file to save that typing and reduce the likelihood of error.

Here's an example of the full command which lists all of the tables in the local DynamoDB.

```
docker run --rm -it --network host -e AWS_ACCESS_KEY_ID=DoesNotMatter -e AWS_SECRET_ACCESS_KEY=DoesNotMatter amazon/aws-cli --region us-east-1 dynamodb list-tables --endpoint-url http://localhost:8000
```

As you can see, it's 200 characters long!

This lengthy command consists of two parts.

  - The first part runs the AWS CLI Docker container with the proper settings.
  - The second part runs the Dynamo DB command.

Here's the output of the command which indicates that there are no tables at present.
```
{
    "TableNames": []
}
```

Here's the first part of the command which just starts the AWS CLI.
```
docker run --rm -it --network host -e AWS_ACCESS_KEY_ID=DoesNotMatter -e AWS_SECRET_ACCESS_KEY=DoesNotMatter amazon/aws-cli
```

  - `docker run` runs the Docker container.
  - `--rm` automatically removes the container when it stops. Normally, Docker saves a stopped
  container just in case additional analysis is needed, but that's not necessary here.
  - `-it` prints the output to the console in a certain format.
  - `--network host` means that the container will have (share) the same network settings as
  the local computer. In other words, when DynamoDB accesses the 'localhost' that
  the local DynamoDB publishes to (at http://localhost:8000 ), that 'localhost' will be
  the same 'localhost' as the one this Docker container uses.
  - `-e AWS_ACCESS_KEY_ID=DoesNotMatter` is needed because AWS CLI expects the login
  credentials (the pair consisting of an 'access key' and 'secret key') to be present.
  These credentials are usually listed in the '~/.aws/credentials' file on your local
  system but the AWS CLI Docker image doesn't have this file. But the 'AWS_ACCESS_KEY_ID'
  environment variable can substitute for the 'access key' value. Note that the value
  of this variable doesn't matter because the local DynamoDB server doesn't have security
  but the AWS CLI expects a value and will generate an error otherwise. Therefore,
  'DoesNotMatter' is a good-enough value to get this to work. These useless but necessary
  value settings are called `dummy values` .
  - `-e AWS_SECRET_ACCESS_KEY=DoesNotMatter` is the 'dummy value' for the secret key.
  - `amazon/aws-cli` is the AWS CLI Docker image to run.

This first part can be placed in a shell script file (known as a batch file on Windows).

Here is the file (call it 'runAws.sh') for Mac or Linux. It's the same command as
the first part above but adds ` "$@"` to the end so that all command-line parameters
passed into this script
(like '--region us-east-1 dynamodb list-tables --endpoint-url http://localhost:8000')
are submitted as parameters at the end of the `aws` command.
```
docker run --rm -it --network host -e AWS_ACCESS_KEY_ID=DoesNotMatter -e AWS_SECRET_ACCESS_KEY=DoesNotMatter amazon/aws-cli "$@"
```
Run `chmod 777 runAws.sh` after creating this file so that it can be executed.

Here is the file (call it 'runAws.bat') for Windows. Instead of ` "$@"` at the end,
the equivalent value in Windows is ` %*` .
```
docker run --rm -it --network host -e AWS_ACCESS_KEY_ID=DoesNotMatter -e AWS_SECRET_ACCESS_KEY=DoesNotMatter amazon/aws-cli
```

Now use the script to execute the same 'list-tables' command as above - with fewer keystrokes!

  - `Windows` - `.\runAws.bat --region us-east-1 dynamodb list-tables --endpoint-url http://localhost:8000`
  - `Mac/Linux` - `./runAws.sh --region us-east-1 dynamodb list-tables --endpoint-url http://localhost:8000`

The parts beyond the shell script are as follows.

  - `--region us-east-1` - For most AWS components (like virtual computers and databases),
  the component must be placed in a specific region where Amazon stores its actual assets
  (like real computers). Like 'access key' and 'secret key', this value doesn't matter
  in this case because you are trying to connect to a local DynamoDB, but the AWS CLI
  still expects a value. 'us-east-1' is a real region value that corresponds to several
  large datacenters in northern Virginia.
  - `dynamodb` - States the type of AWS CLI command to run, in this case it's a DynamoDB
  command.
  - `list-tables` - Lists the tables in the database.
  - `--endpoint-url http://localhost:8000` - States where ('localhost:8080') the database is
  and how ('http://') to communicate with it.

'AWS_ACCESS_KEY_ID' states who you are, 'AWS_SECRET_ACCESS_KEY' confirms who you are,
and '--region' states the region where you want your command to take place.




environment variables as feature flags

generate certificate

billing