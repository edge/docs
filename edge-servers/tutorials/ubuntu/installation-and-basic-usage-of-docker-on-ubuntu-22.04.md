---
description: >-
  This tutorial walks through the installation and a few usage examples of
  Docker on your Ubuntu 22.04 Edge Server.
---

# Installation and Basic Usage of Docker on Ubuntu 22.04

<figure><img src="../../../.gitbook/assets/docker.png" alt=""><figcaption></figcaption></figure>

## Introduction <a href="#introduction" id="introduction"></a>

Docker is an application that simplifies managing application processes in containers. Containers are similar to virtual machines but are more portable, resource-friendly, and dependent on the host operating system. This tutorial will guide you through installing and using Docker Community Edition (CE) on Ubuntu 22.04, working with containers and images, and pushing an image to a Docker Repository.

_Note: This tutorial will probably also work for other versions of ubuntu. It may also work for other linux distributions with slight modifications to the install commands_

### Prerequisites

Before you start, you will need an Ubuntu 22.04 Edge Server with a non-**root** user with `sudo` privileges and a firewall enabled to block non-essential ports.

You can learn how to do this by following our base configuration tutorial for Ubuntu 22.04:

{% content-ref url="base-configuration-for-ubuntu-22.04.md" %}
[base-configuration-for-ubuntu-22.04.md](base-configuration-for-ubuntu-22.04.md)
{% endcontent-ref %}

Once you’re done setting this up, log in as your non-**root** user and proceed to step 1.

## Tutorial

### 1. Installing Docker

