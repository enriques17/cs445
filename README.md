# Reverse ssh tunneler with RaspberryPi



## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

You will need a RaspberryPi B+,
A separate server, this can be in the form of a cloud server or a Linux box.

```
What does this look like
```
### Ensure that SSH is enabled on the Pi
#### Enable with GUI

1. Launch ``` Raspberry Pi Configuration ``` from the ``` Preferences ``` menu.
2. Navigate to the ```Interfaces``` tab.
3. Select ```Enabled``` next to ```SSH```.

#### Enable via terminal

1. Enter ```sudo raspi-config``` in a terminal window
2. Select ```Interfacing Options```
3. Navigate to and select ```SSH```
4. Choose ```Yes```
5. Select ```Ok```
6. Choose ```Finish```

### Set Up SSH without password

#### Create a private key on the source computer (RaspberryPi)

Generate an ssh key with:
```
cd ~/.ssh
ssh-keygen -t rsa
```

#### Move the public key to the destination computer (Google Cloud)

Use SCP to transfer public key from the RaspberryPi to the Google Server.
```
scp id_rsa.pub <googlecloud>@<xx.xx.xx.x>:.ssh/authorized_keys
```
Ensure that the path to ```id_rsa.pub``` is correct.

You can test to see if this worked by running
```
ssh <googlecloud>@<xx.xx.xx.x>
```
if this gives you access to the Google server without a password prompt you set it up correctly.

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

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
* etc
