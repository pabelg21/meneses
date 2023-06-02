Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy"
  
  config.vm.network "private_network", ip: "192.168.33.222" 
  config.vm.network "public_network", ip: "10.1.1.225", bridge: "Realtek PCIe GbE Family Controller #2"
  config.vm.hostname = "jenkins"
  
  config.vm.provider "virtualbox" do |vb|
    vb.name = "jenkins"
    vb.memory = "4096"
  end

  config.vm.provision "shell", inline: <<-SHELL
    # Actualizar los repositorios y paquetes existentes
    sudo apt-get update -y

    # Instalar Java (requerido por Jenkins)
    sudo apt-get install -y default-jdk

    # Descargar e instalar Jenkins
    wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
    sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    sudo apt-get update -y
    sudo apt-get install -y jenkins

    # Iniciar el servicio de Jenkins
    sudo systemctl start jenkins
  SHELL
end
