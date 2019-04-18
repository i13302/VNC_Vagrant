# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url ="https://app.vagrantup.com/ubuntu/boxes/trusty64"
  #config.vm.box_url = "https://app.vagrantup.com/debian"

  config.vm.define "client" do |ct|
    ct.vm.hostname = "vnc"
    #ct.vm.network :public_network, bridge: "eth0"
    ct.vm.network :forwarded_port, id:"ssh",    guest:   22, host:40022
    ct.vm.network :forwarded_port, id:"vnc",    guest: 5901, host:45901
    #ct.gui = true
    #ct.customize ["modifyvm", :id, "--vram", "128"]
    #ct.ssh.username = 'vagrant'
    #ct.ssh.password = 'vagrant'
    #ct.ssh.insert_key = false
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update &&  \
    apt-get upgrade -y &&  \
    apt-get install -y ubuntu-desktop vnc4server gnome-core gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
    mkdir -p /home/vagrant/.vnc 
    echo '#!/bin/bash' > /home/vagrant/.vnc/xstartup
    echo 'unset SESSION_MANAGER' >> /home/vagrant/.vnc/xstartup
    echo 'unset DBUS_SESSION_BUS_ADDRESS' >> /home/vagrant/.vnc/xstartup
    echo 'xrdb $HOME/.Xresources' >> /home/vagrant/.vnc/xstartup
    echo 'xsetrooe -solid grey' >> /home/vagrant/.vnc/xstartup
    echo 'export XKL_XMODMAP_DISABLE=1' >> /home/vagrant/.vnc/xstartup
    echo '/etc/X11/Xsession' >> /home/vagrant/.vnc/xstartup
    echo 'exec gnome-session &' >> /home/vagrant/.vnc/xstartup
    echo 'gnome-panel &' >> /home/vagrant/.vnc/xstartup
    echo 'gnome-settings-daemon &' >> /home/vagrant/.vnc/xstartup
    echo 'metacity &' >> /home/vagrant/.vnc/xstartup
    echo 'nautilus -n &' >> /home/vagrant/.vnc/xstartup
    echo 'gnome-terminal &' >> /home/vagrant/.vnc/xstartup
    chown vagrant:vagrant -R /home/vagrant/.vnc
    chown vagrant:vagrant /home/vagrant/.vnc/xtartup
    chmod +x /home/vagrant/.vnc/xstartup
  SHELL
end
