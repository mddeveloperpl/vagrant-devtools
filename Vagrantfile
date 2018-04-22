Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/artful64"
  
  config.vm.provision "shell", inline: <<-SHELL
	  sudo apt-get install -y software-properties-common python-software-properties
	  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
	  sudo add-apt-repository ppa:webupd8team/java -y
	  sudo apt-get update
	  sudo apt-get install oracle-java8-installer
	  echo "Setting environment variables for Java 8.."
	  sudo apt-get install -y oracle-java8-set-default
  SHELL
  
# requires vagrant plugin .. command: vagrant plugin install vagrant-docker-compose
  config.vm.provision :docker
  config.vm.provision :docker_compose
  
end