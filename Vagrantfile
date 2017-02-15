# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
VAGRANTFILE_API_VERSION = "2" # Vagrantfile API/syntax version. Don't touch unless you know what you're doing!

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  # Handle local proxy settings
  if Vagrant.has_plugin?("vagrant-proxyconf")
    if ENV["http_proxy"]
      config.proxy.http = ENV["http_proxy"]
    end
    if ENV["https_proxy"]
      config.proxy.https = ENV["https_proxy"]
    end
    if ENV["no_proxy"]
      config.proxy.no_proxy = ENV["no_proxy"]
    end
  end

  config.vm.synced_folder "~/", "/vagrant_home"

  # One vm running all the services
  config.vm.define "mbed-dev" do |config|
    config.vm.hostname = 'mbed-dev'
    config.vm.box = "ubuntu/xenial64"
    config.vm.network :private_network, ip: "192.168.10.5"
    config.ssh.insert_key = true
    config.ssh.forward_agent = true
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
    end
    # Python is not installed on 16.04+ ubuntu/xenial64 by default and
    # Ansible won't run without it.
    config.vm.provision "shell",
    inline: "sudo apt-get install python -y",
    keep_color: true
    # Run the Ansible playbooks
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.raw_arguments = ['-T 30', '-e pipelining=True']
    end
  end
end
