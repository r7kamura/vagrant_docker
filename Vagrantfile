Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.provider :virtualbox do |provider, override|
    override.vm.provision :shell, :inline => <<-EOS.gsub(/^ {6}/, "")
      # Add GPG key.
      wget -q -O - https://get.docker.io/gpg | apt-key add -

      # Create docker.list for deb.
      echo 'deb http://get.docker.io/ubuntu docker main' > /etc/apt/sources.list.d/docker.list

      # Update remote package metadata.
      apt-get update -q

      # Install docker.
      apt-get install -q -y lxc-docker

      # Create docker:vagrant user.
      usermod -a -G docker vagrant

      # Install the VirtualBox guest additions. (this may need to reboot machine)
      # Kernel Headers and dkms are required to build the vbox guest kernel modules.
      apt-get install -q -y linux-headers-generic-lts-raring dkms

      # Install VBox Guest Additions 4.3.2.
      wget -cq http://dlc.sun.com.edgesuite.net/virtualbox/4.3.2/VBoxGuestAdditions_4.3.2.iso
      mount -o loop,ro /home/vagrant/VBoxGuestAdditions_4.3.2.iso /mnt
      /mnt/VBoxLinuxAdditions.run --nox11
      umount /mnt

      # Done.
      echo 'Done provisioning.'
    EOS
  end
end
