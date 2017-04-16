# Vagrant Setup

## Why Vagrant?

- Vagrant provides easy to configure, reproducible, and portable work environments. With this ability someone can build a test environment on their own laptop/pc and start working on a project.

- Vagrant also provide full OS capability. Unlike containers (docker),Vagrant provisioned a VM on top of providers like Vmware, virtualbox and AWS.

- Vagrant isolates dependencies and configuration within a single disposable, consistent environment, without sacrificing any of the tools you are used to working. It will also provide consistent workflow for developing and testing infrastructure management scripts.

## The Purpose:

- The aim of this document is to provide guidance for the team members who wanted to learn Ansible using their own laptop/pc anytime they need without the need of other people to setup an environment for that purpose.

- This document will try to provide a detailed step to setup vagrant environment with 3 VM’s running so that you can start your learning using ansible in the most controlled environment and without reliance to other people.

- Vagrant will provide an environment that can be stand up in no time and destroy anytime to build a fresh environment.

## General Requirements:

- Internet access is a must!
- VT support is enabled on your pc/laptop bios!
- Install Notepad++ - <https://notepad-plus-plus.org/download/v7.3.3.html>
- Vagrant - <https://www.vagrantup.com/downloads.html>
- Virtualbox - <https://www.virtualbox.org/wiki/Downloads>

## For **Windows **desktop, you need an additional package to be installed.

This is to enable the ssh client on your desktop.
- git – <http://git.scm.com/downloads>
**Note**: If you have hyperv installed on you laptop, this will cause
virtualbox to show 32bit OS support only and will make the vagrant vm
build failed.

## In short:

- Your Host OS is 64-bits
- Intel Virtualization Technology and VT-d are both enabled in the BIOS
- The Hyper-V platform is disabled in your Windows Feature list.

**Follow the steps on this link to solve this issue:**
http://www.fixedbyvonnie.com/2014/11/virtualbox-showing-32-bit-guest-versions-64-bit-host-os/#.WOLH2leb1hE

## Vagrant Environment Setup

For Linux:
1. Install vagrant:
 * yum install vagrant*
-   After installation, you need to make sure that the following vagrant plugins are installed as well.
``
[root@fedora-pc ~]# vagrant plugin list
 vagrant-proxyconf (1.5.2)
``
To install the plugins, simple issue this command: 
``
vagrant plugin install vagrant-proxyconf*
``
**vagrant-proxyconf** is needed to enable proxy during vm build under vagrant environment.

Note, in some cases, you might need to install the following plugins as
well. But on for this exercise, you won’t need it.

vagrant-vbguest

2\. Install virtualbox:

** **wget
http://download.virtualbox.org/virtualbox/rpm/rhel/virtualbox.repo
 yum --enablerepo=epel install dkms
 yum groupinstall "Development Tools"
 yum install VirtualBox

## For Windows:

1.  Enable Proxy:
** ** Open your command line and issue this command.
* set http_proxy=http://username:*[*password@proxyserver*](mailto:password@proxyserver)*:port*

* set https_proxy=http://username:*[*password@proxyserver*](mailto:password@proxyserver)*:port*

To verify the proxy settings:

  * echo %https\_proxy%*
  * echo %http\_proxy%*

1.  Download and install vagrant from this link:
    <https://www.vagrantup.com/downloads.html>

Note: It is also required to install vagrant proxy plugin.

To install the plugins, simple issue this command: *vagrant plugin
install vagrant-proxyconf*

To verify if plugin is successfully installed: *vagrant plugin list*

vagrant plugin list

vagrant-proxyconf (1.5.2)

**vagrant-proxyconf** is needed to enable proxy during vm build under
vagrant environment

If you encounter issue below: Verify your proxy settings and make sure
you provide the correct username and password.

3\. Download and install virtualbox from this link:
<https://www.virtualbox.org/wiki/Downloads>

4\. Download and install git from this link:
<http://git-scm.co/downloads>. 

Note: if you are somehow being ask to login on github, go to google and
type “git for windows download”. The first link will bring you to the
download site. Choose 64 bit installer

In installing GIT this is the key to enable ssh on windows using Git
client. Select ***Use Git and optional Unix tools from the Windows
Command Prompt"*****.**

If in case you have a git installed in your system already, you will
have to do manually what the installation of Git could have done for
you, but fortunately it is quite trivial:

-   Open the Control Panel
-   Go to System and Security
-   Click on System, then on the Change Settings button
-   Display the Advanced tab and click on Environment Variables...
-   Look for the Path variable in the System variables list, select
    it then Edit...

At the end of the string, add the path to Git's bin (something
like "C:\\Program Files\\Git\\bin") (don't forget to add a semicolon
first to separate it from the previous path):

**Note:** Vagrant install and Virtualbox install require reboot. So wait
until you finish all the installation before you reboot to save some
time.

Environment Setup:

Once the required packages are installed. You then need to setup your
environment so that Vagrant can connect to the internet. In most cases
you need to enable proxy to do this. Here are the steps to enable that.

Linux:

Update the file /etc/environment and put this line

export https\_proxy=http://username:passwd@dnzwgpx2.datacom.co.nz:80

*export
http\_proxy=http://username:*[*passwd@dnzwgpx2.datacom.co.nz*](mailto:passwd@dnzwgpx2.datacom.co.nz)*:80*

Then, issue this command to refresh the environment: *source
/etc/environment*

You can also verify your proxy settings using this command:* env | grep
proxy*

Windows:

Open your command line and issue this command.

 * set
http\_proxy=http://username:*[*password@proxyserver*](mailto:password@proxyserver)*:port*

* set
https\_proxy=http://username:*[*password@proxyserver*](mailto:password@proxyserver)*:port*

To verify the proxy settings:

 * echo %https\_proxy%*

* echo %http\_proxy%*

Note: Unlike Linux, every time you close or open your command line you
need to redo this steps.

**Putting it together:**

Once the initial setup is done, you are now ready to build your Vagrant
environment to start your ansible training.

1.  Download the vagrant box needed for this training from

<http://repo.alabs.datacom.co.nz/repo/vagrant/ansible-training/>

Once you have downloaded the vagrant boxes, you need to add it to active
vagrant box so vagrant can use it during provisioning.

vagrant box add Datacom\_Centos7.3\_gui\_v2
Datacom\_Centos7.3\_gui\_v2.box

vagrant box add Datacom\_Centos7.2base Datacom\_Centos7.2base

For Windows user, you need to use this command: Somehow, the other box
is downloaded as tar so make sure you are pointing to the correct file.

*vagrant box add Datacom\_Centos7.2base Datacom\_Centos7.tar*

below show the successful load of vagrant box to vagrant registry.

To verify if you successfully uploaded, issue this command:

*vagrant box list*

Datacom\_Centos7.2base (virtualbox, 0)

Datacom\_Centos7.3GUI (virtualbox, 0)

**Linux:**

1.  **Download the session-1 training package** from this location:

<https://github.com/mikecali/vagrant-session-1>

*\$*git clone <https://github.com/mikecali/vagrant-session-1.git>

**Windows:**

1.  Download the files from this link:
    <https://github.com/mikecali/vagrant-session-1.git> and unzip it on
    location of your choice. (I would advice to put this on your desktop
    for now).

Firing up your vagrant box:

Now that you have the files needed to build your training environment.
Unzip the file It is now time to build your environment.

Before you build your environment:

-   Change directory to the location of the folder that you downloaded
    from vagrant box.

-   Make sure you update the Vagrantfile to reflect your
    username/password on the proxy variable. Look for something
    like below. I use sublime or notepad++ to edit this files.

Note: for passwords with spaces the format that is accepted is:

Sample password: **pa ss word ! **

 Vagrantfile:
*config.proxy.http="http://username:*pa%20ss%20word!*@dnzwgpx2.datacom.co.nz:80*

-   MAKE SURE that the virtualbox is running/open

 boxes.each do |opts|

 config.vm.define opts\[:name\] do |config|

*\$ Only Enable this if you are connecting to Proxy server*

*
config.proxy.http="http://username:password@dnzwgpx2.datacom.co.nz:80"*

*
config.proxy.https="http://username:password@dnzwgpx2.datacom.co.nz:80"*

 config.proxy.no\_proxy = "localhost,127.0.0.1"

 config.vm.synced\_folder ".", "/vagrant", id: "vagrant-root", disabled:
true

Issue the command below to bring up your environment: *Make sure you are
inside the directory of the vagrant-session-1-master*

*vagrant up*

**Note for Windows user: **If you open the Virtualbox as admin, you
should also run the command vagrant up as administrator. If you don’t do
this, your build will sometimes fail.

Output similar to below should come out.

*\[mikecali@fedora-pc vagrant-session-1\]\$ vagrant up*

*Bringing machine 'client2' up with 'virtualbox' provider...*

*Bringing machine 'client1' up with 'virtualbox' provider...*

*Bringing machine 'ansible-host' up with 'virtualbox' provider...*

*==&gt; client2: Importing base box 'bento/centos-7.2'...*

*==&gt; client2: Matching MAC address for NAT networking...*

*==&gt; client2: Checking if box 'bento/centos-7.2' is up to date...*

*==&gt; client2: Setting the name of the VM:
vagrant-session-1\_client2\_1490554768542\_54140*

*==&gt; client2: Clearing any previously set network interfaces...*

*==&gt; client2: Preparing network interfaces based on configuration...*

* client2: Adapter 1: nat*

* client2: Adapter 2: hostonly*

Once the process is done, you can then issue to command below to show
the status of your vagrant environment:

*vagrant status*

This command will display if the 3 vms are created successfully. You
should see the state “running”

You should see similar output as below:

\[mikecali@fedora-pc vagrant-session-1\]\$ vagrant status

Current machine states:

client2 running (virtualbox)

client1 running (virtualbox)

ansible-host running(virtualbox)

In some cases, that you encounter issue on your build, simply destroy
the VM and re-create it.

Sample output of unsuccessful build:

vagrant status

Current machine states:

client2 running (virtualbox)

*client1 not created (virtualbox)*

*ansible-host not created(virtualbox)*

To destroy the VM: *vagrant destroy*

Similar output below should show:

vagrant destroy

 ansible-host: Are you sure you want to destroy the 'ansible-host' VM?
\[y/N\] y

==&gt; ansible-host: Destroying VM and associated drives...

 client1: Are you sure you want to destroy the 'client1' VM? \[y/N\] y

==&gt; client1: Destroying VM and associated drives...

Once you have your environment running, you can now login to your VM’s

*vagrant ssh ansible-host *

*The above command will enable you to login to ansible-host vm that was
recently created by vagrant up command*

If login is successful, you should see similar output below.

*\[mikecali@fedora-pc vagrant-session-1\]\$ vagrant ssh ansible-host*

*Last login: Sun Mar 26 15:07:56 2017*

*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*\* \**

*\* This system is built specifically for Ansible BAU training.. \**

*\* Don't use this system for Production Deployment. \**

*\* \**

*\* \**

*\* DATACOM/Centos-7.3\_GUI version: 1.0 \**

*\* Built by: MC \**

*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*\[vagrant@ansible-host \~\]\$*

Once you are login to ansible-host vm, you can then play a simple
playbook to ping the other 2 hosts. Below is the command:

*Note that you need to type yes 2 times because it will the the first
time for the ansible-host to establish a connection.*

*\[vagrant@ansible-host \~\]\$ ansible-playbook -i inventory
playbooks/ping.yml*

*PLAY \[all\]
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*TASK \[setup\]
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*The authenticity of host '192.168.29.2 (192.168.29.2)' can't be
established.*

*ECDSA key fingerprint is
fa:c7:04:e6:3a:97:9d:f2:23:b9:ed:53:09:1b:b8:72.*

*Are you sure you want to continue connecting (yes/no)? The authenticity
of host '192.168.29.3 (192.168.29.3)' can't be established.*

*ECDSA key fingerprint is
fa:c7:04:e6:3a:97:9d:f2:23:b9:ed:53:09:1b:b8:72.*

*Are you sure you want to continue connecting (yes/no)? yes*

*ok: \[192.168.29.2\]*

*yes*

*ok: \[192.168.29.3\]*

*TASK \[ping\]
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*ok: \[192.168.29.3\]*

*ok: \[192.168.29.2\]*

*PLAY RECAP
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*192.168.29.2 : ok=2 changed=0 unreachable=0 failed=0 *

*192.168.29.3 : ok=2 changed=0 unreachable=0 failed=0 *

*\[vagrant@ansible-host \~\]\$*

The above playbook basically ping the other 2 vm’s that was created by
vagrant up command:

You can also try use the playbook below to verify if mysql and apache
are installed to the box.

*\[vagrant@ansible-host \~\]\$ ansible-playbook -i inventory
playbooks/verify-install.yml*

*PLAY \[all\]
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*TASK \[verify if apache is installed\]
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*changed: \[192.168.29.2\]*

* \[WARNING\]: Consider using yum, dnf or zypper module rather than
running rpm*

*changed: \[192.168.29.3\]*

*TASK \[debug\]
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*ok: \[192.168.29.2\] =&gt; {*

* "msg": ""*

*}*

*ok: \[192.168.29.3\] =&gt; {*

* "msg": ""*

*}*

*TASK \[verify if mariadb is installed\]
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*changed: \[192.168.29.3\]*

*changed: \[192.168.29.2\]*

*TASK \[debug\]
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*ok: \[192.168.29.2\] =&gt; {*

* "msg": ""*

*}*

*ok: \[192.168.29.3\] =&gt; {*

* "msg": ""*

*}*

*PLAY RECAP
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\**

*192.168.29.2 : ok=4 changed=2 unreachable=0 failed=0 *

*192.168.29.3 : ok=4 changed=2 unreachable=0 failed=0 *

*\[vagrant@ansible-host \~\]\$*

To login to the **vm** console (ansible-host):

1.  Go to your virtualbox and double click the vm with the
    name ansible-host.
2.  Login using vagrant default credential

Username: vagrant

Password: vagrant

1.  Once you are login, you can open atom to edit/update your playbooks.

You can open atom from your ansible-host by opening a terminal and
issuing the command below:

\[vagrant@ansible-host \~\]\$ atom

Atom is a software that you can run on ansible-host vm to view/edit
ansible playbooks using a GUI.

1.  Using Atom you can now edit/create playbooks located on this path:

/home/vagrant/playbooks

List of playbooks baked with the vagrant boxes:

-   ping.yml - a sample playbook to check if all vms are reachable from
    Ansible-host
-   apache.yml - a sample playbook that will install apache and
    configure firewalld to allow port 80 traffic
-   mysql.yml - a sample playbook that will install mysql and configure
    firewalld to allow port 3306 traffic
-   verify-install.yml - a sample playbook to verify if apache and mysql
    are installed
-   update-hostname.yml – a sample playbook that will change a
    server hostname. This time utilizing a simple variables.
-   lamp.yml – a sample playbook that will build LAMP stack on a
    target server.

**Some useful Vagrant commands that you will be needed:**

vagrant status – to view the current status of the vagrant vm on the
specific environment

vagrant up – to bring up the vagrant box using the Vagrantfile.

vagrant up (vm name) – to start/build vagrant vm using the target
Vagrantfile

vagrant box list – to list available boxes on your local vagrant
registry

vagrant box remove (name of box)– to remove the vagrant box from your
local vagrant registry

vagrant reload (box name) --provision – to re provision the vm and
re-run all the provisioner scripts defined on the Vagrantfile

vagrant destroy – to destroy/delete vagrant vm’s using the target
Vagrantfile

The next steps:

Now, that you have a working environment and have a taste of how ansible
work, It is now time for us to try some cool stuff.

The next exercise is focused on BAU support activity using ansible.

Below are the used cases for Linux/Unix BAU:

1\. adhoc-task

-   c\_logs.yml – collect logs from server
-   c\_stats.yml – collect server stats
-   c\_uptime.yml – collect server uptime
-   daily.yml – collect daily server logs
-   r\_cron.yml – edit cron jobs
-   r\_install.yml – install packages
-   r\_script.yml – run scripts

2\. User/account management

-   user\_groups - add groups.
-   user\_remove – remove userid
-   user\_add - add non-ssh Userids
-   user\_add\_ssh – add userid with SSH key

3\. Filesystem Management

-   Re-configure CPU, memory and disk resource Filesystem - disk new
-   Scan for new disk Filesystem - disk increase
-   Re-scan for disk increase Filesystem - vg create
-   Volume group creation Filesystem - vg extend
-   Volume group extension Filesystem - fs new
-   Filesystem creation Filesystem - fs increase
-   Filesystem increase Filesystem – All
-   Scan for new disk
-   Volume group creation

This playbook can be access from this link:
<https://github.com/mikecali/BAU_plays.git>

Below are the steps to get the files from the repository above.

Login to your ansible-host:

 *vagrant ssh ansible-host*

Once login to ansible-host VM, below is the command to use to get
download the files.

*git clone
*[*https://github.com/mikecali/BAU\_plays.git*](https://github.com/mikecali/BAU_plays.git)

After you downloaded the files, you then need to update the variables
needed to target the right host on which you want to use the playbooks.
