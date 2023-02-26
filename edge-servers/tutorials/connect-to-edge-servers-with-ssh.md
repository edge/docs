---
description: >-
  Edge Servers are connected to via SSH or Secure Shell, a network communication
  protocol that enables two computers to communicate.
---

# Connect to Edge Servers with SSH

<figure><img src="../../.gitbook/assets/ssh.png" alt=""><figcaption></figcaption></figure>

## Introduction

Edge Servers are Linux-based virtual machines (VMs) that run on top of decentralised & virtualised hardware. Each Edge Server you create is a new server that you can use, either standalone or as part of a larger, cloud-based infrastructure.

## Tutorial

Edge Servers are managed using a terminal and SSH. You will need to have an SSH client and, optionally, an SSH key pair. Clients generally authenticate either using passwords (which are less secure and generally not recommended) or SSH keys (which are very secure and strongly recommended).

Most users connect to their Edge Servers using SSH and tools like Terminal on OSX or Putty on Windows, however you can also use the Edge Console built in to the account portal.

<details>

<summary>Connect to Your Edge Server Using the Edge Console</summary>

The Edge Account portal has a built in console for connecting to your Edge Server. You can use directly within your web browser.

To access the console, select the `console` tab from within your Edge Server's page in the account portal:

<img src="../../.gitbook/assets/Screenshot 2023-02-26 at 11.58.09.png" alt="" data-size="original">

Next, click on the `Launch Console` button. This will open the console within the account portal:

<img src="../../.gitbook/assets/Screenshot 2023-02-26 at 11.58.17.png" alt="" data-size="original">

You can now proceed to access your Edge Server using the default username and the password that was set at the point of Edge Server creation.

</details>

### Connect to Your Edge Server Using SSH

To log in to your Edge Server with SSH you will need three pieces of information:

1. The server's public IP address
2. The default username on the server
3. The default password for that username, if you haven't already installed SSH keys

To get your Edge Server's **public IP address**, visit the Edge Account Portal. The IP address is displayed in the Edge Server's page within the account portal and will become visible after the Edge Server has finished being deployed. You can hit the copy icon next to the IP address to copy it to your clipboard.

<figure><img src="../../.gitbook/assets/Screenshot-2023-02-25-at-23.45.18.png" alt=""><figcaption></figcaption></figure>

The default username is `root` on most operating systems supported by Edge Server, including Ubuntu, Debian, CentOS and AlamaLinux.

Once you have your Edge Server's IP address, username, and password, follow the instructions for your SSH client. OpenSSH is included on Linux, macOS, and the Windows Subsystem for Linux. Windows users with Bash also have access to OpenSSH. Windows users without Bash can use [PuTTY](https://www.putty.org).
