# Goal or Idea

This vagrant environment will bring up an image of the environment that was created from the opg-backoffice-deploy salt scripts. The main difference is the developer workflow.

1. Developers run vagrant up and vagrant halt. There is no need to run vagrant provision.
   (Whilst this goes against the central idea behind vagrant our environment currently is not a moving target)
2. When files are pushed into the vm the vendor folder is also synced. This means developers need to run composer in the repos on there host machine e.g php composer.phar install

---

## Installation instructions

1. Download Vagrant 1.5.4, Virtualbox 4.3.12
2. Create a directory structure that looks as follows
   /opg-backoffice-image
   /opg-core-back-end
   /opg-core-auth-membrane
   /opg-core-ingestion
   /opg-core-behat
   /opg-core-front-end

2. cd opg-backoffice-image.
   vagrant plugin install vagrant-gatling-rsync
   vagrant plugin install vagrant-vbguest

3. get the box file which is an image of the environment and run
   vagrant box add opgbackofficeimage opgbackofficeimage.box

4. vagrant up.

5. Run rsync

6. Make sure you configs are set correctly for each tier (i.e. F/E points to `membrane.localz)
