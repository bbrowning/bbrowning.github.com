---
title: Developing Rails Apps with TorqueBox and Vagrant

layout: post
---

The [TorqueBox][] project does a great job of bringing together the best parts of Ruby, Rails, JBoss, and the JVM. However, I've recently started using [Vagrant][] for all my development work and couldn't find anyone that had used the two together. So, after hacking around a bit, I've created a Vagrant box anyone can use to easily get up and running with TorqueBox.

[torquebox]: http://torquebox.org/
[vagrant]: http://vagrantup.com

*The rest of this post assumes a basic level of familiarity with TorqueBox and Vagrant - things will make more sense if you browse some of their documention before reading further.*

### What's Included in the Box
* Ubuntu 8.04
* OpenJDK 1.6.0_0-b11
* TorqueBox 1.0.0.Beta19

Because it contains a full TorqueBox binary and a Java runtime, the box is 1.2GB in size.


### Creating Your First Project

* [Install Vagrant][install_vagrant] if you haven't already

[install_vagrant]: http://vagrantup.com/docs/getting-started/index.html

* Add the TorqueBox Box to Vagrant

    **Preferred Method - Bittorrent**

    Use your favorite Bittorrent client to download <http://bbrowning-boxes.s3.amazonaws.com/torquebox.box?torrent> and then run

        $ vagrant box add torquebox path_to_downloaded_file/torquebox.box 

    **Alternate Method - Direct Download**

    The direct download will be faster (but cost me more money) unless several nice people help me seed the torrent.

        $ vagrant box add torquebox http://bbrowning-boxes.s3.amazonaws.com/torquebox.box

* Create and initialize a sample application

        $ mkdir sample_app
        $ cd sample_app
        $ vagrant init torquebox

* Run the box

        $ vagrant up

    This step may take a few minutes.

* Create a Rails project

    To simplify things, all rails/rake commands should be run from inside the TorqueBox VM.

    Log into the VM and cd to the shared vagrant folder.

        $ vagrant ssh
        $ cd /vagrant

    Follow the steps from the [TorqueBox Rails documentation][torquebox_rails_docs] for creating our Rails application with the TorqueBox template:

    [torquebox_rails_docs]: http://torquebox.org/documentation/1.0.0.Beta19/web.html#rails-support

        $ rails -m $TORQUEBOX_HOME/share/rails/template.rb .

    If you look on your host machine, you'll see the Rails application files were created in your sample_app directory. The /vagrant directory inside your VM is a bidirectional shared-folder with the sample_app directory on your host.

    After creating a new project, you'll need to redeploy your Rails app into TorqueBox. You only have to do this once - the VM will automatically pick up on the project the next time it's started.

        $ rake torquebox:rails:deploy

    Wait 15-30 seconds and point your browser to <http://localhost:3000>. You should see the familiar Rails "Welcome aboard" page.

**Congratulations, you're now running a Rails application inside TorqueBox.**

### Next Steps

If you've made it this far, you've done the hard part. Use your favorite editor on your host machine to develop your Rails application like you always have. The only thing to remember is to run `script/generate`, `rake db:migrate`, etc from inside the Vagrant VM. If you try to run these on the host you most likely won't have the right version of Rails or JRuby installed.

Changes made to your Rails project should be visible on the next page refresh just like regular Rails development. To try this, generate a simple Posts scaffold.

    $ ./script/generate scaffold post title:string body:text
    $ rake db:migrate

Point your browser to <http://localhost:3000/posts> and your should see the scaffolded post index.

When you've finished working on this project or need to switch to another one, issue a `vagrant halt` or `vagrant destroy` from the sample_app directory on your host. The next time you need to work on this project again, issue a `vagrant up` to boot everything back up. See the Vagrant docs for more details on these commands.

Let's try it.

If you're still logged into the VM via ssh, log out.

    $ exit

Destroy the VM

    $ vagrant destroy

Now re-create the VM and start it back up (will take several minutes)

    $ vagrant up

Wait 15-30 seconds for TorqueBox to start up and then point your browser to <http://localhost:3000/posts> - your app is back right where we left off.


If you have any feedback, requests, or problems with the TorqueBox box, contact me on Twitter (@bbrowning). Enjoy!