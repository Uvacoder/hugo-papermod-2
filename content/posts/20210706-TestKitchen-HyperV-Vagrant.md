---
draft: true
title: Test kitchen with Hyper-V and Vagrant
description: Setting up Test Kitchen with Hyper-V and vagrant

date: 2021-06-30T20:45:00+01:00
tags: 
    - Test Kitchen
    - Vagrant
    - Hyper-V
categories:
    - development
    - Test Kitchen
    - Hashicorp
---
This post is going to do a quick run through of how to configure test-kitchen on windows, using Hyper-V and Vagrant
## Setup Hyper-V
Setup of Hyper-V is as easy as:
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
``` 
## Install Vagrant
Go ahead and download the installer for [vagrant](https://www.vagrantup.com/downloads)

Run the installer through it's thing and reboot.

## Build a bento box
[Bento](https://github.com/chef/bento) boxes are packer templates, configured with Vagrant in mind. We're going use the [Windows 2019](https://github.com/chef/bento/blob/master/packer_templates/windows/windows-2019.json) image.

CLone the whole repo if you like - or just write out the 2019 packer config somewhere.

We also need to download [packer](https://www.packer.io/)

Then we run the following commands:
```
cd C:\path\to\packer_templates\windows
C:\path\to\packer.exe build -only=hyperv-iso .\windows-2019.json
```
This will then download and configure a hyper-V VM, do some magic, and wrap it up for us as a vagrant `box` file


## Setup Test Kitchen (Chef workstation?)

## Do something cool

