# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.hostname = "xdp-playground"
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.box = "fedora/25-cloud-base"
  config.vm.synced_folder ".", "/srv/app", type: "rsync", rsync__exclude: "package.box"
  config.vm.provision "shell", inline: <<-SHELL
     dnf update -y
     dnf install -y bcc bcc-tools bcc-doc --enablerepo=updates-testing
     dnf install -y make tmux wget unzip openssl openssl-devel
     dnf install -y llvm llvm-libs llvm-doc clang clang-libs
     dnf install -y kernel-devel elfutils-libelf-devel vim bc
     dnf install -y python3-pyroute2 make npm libcap-devel git
     make -C /srv/app tester
     make -C /srv/app systemd
  SHELL
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 4
  end
end
