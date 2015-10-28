---
layout: post
title: "Set up a VM"
date: 2015-02-11 09:21:00
category: hidden
---
# Setting up a VM

Three important things, 

* Virtual Box
* Vagrant
* Homestead

## Virtual Box

First you'll need Virtual Box, a visuaistion provider. 

Download from [here](https://www.virtualbox.org/wiki/Downloads), Look for Virtual Box X.X.XX for OS X Hosts. Once it is downloaded, follow the GUI to install it.

Easy!

## Vagrant

Vagrant helps you build and manage development environments really quickly, everything is automatic and allows you to create identical environemnts over and over again on any computer.

Download from [here](https://www.vagrantup.com/downloads.html). Once downloaded follow the GUI to install.

---

Now we have the easy important tools installed we can start setting up an environment.

There loads of diferent ways to go from here, you could install a plain image of Ubuntu and set it up to install the specific packages you want, but we just want a pretty generic PHP environment.

Vagrant refers to VMs as Boxes, we want to create a box for our PHP dev.

That's where homestead comes in, built by the same guy who made [Laravel](http://laravel.com/) its a premade vagrant box perfect for all things PHP/Laravel.

## Homestead

Jump into terminal.

Since installing Vagrant, we now have access to the `vagrant` command line tool. We can add Homestead box by running the following command.

```bash
vagrant box add laravel/homestead
```

This is going to download the homestead box (ubuntu and the packages), so its big and might take a little while. You only have to do this once, even if you have 20 VMs. Vagrant will store this box so you can quickly provision a new box. 

---

Now it is time to set up a VM and start using it. You will have to do the following for every development environment you create. 

But if you're just going to be building simple applications you can use the same environment for them all.

Find a safe place on your machine and navigate to it in Terminal (I use `~/Developer/Virtual`).

```bash
cd ~/Developer/Virtual
git clone https://github.com/laravel/homestead.git Homestead
```

This will pull down the homestead tools. Open Homestead and run the initializing script.

```bash
cd Homestead
bash init.sh
```

---

## You might have this bit

If you have ever used SSH you might have done this, otherwise, do it. Generate an SSH key. This is so you can connect to your VM.

```bash
ssh-keygen -t rsa -C "you@email"
```

You can hit enter a few times to use the default settings.

---

## Back to Homestead

Now we need to configure the Virtual Machine. Set up our sites, domains and folders.

The file we want to edit is `~/.homestead/Homestead.yaml` Open `~/.homestead` in Finder and edit the file in Sublime or..

```bash
nano ~/.homestead/Homestead.yaml
```

#### Folders

```yaml
folders:
    - map: ~/Code
      to: /home/vagrant/Code
```

The first line maps a local folder `~/Code` to a folder on the VM `/home/vagrant/Code` Adding multiple folders could look like this. Be careful with your indenting.

```yaml
folders:
    - map: ~/Developer/MyApplication
      to: /home/vagrant/MyApplication
    - map: ~/Developer/WebsiteOneTwoThree
      to: /home/vagrant/WebsiteOneTwoThree
    - map: ~/Developer/ClientApp
      to: /home/vagrant/ClientApp
```

Now these folders will sync. If you edit something in `~Developer/ClientApp` it will update in the VM `~/home/vagrant/ClientApp` and vice versa.

#### Sites

Now we need away to access these folders.

```yaml
sites:
    - map: homestead.app
      to: /home/vagrant/Code/Laravel/public
```

The first line maps a domain `homestead.app` to a directory on the VM `/home/vagrant/Code/Laravel/public`. The same folders we set up before could be sites like this.

```yaml
sites:
    - map: myapp.local
      to: /home/vagrant/MyApplication
    - map: website123.dev
      to: /home/vagrant/WebsiteOneTwoThree
    - map: client.app
      to: /home/vagrant/ClientApp/public
```

Be careful setting the VM directory if your application doesn't run in the document root.

To make these domains work, we need to tell your computer to look for a server on the VM.

Open up your `/etc/hosts` file.

```bash
sudo nano /etc/hosts
```

And add each domain, pointed to the VM.

```bash
192.168.10.10 		myapp.local, website123.dev, client.app
```

## Woo!

Now it's time to launch the box.

Navigate back to where we clone the git repo. And tell vagrant to start the VM.

```bash
cd ~/Developer/Virtual/Homestead
vagrant up
```

The first time you run this, it'll take a little time as it sets up all the folders and domains. You'll have to re run this whenever you restart your computer.
