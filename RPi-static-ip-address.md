#How to set up up your Raspberry Pi to have a static IP address

Usually when you connect a Raspberry Pi to a Local Area Network (LAN) it is automatically assigned an IP address. Typically, this address will change each time you connect.

 Sometimes, however, you might want your Pi to boot up with the same IP address each time. This can be useful if you are making a small, self contained network or building a standalone project such as a robot. Here's how to do it.

##Setup

Edit the file `/etc/network/interfaces` as follows: 

1. Type `sudo nano /etc/network/interfaces` at the command prompt.

2. Look for the line:
```
iface eth0 inet dhcp
```
3. Change the word `dhcp` to `static`

4. Press `Enter` and add the following lines:


```
address 192.168.0.2
netmask 255.255.255.0
network 192.168.0.0
broadcast 192.168.0.255
gateway 192.168.0.1
```

5. Save the file with `CTRL-o` and then exit nano with `CTRL-x`.

Your Raspberry Pi will now boot up with the IP address 192.168.0.2 every time (we didn't use 192.168.0.2.1 as this is reserved for the router). You can of course use any address you like, but in the configuration above the range must be 192.168.0.2 to 192.168.0.255.

##Testing

1. Reboot with `sudo reboot`

2. Log in and type `ip a`

3. You should see the IP address you set in the `eth0:` entry.

##Troubleshooting
If your Pi is not networked then the IP address may not show. Either connect your Pi to an active network socket (this can be on another booted Raspberry Pi) or manually bring up (activate) the network interface by typing `sudo ifup eth0` followed by `ip a`.

If you still cannot see your IP address, or it is different to the one you set, then open the `interfaces` file, as in step 1 of Setup, and check that your edits are correct.


