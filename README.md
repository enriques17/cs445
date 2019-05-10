# Reverse ssh tunneler with RaspberryPi


Convert a Raspberry Pi B+ into a reverse ssh tunneler that will automatically connect to a host server via ssh. This allows full access to the network the Pi is connected to, via ethernet, from the host server without entering a password.
## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

You will need:
  * RaspberryPi B+,
  * A server with a static IP address, this can be in the form of a cloud server or a Linux box.
  * An SD card flashed with a Rasbian image. A tutorial to load Rasbian can be found [here.](https://www.raspberrypi.org/downloads/noobs/
 "Download NOOBS")

## 1.  Ensure that SSH is enabled on the Pi
  #### A. Enable with GUI
   1. Launch ``` Raspberry Pi Configuration ``` from the ``` Preferences ``` menu.
   2. Navigate to the ```Interfaces``` tab.
   3. Select ```Enabled``` next to ```SSH```.

  #### B. Enable via terminal
   1. Enter ```sudo raspi-config``` in a terminal window
   2. Select ```Interfacing Options```
   3. Navigate to and select ```SSH```
   4. Choose ```Yes```
   5. Select ```Ok```
   6. Choose ```Finish```

## 2. Set Up SSH without password

#### Create a private key on the source computer (Raspberry Pi)
  1. Generate an ssh key with:
  ```
  cd ~/.ssh
  ssh-keygen -t rsa
  ```
  2. Choose no passphrase when asked and accept the default filename of id_rsa. This creates both the id_rsa private key file and id_rsa.pub public key file. Keep the private key on the source system and copy the public key to the destination system.
  3. Create authorized key file.

  4. Put id_rsa.pub into file named ``` authorized_keys ```.

  5. Put private key from server into the Pi's ``` ~/.ssh/ ``` directory.

#### Move the private key to the Static IP Server
  #### 1. If you have a remote host you can use SCP to transfer private key from the Raspberry Pi to the Static IP Server.
   To do this run on the Raspberry Pi:
    ``` scp id_rsa <staticip>@<xx.xx.xx.x>:~/ ```
   Ensure that the path to ```id_rsa``` is correct.

  #### 2. If you don't have a remote host.
   You can just copy the ``` id_rsa ``` file and email it to yourself.
   Copy the file and manually place it in ``` ~/.ssh ``` on the server.

  #### 3. Test to see if this worked.
   1. On the Raspberry Pi run ``` ifconfig ```, this will return an inet address for ```eth0 ```
   2. On the server run ``` ssh pi@xxx.xxx.xx.x ``` (replace the x's with inet address from the previous step).
   3. If this gives you access to th server without a password prompt you set it up correctly.

## 3. Creating the Reverse SSH tunnel
 1. Navigate to ```sshd_config``` on th Pi. Run:
 ```
 sudo nano ~/etc/ssh/sshd_config
 ```
 2. Look for commented portion that says ```#Port 22``` and change it to ``` Port 4444 ```
 3. Do these same steps on the server but change it to ``` Port 2222 ```.
 4. On the Pi run
```
/usr/bin/ssh -p 2222 -v -N -R 5555:localhost:4444 <server>@<xx.xx.xx>
```


## Authors

* **Jackson Melcher** - [jacksonmelcher](https://github.com/PurpleBooth)
* **James Crocitto** - [jacrocitto](https://github.com/jacrocitto)
* **Enrique Sandoval** - [Enriques17](https://github.com/enriques17)

See also the list of [contributors](https://github.com/enriques17/cs445/graphs/contributors) who participated in this project.
