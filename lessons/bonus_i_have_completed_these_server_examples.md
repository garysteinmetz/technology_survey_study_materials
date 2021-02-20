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

