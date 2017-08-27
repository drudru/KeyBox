
Instructions
------------

## Passwords

This document is going to need a lot of work, but for right now, the GUI on the device should be self explanatory.

## Serial Console

If you need to access the device, you can access the device for debugging purposes via the built in 
UART/serial-port. It is a 3.3V serial that runs at 115200 bps. The login user is 'pi' without a password.

If you install an ssh public key in /home/pi/.ssh/authorized_keys, you can then login via 'ssh pi@keybox.local'.
Note, it may hang the first time you do this (at least it does on my Mac OS X system). The reason is that the mDNS/Zeroconf/Bonjour/ahavi name lookup is failing. Just hit ctrl-c on the ssh and run it again, it should login in about 1 second.

## SSH Authentication

Once you have your ssh keys on the device, you can forward all of your ssh authentication requests to it.

To do this, just set the ssh environment variable to:

```sh
export SSH_AUTH_SOCK=/tmp/ssh-agent
```

Next, get the IP address of the device. You can just 'ping keybox.local' to do that.


Then in another window, use socat to listen on that Unix domain socket and forward packets to the device.

```sh
rm /tmp/ssh-agent ; socat -d UNIX-LISTEN:/tmp/ssh-agent,fork TCP4:169.254.158.207:2222
```

Once you do that, all of your ssh requests will forward to the device to be confirmed manually by you.
Test it out. You should hear the piezo make some sound and it should show a confirmation screen.

Congratulations, your ssh-keys are now more secure because they are not on your computer.




