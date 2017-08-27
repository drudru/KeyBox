
Instructions
------------

## Passwords

This document is going to need a lot of work, but for right now, the GUI on the device should be self explanatory.
The device can emulate keystrokes for any file in the /boot/KeyBox/Passwords directory.

## Serial Console

If you need to access the device, you can access the device for debugging purposes via the built in 
UART/serial-port. It is a 3.3V serial that runs at 115200 bps. The login user is 'pi' without a password.

If you install an ssh public key in /home/pi/.ssh/authorized_keys, you can then login via 'ssh pi@keybox.local'.
Note, it may hang the first time you do this (at least it does on my Mac OS X system). The reason is that the mDNS/Zeroconf/Bonjour/ahavi name lookup is failing. Just hit ctrl-c on the ssh and run it again, it should login in about 1 second.

## SSH Authentication

Unfortunately (or fortunately), ssh agent forwarding only uses Unix domain sockets. In order for the KeyBox to work,
we need to forward these requests over TCP to the device. The device also has a proxy that listens on port 2222 TCP
and forwards the requests to the Unix domain socket for the ssh-agent process running there.


Step 1 is to get the ssh private keys on the device. For now, you can do that with the serial console.
In the very near future, there will be a much nicer way to do this.

Ok, once you have your ssh keys on the device, and added to ssh-agent, you can forward all of your ssh authentication requests to it.


On the ssh-client side, point at a new location via the ssh environment variable:

```sh
export SSH_AUTH_SOCK=/tmp/ssh-agent
```

Next, get the IP address of the device. You can just 'ping keybox.local' to do that.

Then in another window, use socat to listen on that Unix domain socket and forward packets to the device.

```sh
rm /tmp/ssh-agent ; socat -d UNIX-LISTEN:/tmp/ssh-agent,fork TCP4:169.254.158.207:2222
```

Leave this running. (Note: you can get socat for OS X via Homebrew).


Once you do that, all of your ssh requests will forward to the device to be confirmed manually by you.
Test it out. You should hear the piezo make some sound and it should show a confirmation screen.
If you don't answer the request, it will time out automatically in 30 seconds.


Congratulations, your ssh-keys are now more secure because they are not on your computer.




