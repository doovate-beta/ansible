# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  ssh_pub_key = File.readlines("/home/andrei/.ssh/id_rsa.pub").first.strip

  config.vm.define "bbdd" do |node1|
    node1.vm.box = "ubuntu/jammy64"
    node1.vm.network "private_network", ip: "192.168.56.31"
    node1.vm.hostname = "servidorBBDD"
    node1.vm.network "forwarded_port", guest: 3306, host: 33060
    node1.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048"
      vb.name = "BBDD"
      vb.cpus = 2
    end
    node1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      # Agregar clave SSH
      mkdir -p /home/vagrant/.ssh
      echo "#{ssh_pub_key}" >> /home/vagrant/.ssh/authorized_keys
      chmod 700 /home/vagrant/.ssh
      chmod 600 /home/vagrant/.ssh/authorized_keys
      chown -R vagrant:vagrant /home/vagrant/.ssh

      # Install docker on the machine
      apt-get install -y ca-certificates curl
      install -m 0755 -d /etc/apt/keyrings
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
      chmod a+r /etc/apt/keyrings/docker.asc
      echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
        $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
        tee /etc/apt/sources.list.d/docker.list > /dev/null
      apt-get update -y
      apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
      usermod -aG docker $USER || true
    SHELL
  end

  config.vm.define "web0" do |node2|
    node2.vm.box = "ubuntu/jammy64"
    node2.vm.network "private_network", ip: "192.168.56.32"
    node2.vm.hostname = "servidorWeb"
    node2.vm.network "forwarded_port", guest: 80, host: 8080
    node2.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048"
      vb.name = "WEB0"
      vb.cpus = 2
    end
    node2.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install default-jre -y
      # Agregar clave SSH
      mkdir -p /home/vagrant/.ssh
      echo "#{ssh_pub_key}" >> /home/vagrant/.ssh/authorized_keys
      chmod 700 /home/vagrant/.ssh
      chmod 600 /home/vagrant/.ssh/authorized_keys
      chown -R vagrant:vagrant /home/vagrant/.ssh

      # Install docker on the machine
      apt-get install -y ca-certificates curl
      install -m 0755 -d /etc/apt/keyrings
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
      chmod a+r /etc/apt/keyrings/docker.asc
      echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
        $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
        tee /etc/apt/sources.list.d/docker.list > /dev/null
      apt-get update -y
      apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
      usermod -aG docker $USER || true
    SHELL
  end

  config.vm.define "web1" do |node3|
    node3.vm.box = "ubuntu/jammy64"
    node3.vm.network "private_network", ip: "192.168.56.33"
    node3.vm.hostname = "servidorWeb2"
    node3.vm.network "forwarded_port", guest: 80, host: 9090
    node3.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048"
      vb.name = "WEB1"
      vb.cpus = 2
    end
    node3.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get upgrade -y
      # Agregar clave SSH
      mkdir -p /home/vagrant/.ssh
      echo "#{ssh_pub_key}" >> /home/vagrant/.ssh/authorized_keys
      chmod 700 /home/vagrant/.ssh
      chmod 600 /home/vagrant/.ssh/authorized_keys
      chown -R vagrant:vagrant /home/vagrant/.ssh

      # Install docker on the machine
      apt-get install -y ca-certificates curl
      install -m 0755 -d /etc/apt/keyrings
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
      chmod a+r /etc/apt/keyrings/docker.asc
      echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
        $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
        tee /etc/apt/sources.list.d/docker.list > /dev/null
      apt-get update -y
      apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
      usermod -aG docker $USER || true
    SHELL
  end
end
