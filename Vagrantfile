Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu-13.04-amd64"
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/raring/current/raring-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.provider :virtualbox do |provider, override|
    override.vm.provision :shell, :inline => <<-EOS.gsub(/^ {6}/, "")
      # Install docker.
      wget -q -O - https://get.docker.io/gpg | apt-key add -
      echo 'deb http://get.docker.io/ubuntu docker main' > /etc/apt/sources.list.d/docker.list
      apt-get update -q
      apt-get install -q -y lxc-docker

      # Done.
      echo 'Done provisioning.'
    EOS
  end
end
