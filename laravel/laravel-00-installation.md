# Laravel 00 - Installation #

> **Heads Up:** Laravel is a framework that is built using PHP. Very similar to WordPress, a CMS  PHP framework.

Just as you can make functions in PHP that can do more stuff, Laravel is written in PHP and contains many functions that allow you to do WAY more stuff. You can use it to make web sites, api’s, and applications. It’s the Wizard from the Wizard of Oz, working the small levers and buttons of PHP to make big things happen.

Laravel is built on PHP, and we *could* install PHP (and mysql, and apache, and phpmyadmin, etc) directly on our host computer. But installing programs directly onto our computer does not insure that we will all have the same development environment. Plus, if something goes haywire its a lot harder to clean the slate and start over.

So we use Vagrant. That way we have a uniform virtualized environment that will always work the same for all of us.

In theory this should be an easy thing to accomplish. But, as we’ve seen from running our PHP training and Wordpress boxes, sometimes it can be a journey fraught with disaster as we try to reach virtual machine nirvana.

Getting Laravel up and running on Vagrant is no exception. But thankfully there exists a specialized Vagrant box for Laravel; (say with Dumbledore accent) it is called Homestead, and out-of-the-box it does a great many things.

But it does not include actual Laravel - just the ideal environment FOR Laravel. We'll have to install Laravel once the Homestead box is running, and the easiest way is with *another* powerful tool called Composer. Its a PHP package manager that brings in additional functionality…similar to the Node package manager.

With all the additional software required to run this stuff you can imagine that setting up on different platforms can be a bit of a train wreck. And it usually is.

But once it’s running, it’s great…usually…

## Setup ##

- Vagrant and VirtualBox should already be installed from precious stuff we've done...if not, install them! Make sure you have a solid internet connection for this step (and the next one too where you add the laravel/homestead vagrant box)
  - VirtualBox: https://www.virtualbox.org/
  - Vagrant: https://www.vagrantup.com/
- Add the laravel/homestead box to your vagrant boxes
  - ```$ vagrant box add laravel/homestead```
- While that is downloading lets install the Homestead manager (https://laravel.com/docs/5.8/homestead) called "Homestead"
    - Change to your user folder (cd ~/) and then run "git clone https://github.com/laravel/homestead.git ~/Homestead"
    - CD into the Homestead folder (```$ cd ~/Homestead```)
    - Checkout the release branch (```$ git checkout release```)
- Run the installer (```$ bash init.sh``` or ```init.bat``` on windows)
- Edit the ```Homestead.yaml``` file and make the following changes to it, where necessary:
    - ```provider:``` should be designated as ```virtualbox```
    - ```folders:``` should be:
        - ```map: ~/Projects/laravel``` (assuming you placed your Projects folder into your user folder like you were instructed!!)
        - ```to: /home/vagrant/laravel```
    - ```sites:``` should be…
        - ```map: homestead.test```
        - ```to: /home/vagrant/laravel/public```
    - (reference: https://stackoverflow.com/questions/24506192/vagrant-laravel-homestead-ssh-authentication-failed)
- Create a new folder for our Laravel project called ```laravel``` in our Projects folder
- In the ```/Homestead``` folder ```$ vagrant up```
- Now we need to install Composer to install Laravel…which basically means it downloads a Laravel bootstrap collection of files so that you just type "laravel new" to start a new laravel project. However, Composer wants to live in the environment that your database, server, and php lives in. Some of us probably have PHP installed on our laptops but the configuration is going to be all over the place. So, we’ll need to do the composer stuff inside our Homestead Vagrant box. AAAAAND Our vagrant box already has composer installed! So really, now all we need to do is install the laravel installer.
- SSH into the Vagrant box (```$ vagrant ssh```)
- Install Composer with ```$ composer global require laravel/installer```
- Now cd into the laravel folder, which will be at ```/home/vagrant/laravel```
- Create a new Laravel install in this folder by typing ```$ laravel new```
- The installer will copy the Laravel template files and then download and install what are called dependencies
- Go to your browser and enter ```192.168.10.10``` - BAM! (you should see the Laravel welcome screen)
