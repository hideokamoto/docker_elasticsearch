VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = "guest"
  config.vm.box = "opscode-centos-6.5"
  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_centos-6.5_chef-provisionerless.box"

  config.vm.network "private_network", ip: "192.168.33.20"

  config.vm.provision "shell", inline: <<-SHELL
    sudo rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-6
    sudo yum -y install http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
    sudo yum -y install docker-io
	sudo service docker start
	export DOCKER_HOST=unix:///var/run/docker.sock
	docker run -d -p 9200:9200 -p 9300:9200 -v "$PWD/esdata":/usr/share/elasticsearch/data elasticsearch
  SHELL

end
