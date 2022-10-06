# Basic Hardening
This primer will introduce you to basic Linux server security. While it focuses on Debian/Ubuntu, you can apply everything presented here to other Linux distributions.

## 1. Update your server
The first thing you should do to secure your server is to update the local repositories and upgrade the operating system and installed applications by applying the latest patches.

On Ubuntu and Debian:

```$ sudo apt update && sudo apt upgrade -y```   

On Fedora, CentOS, or RHEL:

```$ sudo dnf upgrade```  
## 2. Create a new privileged user account
Next, create a new user account. You should never log into your server as root. Instead, create your own account ("<user>"), give it sudo rights, and use it to log into your server.

### Start out by creating a new user:

`$ adduser <username>`  
Give your new user account sudo rights by appending (-a) the sudo group (-G) to the user's group membership:

`$ usermod -a -G sudo <username>`
## 3. Upload your SSH key
You'll want to use an SSH key to log into your new server. You can upload your pre-generated SSH key to your new server using the ssh-copy-id command:

`$ ssh-copy-id <username>@ip_address`  
Now you can log into your new server without having to type in a password.

## 4. Secure SSH
Next, make these three changes:

    1. Disable SSH password authentication  
    2. Restrict root from logging in remotely  
    3. Restrict access to IPv4 or IPv6  

Open **/etc/ssh/sshd_config** using your text editor of choice and ensure these lines:

**PasswordAuthentication yes**  
**PermitRootLogin yes**  

are changed to look like this:

**PasswordAuthentication no**  
**PermitRootLogin no**  

Next, restrict the SSH service to either IPv4 or IPv6 by modifying the AddressFamily option. To change it to use only IPv4 (which should be fine for most folks) make this change:

**AddressFamily inet**  
Restart the SSH service to enable your changes. Note that it's a good idea to have two active connections to your server before restarting the SSH server. Having that extra connection allows you to fix anything should the restart go wrong.

On Ubuntu:

```$ sudo service sshd restart```

On Fedora or CentOS or anything using Systemd:

`$ sudo systemctl restart sshd`  
## 5. Enable a firewall
Now you need to install a firewall, enable it, and configure it only to allow network traffic that you designate. Uncomplicated Firewall (UFW) is an easy-to-use interface to iptables that greatly simplifies the process of configuring a firewall.

You can install UFW with:

`$ sudo apt install ufw`  
By default, UFW denies all incoming connections and allows all outgoing connections. This means any application on your server can reach the internet, but anything trying to reach your server cannot connect.

First, make sure you can log in by enabling access to SSH, HTTP, and HTTPS:

`$ sudo ufw allow ssh`  
`$ sudo ufw allow http`  
`$ sudo ufw allow https`  

Then enable UFW:

`$ sudo ufw enable`  

You can see what services are allowed and denied with:

`$ sudo ufw status`  
If you ever want to disable UFW, you can do so by typing:

`$ sudo ufw disable`  

You can also use firewall-cmd, which is already installed and integrated into some distributions.

## 6. Install Fail2ban
Fail2ban is an application that examines server logs looking for repeated or automated attacks. If any are found, it will alter the firewall to block the attacker's IP address either permanently or for a specified amount of time.

You can install Fail2ban by typing:

`$ sudo apt install fail2ban -y`

Then copy the included configuration file:

`$ sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`  

And restart Fail2ban:

`$ sudo service fail2ban restart`

That's all there is to it. The software will continuously examine the log files looking for attacks. After a while, the app will build up quite a list of banned IP addresses. You can view this list by requesting the current status of the SSH service with:

`$ sudo fail2ban-client status ssh`

## 7. Remove unused network-facing services
Almost all Linux server operating systems come with a few network-facing services enabled. You'll want to keep most of them. However, there are a few that you might want to remove. You can see all running network services by using the ss command:

`$ sudo ss -atpu`  

The output from ss will differ depending on your operating system. This is an example of what you might see. It shows that the SSH (sshd) and Ngnix (nginx) services are listening and ready for connection:

```tcp LISTEN 0 128 *:http *:* users:(("nginx",pid=22563,fd=7))```   
```tcp LISTEN 0 128 *:ssh *:* users:(("sshd",pid=685,fd=3))```  
How you go about removing an unused service ("<service_name>") will differ depending on your operating system and the package manager it uses.

To remove an unused service on Debian/Ubuntu:

`$ sudo apt purge <service_name>`  

To remove an unused service on Red Hat/CentOS:

`$ sudo yum remove <service_name>`

Run `ss -atup `again to verify that the unused services are no longer installed and running.
