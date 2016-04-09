# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "dummy"

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = ENV['AWS_KEY']
    aws.secret_access_key = ENV['AWS_SECRET']
    aws.keypair_name = ENV['SSH_KEY_NAME']
    override.ssh.private_key_path = ENV['SSH_KEY_FILE']

	# Ubuntu 15.04 in N. Virginia
    aws.region = "us-east-1"
    aws.ami = "ami-f50e209f"

    # K520 - 8 processors
    aws.instance_type = 'g2.2xlarge'
    #aws.instance_type = 't2.micro'

    override.ssh.username = "ubuntu"
  end

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
