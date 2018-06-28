# openstack-odl
# The requirements
- Virtual machine on a real ESXi/KVM/Xen/etc. hypervisor, or a bare metal server with virtualization support
- 8 GB of RAM (minimum)
- 100 GB of hard disk space (minimum)
- An updated Ubuntu 16.04 LTS server

# Update and install dependencies
First, you must update Ubuntu. Open a terminal window and issue the commands:

`
sudo apt-get update
sudo apt-get upgrade
`
Once those commands have completed, you'll need to install git. To do this, issue the command:

`
sudo apt-get install git
`
Allow that installation to complete.

# Clone devstack
We're going to use git to clone devstack. To do this, go back to your terminal window and issue the following two commands:

`
cd /
sudo git clone https://git.openstack.org/openstack-dev/devstack master
`
Next, we have to copy the sample configuration file and set a password to be used for automated deployment. To complete this task, issue the following commands:

`
cd devstack
sudo nano local.conf
`
