##Materials for MABUG 2014 Presentation

###Title: Automated Build and Deployment of Tomcat Apps, ~~or, How Ops can get out of the way of development~~

* Chris Peck
* College of William and Mary
* Date: 9/29/2014
* Session ID: 8743



Last Fall, the IT Unix "Ops" team at William and Mary implemented a new tool named Jenkins for managing software projects.  Eventually, we were able to to talk some Developers into using this tool for the development of their Grails Apps.  I’ll briefly discuss what Jenkins is and how to get it (it’s free as in beer), as well as what the IT Unix Team uses it for, then I’ll take a deep-dive into using it for developing and deploying Apps to Tomcat Servers.

As I began developing our team was informed that Banner XE would be deployed to Linux servers (which is what our team “does”).  I had attend MABUG last Fall to learn more about what XE was, the development strategy and had read how Ellucian appeared to be using technologies similar to what we had focused on using as we began to rollout our “next-generation” of servers & services in *nixland*. I was intrigued to say the least.  I had a talk over some beers at the pig roast with Ed Hauser & a “tech” person from Ellucian, and, we seemed in sync conceptually on this. We are planning on using the same processes described here to deploy Banner XE Apps as they become available.

In the pre-Jenkins world, Grails warfiles were built on the developers desktop, then copied to a network "drive". They would then contact the Ops team who would copy it from the network drive to the Tomcat server, put it in place and restart the service. This led to a lot of pain points, what version of grails and java was being used, etc. The age-old "Well, it worked on my Desktop" statement was rather common. Since so much of this was manual, this process was fragile, with many points of possible failure. Since Developers depended on Ops for deployment it was a very slow process

In the post-Jenkins world, well, Jenkins does it all for us, with some help from some other tools.  When code is committed to our local source code repository, Jenkins will automatically build the War files (in the same environment as the Tomcat servers).  If Jenkins can build the App successfully, the following occurs:
For the Development Environment the WAR file is automatically deployed to the Tomcat server. 
For the Production Environment, since Ops are the only ones allowed to deploy to PROD, then someone from Ops tells Jenkins to deploy the App. 
Since the process is automated, the chance of failure is minimized. Developers are happy, and, Ops are ecstatic.

This presentation will describe the journey to a faster, less-painful deployment process for Grails (or any other) Apps to a Tomcat server.  I will describe the processes in place before, how we got to where we are, and the tools we used to implement the current environment.

During the creation of this presentation, I created a "Vagrantfile" for demonstrating how this is done. This Vagrantfile will spin up an Ubuntu 14.04 server VM running Tomcat and Jenkins. It also installs a simple source tree using git to use as an example. This git source tree contains a post-commit hook into Jenkins to kick off the building of a warfile based on it, and, then auto-reploying it to the Tomcat server.

If you would like to use this Vagrantfile to play with, head on over to https://github.com/crpeck/vagrant-mabug and *git* it.

