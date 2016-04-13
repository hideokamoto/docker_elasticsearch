VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = "guest"
  config.vm.box = "centos-6.6"
  config.vm.box_url = "https://github.com/tommy-muehle/puppet-vagrant-boxes/releases/download/1.0.0/centos-6.6-x86_64.box"

  config.vm.provision "shell", inline: <<-SHELL
    sudo rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-6
    sudo yum -y install http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
    sudo yum -y install docker-io
	sudo yum -y install jq
	sudo service docker start
	export DOCKER_HOST=unix:///var/run/docker.sock
	sudo docker run -d -p 9200:9200 -p 9300:9200 -v "$PWD/esdata":/usr/share/elasticsearch/data elasticsearch
  SHELL

end
