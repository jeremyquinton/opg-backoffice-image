Vagrant.configure(2) do |config|
  
  if Vagrant.has_plugin?("vagrant-gatling-rsync")
    config.gatling.latency = 0.2
  end
  
  config.cache.scope = :box

  config.cache.synced_folder_opts = {
    type: :nfs,
    mount_options: ['rw', 'vers=3', 'tcp', 'nolock']
  }

  config.vm.box = "opgbackofficeimage"

  config.vm.network :private_network, ip: "192.168.33.10"

  config.vm.provider "virtualbox" do |vb, override|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
    unless Vagrant.has_plugin?("vagrant-vbguest")
      puts 'The vagrant-vbguest plugin is not installed! This plugin ensures that VirtualBox Guest Additions are up to date.  Install with `vagrant plugin install vagrant-vbguest`'
    end
  end

  config.vm.provider "vmware_fusion" do |vb, override|
    vb.vmx["memsize"] = "2048"
    vb.vmx["numvcpus"] = "2"
  end

  config.vm.provider "vmware_workstation" do |vb, override|
    vb.vmx["memsize"] = "4096"
    vb.vmx["numvcpus"] = "2"
  end

  config.vm.synced_folder "../opg-core-back-end/", "/srv/opg-core-api/application/current", type: "rsync", owner: "opg-core-api", group: "opg-core-api", rsync__exclude: [".git/"], :rsync__args => ["--chmod=ugo=rwX","--verbose", "--archive", "-z"]
  config.vm.synced_folder "../opg-core-auth-membrane/", "/srv/opg-core-membrane/application/current", type: "rsync", owner: "opg-core-membrane", group: "opg-core-membrane", rsync__exclude: [".git/"], :rsync__args => ["--chmod=ugo=rwX","--verbose", "--archive", "-z"]
  config.vm.synced_folder "../opg-core-ingestion/", "/srv/opg-core-ingestion/application/current", type: "rsync", rsync__exclude: [".git/"], :rsync__args => ["--chmod=ugo=rwX","--verbose", "--archive", "-z"]
 config.vm.synced_folder "../opg-core-behat/", "/srv/opg-core-behat/application/current", type: "rsync", rsync__exclude: [".git/"], :rsync__args => ["--chmod=ugo=rwX","--verbose", "--archive", "-z"]
  config.vm.synced_folder "../opg-core-front-end/", "/srv/opg-core-front/application/current", type: "rsync", owner: "opg-core-front", group: "www-data", rsync__exclude: [".git/", "node_modules"], :rsync__args => ["--chmod=ugo=rwX","--verbose", "--archive", "-z"]

  config.vm.network :forwarded_port, guest: 80, guest_ip: "front.local", host: 8081
  config.vm.network :forwarded_port, guest: 80, guest_ip: "api.local", host: 8082
  config.vm.network :forwarded_port, guest: 80, guest_ip: "membrane.local", host: 8083
  config.vm.network :forwarded_port, guest: 9200, host: 9201
  config.vm.network :forwarded_port, guest: 9444, host: 9445
  config.vm.network :forwarded_port, guest: 3306, host: 3307
 
end


