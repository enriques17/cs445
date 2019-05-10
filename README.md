# Reverse ssh tunneler with RaspberryPi


Convert a Raspberry Pi B+ into a reverse ssh tunnler that will automatically connect to a host server via ssh. This allows full access to the network the Pi is connected to, via ethernet, from the host server without entering a password.
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
  Create authorized key file

  Put id_rsa.pub into file

  give private key to server

#### Move the private key to the Static IP Server
  #### 1. If you have a remote host you can use SCP to transfer private key from the Raspberry Pi to the Static IP Server. 
   To do this run on the Raspberry Pi: 
    ``` scp id_rsa <staticip>@<xx.xx.xx.x>:~/ ``` 
   Ensure that the path to ```id_rsa``` is correct.

  #### 2. If you don't have a remote host.
    You can just copy the ``` id_rsa ``` file and email it to yourself. 
    Copy the file and manually place it in ``` ~/.ssh ``` on the server.

#### 3. Test to see if this worked.
  1. On the Raspberry Pi run:
  ```
  ifconfig
  ```
and then on the 

from the Pi
If this gives you access to th server without a password prompt you set it up correctly.
## 3. Creating the Reverse SSH tunnel

On the Pi run
```
ssh -N -R 4444:localhost:22 <googlecloud>@<xx.xx.xx.x>
```

<!-- ### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags).

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc -->
