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
  
  config.vm.provision 'docker', type: 'shell', inline: <<-SHELL
    set -eu -o pipefail
    DOCKER_VERSION=18.03
    if [[ -z "$DOCKER_VERSION" ]]; then
      echo 'DOCKER_VERSION is not set.'
      exit 1
    fi
    export DEBIAN_FRONTEND=noninteractive
    apt-get update
    apt-get install -y apt-transport-https ca-certificates curl software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
    apt-key fingerprint 0EBFCD88
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    apt-get update
    apt-get install -y "docker-ce=${DOCKER_VERSION}.*"
    docker info
    usermod -aG docker vagrant
  SHELL
  
end