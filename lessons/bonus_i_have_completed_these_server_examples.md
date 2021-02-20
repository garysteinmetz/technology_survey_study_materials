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
