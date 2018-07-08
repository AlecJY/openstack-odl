# Guide how to setup Openstack Ocata and Open Day Light using devstack
# System requirements
- Virtual machine on a real ESXi/KVM/Xen/etc. hypervisor, or a bare metal server with virtualization support
- 8 GB of RAM (minimum)
- 4 cores of CPU (minimum)
- 100 GB of hard disk space (minimum)
- An updated Ubuntu 16.04 LTS server
- Static IP

# Update and install dependencies
First, you must update Ubuntu
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```
Once those commands have completed, you'll need to install git.

```
sudo apt-get install git
```
Next we need to install java 7 manualy
## Installing JDK
Because Ubuntu 16.04 LTS no longer provides Oracle JDK 7 packages, so you need to install OpenJDK 7 yourself.
```
sudo su
add-apt-repository ppa:openjdk-r/ppa  
apt-get update   
apt-get install openjdk-7-jdk  
```
## Verify your installation
Verify that java has been successfully configured by running:
```
update-alternatives --display java
update-alternatives --display javac
```
The output should look like this:
```
java - auto mode
  link best version is /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java
  link currently points to /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java
  link java is /usr/bin/java
  slave java.1.gz is /usr/share/man/man1/java.1.gz
/usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java - priority 1071
  slave java.1.gz: /usr/lib/jvm/java-7-openjdk-amd64/jre/man/man1/java.1.gz

javac - auto mode
  link best version is /usr/lib/jvm/java-7-openjdk-amd64/bin/javac
  link currently points to /usr/lib/jvm/java-7-openjdk-amd64/bin/javac
  link javac is /usr/bin/javac
  slave javac.1.gz is /usr/share/man/man1/javac.1.gz
/usr/lib/jvm/java-7-openjdk-amd64/bin/javac - priority 1071
  slave javac.1.gz: /usr/lib/jvm/java-7-openjdk-amd64/man/man1/javac.1.gz
```
Another easy way to check your installation is:
```
java -version
```
The output should look like this:
```
java version "1.7.0_95"
OpenJDK Runtime Environment (IcedTea 2.6.4) (7u95-2.6.4-3)
OpenJDK 64-Bit Server VM (build 24.95-b01, mixed mode)
```    
# Clone devstack
We're going to use git to clone devstack. To do this, go back to your terminal window and issue the following two commands:

```
cd /
sudo git clone https://git.openstack.org/openstack-dev/devstack -b stable/ocata
```
Next, we have to create local config file. In this repo, I have included `local.conf` for serveral case, but the case we are going to use is `allinone` `multi-node`. Select local.conf file in `compute` or `control` folder and paste it to `local.conf` file in ubuntu server

```
cd devstack
sudo nano local.conf
```
Next we'll run a script to create a new user for OpenStack, then make that new user the owner of the devstack folder.
```
sudo /devstack/tools/create-stack-user.sh
sudo chown -R stack:stack /devstack
```
For the error `can not determine HOST_IP` we need to open `stackrc` in devstack folder go to line 749 and enter the HOST_IP manually
Now we need to execute the following command to begin the installation openstack. This will take several minutes to complete.
```
sudo su stack
/devstack/stack.sh
```
Drink a cup of tea and wait then you will have the OpenStack and OpenDayLight installed on your machine. The Compute node just need to repeat the same
