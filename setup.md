---
title: "Setup"
---

<div class="questions">

### Questions

- How do I securely log into a Nimbus VM instance?
</div>  

<div class="objectives">

### Objectives

- Successfully log in to a Nimbus instance using ssh.

</div>  


## The Pawsey Supercomputing Research Centre
The [Pawsey Supercomputing Research Centre](https://pawsey.org.au/about-us/about-pawsey/) is one of two, Tier-1, High Performance Computing facilities in Australia, whose primary function is to accelerate scientific research for the benefit of the nation. Pawsey service and expertise in supercomputing, data, cloud services and visualisation, enables research across a spread of domains including astronomy, life sciences, medicine, energy, resources and artificial intelligence.

## Bioinformatics with Nimbus

Nimbus cloud from Pawsey can help the reserachers scale their problems and make them solvable in a reasonable timeframe. Nimbus instance is a virtual machine (VM) located on Nimbus servers, that you use in place of your laptop or desktop computer. Nimbus is a useful solution for bioinformatics applications that may not be suitable for large-scale HPC machines including:

- Developing and refining scalable workflows in prepration for HPC allocation applications. 
- Workflows with long runtimes that excede wall time queue limits on HPC facilities. 
- Complex data-bound workflows with variable compute resource profiles that are common in bioinformatics pipelines.

## Set up your laptop 

### Get a shell terminal emulator

To connect to the Nimbus VM, and follow this lesson, you will need a **'terminal emulator'** program installed on your computer. Often just called a 'terminal', or 'shell terminal', 'shell client', terminal emulators give you a window with a _command line interface_ through which you can send commands to be executed by your computer.

#### A. Linux systems

If you use Linux, then chances are you already know your shell and how to use it. Basically, just open your preferred terminal program and off you go! An X-Window server (X11) may also be useful if you want to be able to use GUIs; again, if you're using Linux you probably have one, and if you don't have one, it's probably because you intentionally disabled it! 

#### B. OSX (Mac computers and laptops)

Mac operating systems come with a terminal program, called Terminal. Just look for it in your Applications folder, or hit Command-Space and type 'terminal'. You may find that other, 3rd party terminal programs are more user-friendly and powerful -- I use [Iterm2](https://www.iterm2.com/).

![<b>Terminal</b> is OSX's native terminal emulator.](../fig/s_terminal_app.png) 

We also recommend installing [XQuartz](https://www.xquartz.org/), which will replace OSX's native X-Window server. XQuartz has some extra features that may offer better performance when using GUI programs. You'll need to log out and back in again after installing XQuartz in order for it to activate.

#### C. Windows

If you're using a Windows machine, don't panic! You might not have used 'CMD' since Windows 95 but, rest assured, Windows still has a couple of terminal programs and shells buried in the Programs menu.
However, those aren't going to work for us, as you'll need extra programs and utilities to connect to Nimbus, such as an _SSH_ implementation. 

- To use Nimbus on a Windows computer, you have a couple of options, as shown below. 
- We recommend using the `MobaXterm` terminal application. 

##### i. MobaXterm
[MobaXterm](https://mobaxterm.mobatek.net/download.html) offers a rich experience as a full-featured X-server and terminal emulator for ssh connections, the free version is more than adequate.

`Directions` to install and start using MobaXterm

- Go to https://mobaxterm.mobatek.net/download.html
- Under ‘Home Edition’ select the `Download now` button
- Select the MobaXterm Home Edition (Installer edition)
- Once the program is downloaded, install it as you would any other windows program
- Once the program is installed, start the MobaXterm program.  
- From this screen, click on ‘start local terminal’
- Type in: ssh training@XXX.XXX.XX
- When prompted, enter your password

##### ii. PuTTY
PuTTY, an SSH and telnet client, is a good simple option. However, note that PuTTY **does not** provide an X11 server, so you won't be able to use GUI programs with _just_ PuTTY. Head to [https://putty.org](https://putty.org) and download PuTTY. You can install it to your computer, or just download the 'binary' and run it directly. 

##### iii. WSL and Ubuntu
Install Ubuntu or some other Linux distro on the Windows Subsystem for Linux see [here for details](https://ubuntu.com/tutorials/tutorial-ubuntu-on-windows#1-overview). This one will give you a full suite of Linux functions and I like it for emulating Linux.


## Connecting to a Nimbus instance

Loggin into a Nimbus instance requires three things:
1. The **IP Address** (virtual address) of your instance. It is a series of numbers i.e. ###.###.###.###. Every participant is provided with an separate IP Address which points to an independant VM instance.
2. Your **login name**: this depends on the name of the Linux OS image you selected and in our case it is ```training```.
3. Your **password**. Every participant is provided with a password

![SSH connection to Nimbus VM instance](../fig/Pawsey_VM_instance.png)  

### Logging-in using a terminal

The primary means by which we can connect to this VM is via a Secure Shell (SSH) over a Command Line Interface (CLI). Type the following into your terminal, using your login name and the instance’s IP address:

```
ssh training@###.###.###.###
```

You will receive a message saying:
```
The authenticity of host '146.118.67.137 (146.118.67.137)' can't be established.
```
Remember your host address will be different than the one above. There will then be a message saying:
```
Are you sure you want to continue connecting (yes/no)?
```
If you are sure (and/or confirm the fingerprint), answer ‘yes’ to continue. It will then give a warning:
```
Warning: Permanently added '146.118.67.137' (ECDSA) to the list of known hosts.
```
```
Enter password:
```
Meaning that next time you log in using this key and IP address you won’t receive this message. Having done that, your terminal should then display something like that shown in the figure below:

![figure](../fig/Nimbus_login_screen.png)

**Congratulations, you have now successfully logged on to your instance!**


<div class="keypoints">

### Key points

- Nimbus VM instances from Pawsey provide on-demand access for scalability.
- We use a ssh client to connect to a Linux instance.
</div>  