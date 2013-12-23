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

      # Done.
      echo 'Done provisioning.'
    EOS
  end
end
