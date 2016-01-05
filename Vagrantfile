# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "gsfjohnson/centos71"

  config.vm.define "reaction-dev" do |v|
    v.vm.network "forwarded_port", guest: 3000, host: 3000
    v.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
    v.vm.hostname = "reaction-dev"
    v.vm.provision "shell", inline: <<-SHELL
      echo
      echo Use \\\'vagrant ssh\\\' to enter client environment and run:
      echo ansible-playbook -i inventory playbook.yml
    SHELL

  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo yum -y install npm git GraphicsMagick patch
    curl https://install.meteor.com > install-meteor.sh
    git clone https://github.com/reactioncommerce/reaction.git
    chmod a+x install-meteor.sh
    chown -R vagrant:vagrant install-meteor.sh reaction
    ./install-meteor.sh >install-meteor.log
    cd reaction && git checkout master
    patch -p1 </vagrant/reaction.patch

  SHELL
end


