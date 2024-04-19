
#### pull docker image from docker hub
```
docker pull ubuntu 
```

#### run ubuntu image interactive
``` 
docker run -it --name=c1 ubuntu
```

``` 
apt-get update
apt-get install sudo
apt-get install nano
```

#### set password for root
``` sudo passwd root```

#### Java installation
To quickly setup and install Java on Ubuntu, follow these steps:

-Verify that you have not already installed Java
-Issue the sudo apt update command
-Install Ubuntu’s default JDK with apt
-Run Java on the command line to test the install
-Set JAVA_HOME globally for all Ubuntu users

```
java - version // Command 'java' not found, but can be installed with:
sudo apt install default-jdk
sudo apt install default-jre
```

