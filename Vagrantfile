Vagrant.configure("2") do |config|
    # Especifica la caja base
    config.vm.box = "ubuntu/jammy64"
    
    # Configurar recursos de la máquina virtual
    config.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 1
    end
  
    # Configurar el aprovisionamiento de Apache
    config.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y apache2
      echo "<h1>Hola Mundo</h1>" | sudo tee /var/www/html/index.html
      sudo systemctl restart apache2
    SHELL
  
    # Configurar el puerto para acceder a Apache
    config.vm.network "forwarded_port", guest: 80, host: 8080
  
    # Compartir el directorio local 'src' con la carpeta de Apache en la VM
    config.vm.synced_folder "src", "/var/www/html", type: "virtualbox"
  end