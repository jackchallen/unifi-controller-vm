# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/xenial64"

  config.vm.network "public_network"

  config.vm.network :forwarded_port, host: 8443, guest: 8443

  config.vm.provision "shell", inline: <<-shell
    set -e;

    apt-get update
    apt-get upgrade -y --force-yes
    apt-get install -y aptitude
    apt-get install -y openjdk-8-jre-headless jsvc mongodb-server binutils

    # http://www.ubnt.com/download/unifi/
    cd /home/ubuntu
    #UNIFI_VERSION="4.7.5"
    UNIFI_VERSION="5.4.11"
    UNIFI_FILENAME="unifi_sysvinit_all.deb"
    wget -q https://www.ubnt.com/downloads/unifi/$UNIFI_VERSION/$UNIFI_FILENAME
    dpkg -i $UNIFI_FILENAME

    echo "Unifi Controller v$UNIFI_VERSION is now listening at"
    for i in `hostname --ip-address`
    do
      echo "https://$i:8443"
    done
  shell

end
