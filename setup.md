---
fig-cap-location: top
---

# **Set up**

<div class="questions">

### **Questions**

- How do I set up a terminal application on my computer?
- What internet browser do I need for this workshop?
- How do I log in to a Nimbus instance?
</div>  

<div class="objectives">

### **Objectives**

- Set up your computer for this workshop series.
- Log in to your Nimbus instance.
</div>  

In this workshop series, we will be using Pawsey's Nimbus cloud. The main requirements for this workshop is a personal computer with a web browser and a command line shell program, or terminal emulator. You will need a terminal emulator to access your Nimbus instance and a web browser to run all the exercises and visualise the outputs. On this page you will find instructions on how to set up a terminal application and web browser on your computer and how to connect to Nimbus.  

[1. Get a shell terminal emulator](#get-a-shell-terminal-emulator)  
[2. Download the right web browser](#check-your-web-browser)
<br>[3. Connect to Nimbus](#connect-to-nimbus)  


## **Bioinformatics with Nimbus**
The [Pawsey Supercomputing Research Centre](https://pawsey.org.au/about-us/about-pawsey/) is one of two, Tier-1, High Performance Computing facilities in Australia, whose primary function is to accelerate scientific research. 

Pawsey's Nimbus cloud is a flexible solution for bioinformatics applications that may not be suitable for large-scale HPC machines including:
    -   Developing and refining scalable workflows in prepration for HPC allocation applications.
    -   Workflows with long runtimes that excede wall time queue limits on HPC facilities. 
    -   Complex data-bound workflows with variable compute resource profiles that are common in bioinformatics pipelines.

## **Get a shell terminal emulator**
To connect to your Nimbus instance, and follow this lesson, you will need a **'terminal emulator'** program installed on your computer. Often just called a 'terminal', or 'shell terminal', 'shell client', terminal emulators give you a window with a _command line interface_ through which you can send commands to be executed by your computer.

More precisely, these commands are executed by your _shell_, which is a program designed to do just that: execute commands! The most commonly used shell is 'Bash', and we'll generally refer to the shell as a 'Bash shell', and to scripts as 'Bash scripts'. There are other shells, and each has its own set of extra commands or syntaxes it can accept -- its own _scripting language_.

You don't need to worry too much about this! You just need **a** shell -- almost all will understand the commands we're going to be using.

#### **A. Linux systems**
If you use Linux, then chances are you already know your shell and how to use it. Basically, just open your preferred terminal program and off you go! An X-Window server (X11) may also be useful if you want to be able to use GUIs; again, if you're using Linux you probably have one, and if you don't have one, it's probably because you intentionally disabled it! 

#### **B. OSX (Mac computers and laptops)**
Mac operating systems come with a terminal program, called Terminal. Just look for it in your Applications folder, or hit Command-Space and type 'terminal'. You may find that other, 3rd party terminal programs are more user-friendly and powerful -- I use [Iterm2](https://www.iterm2.com/).

![<b>Terminal</b> is OSX's native terminal emulator](/fig/s_terminal_app.png)

We also recommend installing [XQuartz](https://www.xquartz.org/), which will replace OSX's native X-Window server. XQuartz has some extra features that may offer better performance when using GUI programs. You'll need to log out and back in again after installing XQuartz in order for it to activate.

#### **C. Windows**
To use Nimbus on a Windows computer, you have a couple of options, as shown below. We recommend using the `MobaXterm` terminal application. 

##### **i. MobaXterm (recommended)**
[MobaXterm](https://mobaxterm.mobatek.net/download.html) offers a rich experience as a full-featured X-server and terminal emulator for ssh connections, the free version is more than adequate.

To install and start using MobaXterm:

![](/fig/s_mobaxterm.png)

1. Go to https://mobaxterm.mobatek.net/download.html
2. Under ‘Home Edition’ select the `Download now` button
3. Select the MobaXterm Home Edition (Installer edition)
4. Once the program is downloaded, install it as you would any other windows program
5. Once the program is installed, start the MobaXterm program.  
6. From this screen, click on ‘start local terminal’
7. Type in: ssh training@XXX.XXX.XX
8. When prompted, enter your password

##### **ii. PuTTY**
PuTTY, an SSH and telnet client, is a good simple option. However, note that PuTTY **does not** provide an X11 server, so you won't be able to use GUI programs with _just_ PuTTY. 
Head to [https://putty.org](https://putty.org) and download PuTTY. You can install it to your computer, or just download the 'binary' and run it directly. 

1. Fill in the connection details:
    - Host Name: **<YOUR ASSIGNED IP>**  
    - Port: **22**  
    - Connection type: **SSH**     

2. Name this session **"RNAseq_nimbus"** and click 'Save'  
3. When you are ready to log in to your Nimbus instance, click on 'Open'  
4. When the terminal opens, enter 'training' for `log in as:` and provide your password.   

![](/fig/s_putty_nimbus.png)

    
## **Connect to Nimbus**
To login to Nimbus, we will use a Secure Shell (SSH) connection, which enables 2 computers to communicate with one another. To connect, you need 3 things: 
    <br>1. *The assigned IP address* of your instance (i.e. ###.###.##.###). Each participant will be provided with their instance's IP address at the beginning of the workshop.   
    2. *Your login name*. In our case, this will be `training` for all participants. 
    <br>3. *Your password*. All participants will be provided with a password at the beginning of the workshop. 
    
To log in, type the following into your terminal, using your login name and the instance’s IP address:

```default
ssh training@###.###.###.###
```

You will receive a message saying:
```default
The authenticity of host 'XXX.XXX.XX.XXX (XXX.XXX.XX.XXX)' can't be established.
```
    
Remember your host address will be different than the one above. There will then be a message saying:
```default
Are you sure you want to continue connecting (yes/no)?
```
    
If you would like to skip this message next time you log in, answer ‘yes’. It will then give a warning:
```default
Warning: Permanently added 'XXX.XXX.XX.XXX' (ECDSA) to the list of known hosts.
```
Enter the password provided at the beginning of the workshop. Ask one of the demonstrators if you've forgotten it. 
```default
Enter password:
```
::: {.callout-note appearance="simple"}
## Pay Attention
When you type a password on the terminal, there will not be any indication the password is being entered. You'll not see a moving cursor, or even any asterisks, or bullets. That is an intentional security mechanism used by all terminal applications and can trip us up sometimes, so be careful when typing or copying your password in.  
:::
    
Having successfully logged in, your terminal should then display something like that shown in the figure below:

![](/fig/Nimbus_login_screen_with_border.png)

**Congratulations, you have now successfully logged on to your instance!**


## **Check your web browser**
We will be using a web browser to view output `.html` files generated by the nf-core pipeline for part 1 of the workshop and run Rstudio for part 2. We recommend using [Google Chrome](https://www.google.com/intl/en_au/chrome/) or Safari (for Mac users). Participants using Firefox may experience issues with running Rstudio. 


<br>
<div class="keypoints">
### **Key points**

- You'll need a terminal application to access the command line of your Nimbus instance. 
- Safari or Chrome web browsers are required for this workshop. 
- Use a ssh connection to login to your Nimbus instance.     
</div>  
