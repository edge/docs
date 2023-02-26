---
description: >-
  Upon the creation of a new Ubuntu 22.04 Edge Server, it is vital to perform
  critical configuration steps as part of the initial setup to secure the
  server.
---

# Base Configuration for Ubuntu 22.04

<figure><img src="../../../.gitbook/assets/ubuntu.png" alt=""><figcaption></figcaption></figure>

## Introduction

Upon the creation of a new Ubuntu 22.04 Edge Server, it is vital to perform critical configuration steps as part of the initial setup to improve the server's security and usability, creating a stable foundation for future actions.

## Tutorial

### 1. Logging in as root <a href="#step-1-logging-in-as-root" id="step-1-logging-in-as-root"></a>

To log into your Edge Server, you will need to know your **server’s public IP address**. You will also need the password or the private key for the **root** user’s account if you installed an SSH key for authentication. If you have not already logged into your server, you may want to follow our guide on how to Connect to Edge Servers with SSH, which covers this process in detail:

{% content-ref url="../connect-to-edge-servers-with-ssh.md" %}
[connect-to-edge-servers-with-ssh.md](../connect-to-edge-servers-with-ssh.md)
{% endcontent-ref %}

If you are not connected to your server currently, log in as the **root** user using the following command. Substitute the highlighted `your_server_ip` portion of the command with your server’s public IP address:

```
ssh root@your_server_ip
```

Accept the warning about host authenticity if it appears.

If your server uses password authentication, provide your **root** password to log in. If you use an SSH key that is passphrase protected, you may need to enter the passphrase the first time you use the key each session.

If you do not know your Edge Server’s IP address, you can find it in your Edge Account:

<figure><img src="../../../.gitbook/assets/Screenshot-2023-02-25-at-23.45.18.png" alt=""><figcaption></figcaption></figure>

#### About root

The **root** user is the administrative user in a Linux environment. It has elevated privileges and full access to the operating system. Because of this, you are _discouraged_ from using it regularly. The **root** account can make destructive changes and you will be surprised how easy it is to do this by accident!

The next step is setting up a new user with reduced privileges specifically for day-to-day use.

### 2. Creating a New User

Once you log in as **root**, you’ll be able to add the new user account. In the future, you’ll log in with this new account instead of **root**.

This example creates a new user called **adam**, but you can replace that with any username that you like:

```
adduser adam
```

You will be asked a few questions, starting with the account password.

Enter a strong password and optionally fill in any of the additional information if you would like. This information is not required, and you can press `ENTER` in any field you wish to skip.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-02-26 at 12.29.32.png" alt=""><figcaption></figcaption></figure>

### 3. Granting Administrative Privileges

Now you have a new user account with regular account privileges. However, you will sometimes need to perform administrative tasks as the **root** user.

To avoid logging out of your regular user and logging back in as the **root** account, you can set up what is known as _superuser_ or **root** privileges for your user’s regular account. These privileges will allow your normal user to run commands with administrative privileges by putting the word `sudo` before the command.

To add these privileges to your new user you will need to add the user to the **sudo** system group. By default on Ubuntu 22.04, users who are members of the **sudo** group are allowed to use the `sudo`command.

As **root**, run this command to add your new user to the **sudo** group (substitute the highlighted `adam`username with your new user):

```
usermod -aG sudo sammy
```

You can now type `sudo` before commands to run them with superuser privileges when logged in as your regular user.

### 4. Securing Your Edge Server with Fail2Ban

Fail2Ban is a log-parsing application that protects Linux based servers against many security threats, such as dictionary, DoS, DDoS, and brute-force attacks. It works by monitoring system logs for any malicious activity and scanning files for any entries matching identified patterns.

It is recommended that you install Fail2Ban on your Edge Server. A basic setup is described here. An enhanced tutorial that shows you how to customise the installation is being written and will be published soon.

Fail2ban is available in the default Ubuntu repository, so we can simply run the following command to install it:

```
sudo apt install fail2ban -y
```

Then, run this command to enable and run fail2ban

```
sudo systemctl enable --now fail2ban
```

Fail2ban is now installed and running. You can verify this by invoking this command:

```
sudo systemctl status fail2ban
```

{% hint style="info" %}
**A more detailed configuration tutorial for Fail2Ban will be published soon**
{% endhint %}

### 5. Securing Your Edge Server with a Firewall

Edge Servers running Ubuntu 22.04 can use the UFW firewall to ensure that only connections to certain services are allowed. You can set up a basic firewall quiclkly using this application.

Applications are able to register their profiles with UFW upon installation. These profiles allow UFW to manage these applications by name. OpenSSH – the service that allows you to connect to your Edge Server – has a profile registered with UFW.

You can examine the list of installed UFW profiles by typing:

```
ufw app list
```

You will see a response like this:

```
Available applications:
  OpenSSH
```

You will need to make sure that the firewall allows SSH connections so that you can log into your Edge Server. You can allow these connections by typing:

```
ufw allow OpenSSH
```

Now enable the firewall by typing:

```
ufw enable
```

Type `y` and press `ENTER` to proceed. You can see that SSH connections are still allowed by typing:

```
ufw status
```

```
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
```

**The firewall is now blocking all connections except for SSH**. If you install and configure additional services (such as Apache), you will need to adjust the firewall settings to allow the new traffic to connect to your server.

{% hint style="info" %}
**A more detailed configuration tutorial for UFW will be published soon**
{% endhint %}

### 6. Enabling External Access for Your Regular User

Now that you have a regular user for daily use, you will need to make sure that you can SSH into the account directly.

Note that until you have verified that you can log in and use `sudo` with your new user, we recommend staying logged in as **root**. If you have problems connecting, you can troubleshoot and make any necessary changes as **root**.

Configuring SSH access for your new user depends on whether your server’s **root** account uses a password or SSH keys for authentication.

#### If the root Account Uses Password Authentication

If you logged in to your **root** account _using a password,_ password authentication is _enabled_ for SSH. You can SSH to your new user account by opening up a new terminal session and using SSH with your new username:

```
ssh adam@your_server_ip
```

After entering your regular user’s password, you will be logged in. Remember that if you need to run a command with administrative privileges, type `sudo` before it like this:

```
sudo command_to_run
```

You will receive a prompt for your regular user’s password when using `sudo` for the first time each session (and periodically afterward).

To enhance your server’s security, **we strongly recommend setting up SSH keys instead of using password authentication**. A guide for setting up SSH Keys on your Ubuntu 22.04 Edge Server will be published soon.

{% hint style="info" %}
**A more tutorial for setting up SSH Keys will be published soon**
{% endhint %}

#### If the root Account Uses SSH Key Authentication

If you logged in to your **root** account _using an SSH key_, then password authentication is _disabled_ for SSH. To log in as your regular user with an SSH key, you must add a copy of your local public key to your new user’s `~/.ssh/authorized_keys` file.

Since your public key is already in the **root** account’s `~/.ssh/authorized_keys` file on the server, you can copy that file and directory structure to your new user account using your current session.

The simplest way to copy the files with the correct ownership and permissions is with the `rsync`command. This command will copy the **root** user’s `.ssh` directory, preserve the permissions and modify the file owners in a single command. Make sure to change the highlighted portions of the command below to match your regular user’s name:

```
rsync --archive --chown=adam:adam ~/.ssh /home/adam
```

Note that the `rsync` command treats sources and destinations that end with a trailing slash differently than those without a trailing slash. When using `rsync`, ensure that the source directory (`~/.ssh`) **does not** include a trailing slash (check to make sure you are not using `~/.ssh/`).

If you accidentally add a trailing slash to the command, `rsync` will copy the _contents_ of the **root** account’s `~/.ssh` directory to the `sudo` user’s home directory instead of copying the entire `~/.ssh` directory structure. In this instance the files will be in the wrong location and SSH will not be able to find and use them.

Next, open a new terminal session on your local machine and use SSH with your new username:

```
ssh adam@your_server_ip
```

You should be connected to your server with the new user account without using a password. Remember that if you need to run a command with administrative privileges, type `sudo` before the command like this:

```
sudo command_to_run
```

You will be prompted for your regular user’s password when using `sudo` for the first time each session (and periodically afterward).

### Conclusion

You now have a solid foundation for your Edge Server and can safely proceed to install any additional software that you need.
