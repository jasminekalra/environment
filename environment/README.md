
# Constructing your Test/Development Environment

## Contents 

* [Introduction](#introduction)
* [What is in This Repository](#what-is-in-this-repository)
* [Easy Mode Install](#easy-mode-install)
* [Git](#git)
* [Submitting Code Outside the VM](#submitting-code-outside-the-vm)
* [Testing](#testing) 
* [Debugging](#debugging) 

## Introduction

Note that this course does not provide you with a test framework for your code development; we expect you to develop your _own_ tests; this work can (and should) be done cooperatively.

Your code will be graded by a an automated framework provided to us by Udacity called **Bonnie**.  Bonnie runs in an **Ubuntu Linux 18.04 environment** and we will provide you with some **binaries** that are complied for Linux 18.04. We can't guarantee these binaries will run on anything outside of the Ubuntu 18.04 environment, which means 18.10, 19.04, et. al. will most likely not work. 

Since we aren't running the grader within your environment, we actually do not dictate that you do your own development in one specific way.  This is consistent with systems development, where you are encouraged to work in whatever manner is productive _for you_. 

**For those of you who don't have a preferred environment, please scroll down to the ["Easy Mode Install"](#easy-mode-install) section below.**  This will provide you with a configuration that is functional; it is _not_ the only viable configuration.

You build your own tests and code in your own environment.  You may submit it to Bonnie for grading; because Bonnie is not a test harness (and we discourage you from using it as such), we restrict the number of times that you can submit to Bonnie.

Bonnie does provide some feedback regarding failing tests.  Note:

1. We attempt to provide useful feedback, but there are far more ways to do things wrong, than to do it right (though there are multiple ways to do it right!)  If you don't understand the feedback, ask on Piazza (in a **public** thread).

2. We are allowed to return around 10KB of log output **for all tests combined**, so we must limit the log output **up to that limit** and then truncate the log beyond that.  If you see a failed test, but no feedback, fix one of the failing tests **with** feedback.  Once a test **passes** we won't return its feedback to you.  This permits us to send feedback on other failing tests.

3.  Bonnie isn't a test harness.  You should build your own tests; we strongly encourage you to build scripts or other automated tests.  We encourage you to share your tests (so long as they do not give away the _solution_ to the project).

One of your first challenges in this class is to construct your development and test environment. You have latitude on how you do this.  We note that for some this can be a challenge, while others in the class will delight in their ability to use an environment with which they are comfortable.  In the past we have tried other approaches: thus far, this one has worked the best.

## What is in this Repository

This repository contains three files (in addition to this **README**) for your reference:

* **Vagrantfile** -- use this if you wish to provision with **Vagrant and VirtualBox**.
* **Dockerfile** -- use this if you wish to construct your own Docker image (you do not _have_ to build your own.)
* **requirements.txt** -- this can be used with `pip` to ensure you have installed the required packages.

## Constructing Your Development Environment

There are many ways to construct your development environment.  Here are some that students have found successful. 

* If you are already running on Ubuntu 18.04, then you can simply ensure the necessary packages are installed.
* If you are running on a different Linux version, Mac OS X or UNIX variant, you should be able to figure out how to install the necessary packages. Please understand, we'll answer questions if we can, but you are responsible for your development environment - we're not experts on every possible configuration (e.g., "Why doesn't this package work on my Raspberry Pi running Kali Linux?" - we're not going to know. Maybe someone else in the class does.)
* If you are running on Windows 10 (1703) or newer, you may find that you can install an Ubuntu environment. However, that is **NOT compatible** with the default settings in the project makefile. You can work around these issues, but you are working outside the supported environment. Also note that Visual Studio now has a "build on Linux" option; you may find that easier to use.
* You may construct a virtual machine image. This could include:

    * Hyper-V on Windows (Hyper-V does not play well with other hypervisors. You can get it to do so, but it's a much more complex configuration.)
    * Virtual Box on Windows, Mac OS or Linux
    * KVM on Linux
    * ESXi. If you don't know what this is and don't recognize the term "bare metal hypervisor" then you probably don't want this particular option.
    * Xen. Again, this is a bare-metal hypervisor so if you don't know what that means, don't pursue this option.
    * VMWare Workstation. Note that this is a paid product but as a Georgia Tech student you get a free license. Start here: http://onthehub.com/download/software-discounts/vmware and enter information about Georgia Tech. For campus pick "Atlanta Main Campus" and then choose "College of Computing" - if you pick CoC from the first dropdown it tells you there is no store (which isn't true). If you take CS-6750 you'll learn all about these HCI failures and how to avoid them...  GT does not make the student roster data available to On The Hub until AFTER the registration period closes.  You can use a 30 day evaluation version in the interim.  Also note that Vagrant requires a separate plugin license to use Vagrant with VMWare (US$72 after student discount.)  If you install the plugin on Linux and don't have a license, you won't be able to use any provider (so don't go down this path unless you get the license.) **Bottom line: if you want to use Vagrant, you probably don't want to use VMWare.**
    
    * Parallels.  Virtualization server for MacOS X.  Once again, a free license is available via Georgia Tech (see link under VMWare).
    * You may use Vagrant to construct your environment.  See [Easy Mode Install](#easy-mode-install) for details. Note: the Vagrantfile
      includes the ability to use the **hyperv** provider (on Windows 10/Server 2016+).  This is new, so please understand that this
      _may not work_.  We have not enabled the SMB sharing yet - if you get it to work, please let us know.
    * You may use a cloud environment

        Google will give you up to $300 in free time when you first sign up.
        AWS can provide you with EC2 instances for a nominal fee (cheaper than buying a new computer).
        Georgia Tech has virtual machine resources that you can use, though nobody in class has reported doing this so far: https://support.cc.gatech.edu/services/instructional-computing.
        Microsoft Azure credits are available as part of the On the Hub software offerings from GT's CoC web store and it is certainly enough to run a virtual machine ($100 over the course of the year).
    * You may use the Ubuntu 18.04 environment on Windows 10 (1703 and more recent). Note that address sanitizer is not supported in this environment (or at least it wasn't in 16.04). This is a serious limitation for those students who are not familiar with C because address sanitizer checks for and reports memory handling issues. But this is an option. https://www.microsoft.com/en-us/p/ubuntu-1804-lts/9n9tngvndl3q
    * You may use the Docker container (on https://hub.docker.com as fsgeek/omscs6200) or build your own Docker image (the Dockerfile we use is included
      in this repository).
    
    **This list is not exhaustive**. There are other, more exotic ways that you could build a working development environment. Feel free to experiment - and let us know how it goes so we can tell future students what works and what to avoid.

If you have an existing Ubuntu 18.04 base, you can install the requisite software (using sudo apt-get install). You will also need to add the PPA we provide for use in Project 4:  
 
 ```bash
 # Add the course PPA
 wget -O - https://ppa.bitanical.com/pward8@gatech.edu.gpg.key | sudo apt-key add -
 echo "deb https://ppa.bitanical.com/apt/debian bionic main" | sudo tee -a /etc/apt/sources.list.d/ppa.bitanical.list

 # Update the repos
 sudo apt-get update

 # Install requirements
 sudo apt-get install build-essential git pkg-config zip unzip software-properties-common python-pip python-dev libgmp-dev gcc-multilib valgrind openmpi-bin openmpi-doc libopenmpi-dev portmap rpcbind libcurl4-openssl-dev bzip2 imagemagick libmagickcore-dev libssl-dev libffi6 libffi-dev llvm grpc-cs6200 protobuf-cs6200
```    

Finally, install the relevant python packages:

    pip install --upgrade future cryptography pyopenssl ndg-httpsclient pyasn1 nelson

You may need to do this as root (or via elevation using sudo) depending upon your environment. (the --upgrade on that line ensures you have a version of cryptography that works with pyopenssl.  Without that, you will get warnings).  Note: it's not good practice to forcibly upgrade (for example, I'm using Anaconda and I don't need to use sudo.)

Note: there are known issues with some versions of imagemagick having a memory leak that may manifest in your environment. Bonnie uses a version without this leak. You won't need to use imagemagick until Project 4. (Fair warning: we are making changes to Project 4 so this might change.)

But in the end, **the grading environment will be the docker container, based upon Ubuntu 18.04 configured with the packages that I've listed**. We have found that this environment definitely seems to stress student code in ways that cause it to break. We suspect some of this is because it's running on a large MP machine with plenty of resources and different behavior. Of course, the usual practice is to blame Bonnie for bugs in your code ("it works on my machine"). One of the challenges of being a systems developer is learning how to replicate the problems users of your code see. Try building some tests. Feel free to share them with other students.

Bottom line: work in an environment that is comfortable for you. If you want to build and test all of your code in a different environment more comfortable to you, please feel free to do so. When you submit your code to the grader, it will run it, test it, and provide you with feedback. You own your environment. We own the test environment. We don't care that it works in your environment, we care that it works in our environment.

Also, feel free to share a description of your environment on Piazza so other people can learn from your own experiences.

## Easy Mode Install

_For some value of easy..._

The simplest way to construct your environment is to use Vagrant.  Just a few steps and you should have a working virtual machine image with all the necessary parts:

1. Assuming you don't have Vagrant installed already, download the latest [Vagrant binary](https://www.vagrantup.com/downloads.html) for your native platform. You may also need to download [Virtual Box](https://www.virtualbox.org/wiki/Downloads). For more details, please see the guides below (HT: Isabel Lupiani and Charles McGuinness from Computational Photography).

    * [Windows](https://docs.google.com/document/d/1FxuHsekpU5ng1ZxULZjpHg6u145fz8cie6kgH86y2uI/edit?usp=sharing)
    * [Mac OSX](https://docs.google.com/document/d/13IZnOzZtC5ZVmSy162fkpb44M3xsbhlIzjTAbfqDjjo/edit)

2. Copy the **Vagrantfile** from this repository to the top-level directory that you plan to use for the course.  For example:

    * CS6200/
        * Vagrantfile
        * pr1/
        * pr2/
        * pr3/
        * pr4/

From any directory in which the `Vagrantfile` is present, you can start your virtual machine with just the command `vagrant up` and connect to it with just `vagrant ssh`.  Note that by default the vagrant machine will share the folder containing the Vagrantfile at `/vagrant`. Therefore, your first command after logging into the vagrant machine will almost always be `cd /vagrant`.  See the [Vagrant documentation](https://www.vagrantup.com/docs/getting-started/) for more details.

Most students have found this works well; however, sometimes something goes wrong and the error isn't reported back in which case you end up with an environment that doesn't quite work right. If that happens, you should destroy the Vagrant image and recreate it - usually that does the trick.  Just remember, anything _inside_ the virtual machine will be lost, so make sure you save anything important first!
        
Vagrant is probably the least resource intensive environment - the image it gives you with our default configuration file has no GUI (use ssh to access it - easiest way to do this is vagrant ssh in the same directory as the Vagrantfile after you start it with vagrant up).
        
You can share files between Vagrant (Virtual Box) and your host machine using NFS, SMB or built-in guest sharing. Windows, MacOS, Linux and UNIX all have an NFS client available.
        
You can install a windowing environment inside the guest machine. For example, I have installed the X Windows pieces in the guest and an X server on the host (I use MobaXterm on Windows). You can configure sshd to forward X as well. Then you can open xterm windows, run CLion inside the VM while it displays on your host monitor, etc.

Feel free to change the Vagrantfile to change the options if you'd like (e.g., if you don't want a gui window to show up.)
Login for the bento/ubuntu-18.04 environment is user vagrant password vagrant.

Use vagrant help to get a list of command.  Google is also your friend - this is a commonly used deployment tool.

## Git

This and all assignments will be made available on the [https://github.gatech.edu](https://github.gatech.edu) server.  To access the code and import any updates, you will want to [install git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).  Git on Windows is a little different, so you may want to consult this [guide for Windows](https://docs.google.com/document/d/1_geDGrI0JlHHtnJY0P5pe6yU3E19NLEejdAOyDloqdQ/edit?usp=sharing) (HT: Isabel Lupiani).

Change to the directory you plan to use for the course.  Then clone this repository with the command

```console
$ git clone https://github.gatech.edu/gios-spr-20/pr1.git
...
```

(If this command fails with a complaint about "server certificate verification failed", then you might need to run

```console
$ GIT_SSL_NO_VERIFY=true git clone --recursive https://github.gatech.edu/gios-spr-20/pr1.git
...
$ cd pr1
$ git config http.sslVerify false
```

instead. Note we don't really recommend using git without SSL, but some people have had issues with misconfiguration in the past and this is a work around, albeit one that 
pretends security is not an issue.)

**Note: the repositories won't be available until the project is released.  The first project is normally released shortly after the registration period ends.**

## Submitting Code Outside the VM

Some students prefer to develop mostly on their native environment and only use the Vagrant VM for testing.  In this setup, it is also convenient to be able to submit code from the native environment.  To do this you will need to install

* [python 2.7](https://www.python.org/downloads/)
* [python's requests library](http://docs.python-requests.org/en/master/user/install/)
* [python's future library](http://python-future.org/quickstart.html)

** Note that these steps are optional.  The VM has everything you need already **

All are very standard tools and should be easy to install by following the directions at the links above.  There is also a [guide for Windows](https://docs.google.com/document/d/1nvHUqwo2wXR6CAJYzDkVxwWxdvT8I2fodBZrn88d6E0/edit#) (HT: Isabel Lupiani).  If you have any problems, please ask for assistance on Piazza.

The scripts should be Python 3 compatible as well.


## Testing

We do not provide you with a test harness.  We **strongly** recommend that you build such an environment, as doing so will make your experience in the course much more pleasant.

* You can construct your test environment using standard Ubuntu Linux tools, such as `netcat`.
* You can use unit test frameworks (there are several)
* You can code tests in other languages (e.g., Python) -- you may find it easier to implement the projects in your favorite language, which can form the basis of good tools.

**Bonnie** (the grader platform) is not a test harness.

## Debugging

You will have bugs in your code.  You should use the tools available for debugging.  These include:

* gdb -- there's a bit of a learning curve with gdb, but knowing how to use a debugger is a useful skill.  Use it
* valgrind -- the code that we provide to you will generally be set up to use _AddressSanitizer_ which is a Google developed library for making sure your code is properly using memory (including stack space, dynamically allocated memory ("heap"), etc.)  Valgrind is another tool for doing a similar job.  **Valgrind and AddressSanitizer do not work together.**  To use valgrind you must use non-address sanitizer versions of your code.
* strace -- this will show you _what your code is doing_.
* hexdump -- you will be transferring binary files; showing them in a hex representation can be useful

**This list is not exhaustive**

# Pull Requests

If you wish to contribute towards this document, please feel free to do so. 

**We will accept pull requests (PRs) for this repository**  (note that we will _not_ accept them from the project repositories).

