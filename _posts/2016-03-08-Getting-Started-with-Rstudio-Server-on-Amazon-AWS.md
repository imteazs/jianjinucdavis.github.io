---
layout: post
title: Getting Started with Rstudio Server on Amazon AWS
modified: 2016-03-08
comments: true
share: true
tags: [AWS, cloud]
---

Working with Amazon AWS is amazingly easy to get started. Titus Brown had a wonderful workshop yesterday. He walked us through setting up Rstudio server using EC2 instances.  [The tutorial](http://dib-training.readthedocs.org/en/pub/2016-03-03-aws-br.html) and the [Youtube video](http://dib-training.readthedocs.org/en/pub/2016-03-03-aws-br.html) are perfect to get you started on using Amazon. 

This article is mostly a short version of the tutorial Titus put together. It serves as a quick guide and will mostly likely be useful for those who had go through a step-by-step guide once. 

## Launch an Amazon instance
The first step is launching an Amazon instance from an ubuntu AMI (ami-05384865), and setting up instance firewall by adding a custom TCP rule of port range 8000-9000. Waiting for your instances to be running and status checks passed.

## log in your remote machine and setup your remote machine

Logging in your remote machine using your keypair. If this is the first time you use your keypair, you'll need to set permissions.

~~~
chmod og-rwx ~/Downloads/amazon-key.pem
~~~
Connect to your remote machine from ssh:

~~~
ssh -i ~/Downloads/amazon-key.pem -l ubuntu MACHINE_NAE
~~~

set your password

~~~
sudo passwd ubuntu
~~~

Install R and gdebi tool

~~~
sudo apt-get update && sudo apt-get -y install gdebi-core r-base
~~~

Download and Install Rstudio Server

~~~
wget https://download2.rstudio.org/rstudio-server-0.99.891-amd64.deb
sudo gdebi -n rstudio-server-0.99.891-amd64.deb
~~~

If installations are successful, you'll see:

~~~
Mar 08 16:30:40 ip-172-31-16-57 systemd[1]: Starting RStudio Server...
Mar 08 16:30:40 ip-172-31-16-57 systemd[1]: Started RStudio Server.
~~~

## Open RStudio Server

Go to your browser, type in your hostname + ":8787", eg.

~~~
http://ec2-54-193-110-53.us-west-1.compute.amazonaws.com:8787
~~~

There you go! Hope you see the familiar RStudio windows and feel at home again. 

The username is 'ubuntu' and the password is the password you just set.

## Transfer data

Now that you're ready for analysis, to transfer data to your remote machine:

~~~
scp -i ~/Downloads/amazon-key.pem ~/Desktop/file.txt ubuntu@ec2-54-193-110-53.us-west-1.compute.amazonaws.com:~/
~~~

~~~
scp -i ~/Downloads/amazon-key.pem ubuntu@ec2-54-193-110-53.us-west-1.compute.amazonaws.com:~/results.pdf ~/Download/
~~~

Enjoy!

