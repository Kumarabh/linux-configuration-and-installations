
# https://phoenixnap.com/kb/install-java-ubuntu

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

* Verify that you have not already installed Java
* Issue the sudo apt update command
* Install Ubuntu’s default JDK with apt
* Run Java on the command line to test the install
* Set JAVA_HOME globally for all Ubuntu users

#### Default version 11
```
java - version // Command 'java' not found, but can be installed with:
sudo apt install default-jdk
sudo apt install default-jre
```

#### version 17
```
apt-get install wget
sudo apt install libc6-i386 libc6-x32 libxi6 libxtst6 -y
wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.deb
sudo dpkg -i jdk-17_linux-x64_bin.deb
java -version
```

#### install specific version
```
sudo apt install openjdk-#-jdk
```
#### Choose a java version from your system if have multiple installed
```
sudo update-alternatives --config java
```

#### Remove default java
```
sudo apt remove default-jdk
```

#### Remove java version
```
sudo apt remove openjdk-#-jdk
```


#### Locate your Java installation on Ubuntu
```
update-alternatives --config java
```

#### Add JAVA_HOME to the environment
```
sudo nano /etc/environment
```
