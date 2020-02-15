# Install Docker

## For Windows, Enable Virtualization
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

## General Instructions
1) Go to https://github.com/docker/toolbox/releases

2a) For Windows, download the '*.exe' (like 'DockerToolbox-19.03.1.exe') file

2b) For Mac, download the '*.pkg' (like 'DockerToolbox-19.03.1.pkg') file

3) Install the software (just keep clicking the 'Continue' button)

## Exercise - Confirm Installation

1) Open a command prompt (actually, search for Docker and start its 'daemon')
2) Enter the following command to start a local server
```
docker run hello-world
```
3) Confirm that 'Hello from Docker!' appears in the output