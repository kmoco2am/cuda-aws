# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "dummy"

  # config.vm.box_check_update = false

  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # config.vm.network "private_network", ip: "192.168.33.10"

  # config.vm.network "public_network"

  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = "<xxx>"
    aws.secret_access_key = "<yyy>"
    aws.keypair_name = "cuda-test-east1"

	# Ubuntu 15.04 in N. Virginia
    aws.region = "us-east-1"
    aws.ami = "ami-f50e209f"

    # aws.user_data = "#!/bin/bash\nsed -i -e 's/^Defaults.*requiretty/# Defaults requiretty/g' /etc/sudoers"

    # K520 - 8 processors
    #aws.instance_type = 'g2.2xlarge'
	aws.instance_type = 't2.micro'

    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = "/Users/kmoch/Workspace/keystore/cuda-test-east1.pem"
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update
	 sudo apt-get -y upgrade
	 sudo apt-get install -y linux-image-extra-`uname -r`
	 sudo wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1504/x86_64/cuda-repo-ubuntu1504_7.5-18_amd64.deb
     sudo dpkg -i cuda-repo-ubuntu1504_7.5-18_amd64.deb
	 sudo apt-get update
     sudo apt-get install -y cuda
	 echo -e "\nexport PATH=/usr/local/cuda/bin:$PATH\n\nexport LD_LIBRARY_PATH=/usr/local/cuda/lib64" >>/root/.bashrc
  SHELL
end
