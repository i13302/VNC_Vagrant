# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url ="https://app.vagrantup.com/ubuntu/boxes/trusty64"

  config.vm.define "client" do |ct|
    ct.vm.hostname = "vnc"
    #ct.vm.network :public_network, bridge: "eth0"
    ct.vm.network :forwarded_port, id:"ssh",    guest:   22, host:40021
    ct.vm.network :forwarded_port, id:"vnc",    guest: 5901, host:45901
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update  -y && \
    #apt-get install -y ubuntu-desktop vnc4server gnome-core gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
    apt-get install -y ubuntu-desktop
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
    echo '??<?rzX' > /home/vagrant/.vnc/passwd
    chown vagrant:vagrant -R /home/vagrant/.vnc
    chown vagrant:vagrant /home/vagrant/.vnc/xstartup
    chmod +x /home/vagrant/.vnc/xstartup
    cd /home/vagrant
    #sudo -u vagrant vncserver :1 --geometry 1024x768

  SHELL
end
