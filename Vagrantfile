# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.vm.define "ub1404" do |ub1404|
    ub1404.vm.box = "galaxy3/metasploitable2"
    #
    config.ssh.username = 'msfadmin'
    config.ssh.password = 'msfadmin'
    config.ssh.shell = "bash"

    # ub1404.vm.network "private_network", ip: '172.28.128.3'

    ub1404.vbguest.auto_update = false
    ub1404.ssh.insert_key = false
    ub1404.ssh.connect_timeout = 20
    ub1404.vm.boot_timeout = 120

  config.vm.synced_folder ".", "/vagrant", disabled: true

#    ub1404.vm.network "private_network", type: "dhcp",
#        auto_config: false,
#    	virtualbox__intnet: "metasploitable3"

    ub1404.vm.network "private_network", ip: '10.55.56.49',
        auto_config: false,
    	virtualbox__intnet: "metasploitable3"

#    ub1404.vm.network :private_network,
#                   :libvirt__network_name => 'metasploitable3'
#                   :ip => '192.168.1.10',
#                   :libvirt__netmask => '255.255.255.0',
#                   :libvirt__network_name => 'mynetwork',
#                   :libvirt__forward_mode => 'none'

    config.vm.network "forwarded_port", guest: 22, host: 2200, id: "ssh", disabled: true
    config.vm.network "forwarded_port", guest: 22, host: 25652, host_ip: "0.0.0.0", auto_correct: true

    config.vm.provision "shell" do |cmd|
        cmd.inline = "ifconfig eth1 10.55.56.49 netmask 255.255.255.0 up"
    end

    ub1404.vm.provider "virtualbox" do |v|
      v.name = "Metasploitable3-ub0000"
      v.memory = 2048
    end
  end

#  config.vm.define "win2k8" do |win2k8|
#    # Base configuration for the VM and provisioner
#    win2k8.vm.box = "rapid7/metasploitable3-win2k8"
#    win2k8.vm.hostname = "metasploitable3-win2k8"
#    win2k8.vm.communicator = "winrm"
#    win2k8.winrm.retry_limit = 60
#    win2k8.winrm.retry_delay = 10

#    win2k8.vm.network "private_network", type: "dhcp"

#    win2k8.vm.provider "libvirt" do |v|
#      v.memory = 4096
#      v.cpus = 2
#      v.video_type = 'qxl'
#      v.input :type => "tablet", :bus => "usb"
#      v.channel :type => 'unix', :target_name => 'org.qemu.guest_agent.0', :target_type => 'virtio'
#      v.channel :type => 'spicevmc', :target_name => 'com.redhat.spice.0', :target_type => 'virtio'
#      v.graphics_type = "spice"

#      # Enable Hyper-V enlightenments: https://blog.wikichoon.com/2014/07/enabling-hyper-v-enlightenments-with-kvm.html
#      v.hyperv_feature :name => 'stimer',  :state => 'on'
#      v.hyperv_feature :name => 'relaxed', :state => 'on'
#      v.hyperv_feature :name => 'vapic',   :state => 'on'
#      v.hyperv_feature :name => 'synic',   :state => 'on'
#    end

#    # Configure Firewall to open up vulnerable services
#    case ENV['MS3_DIFFICULTY']
#      when 'easy'
#        win2k8.vm.provision :shell, inline: "C:\\startup\\disable_firewall.bat"
#      else
#        win2k8.vm.provision :shell, inline: "C:\\startup\\enable_firewall.bat"
#        win2k8.vm.provision :shell, inline: "C:\\startup\\configure_firewall.bat"
#    end

#    # Insecure share from the Linux machine
#    win2k8.vm.provision :shell, inline: "C:\\startup\\install_share_autorun.bat"
#    win2k8.vm.provision :shell, inline: "C:\\startup\\setup_linux_share.bat"
#    win2k8.vm.provision :shell, inline: "rm C:\\startup\\*" # Cleanup startup scripts
#  end
end