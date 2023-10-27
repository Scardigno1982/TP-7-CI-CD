Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.network "public_network", type: "dhcp"

  config.vm.provision "shell", inline: <<-SHELL
    # Actualiza el sistema
    sudo apt-get update
    sudo apt-get upgrade -y

    # Instala Docker
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    sudo apt-get update
    sudo apt-get install openjdk-11-jre -y
    sudo apt-get install docker-ce -y
    sudo usermod -aG docker ${USER}
    sudo systemctl enable docker

    # Instala Jenkins

    # Agrega la clave GPG del repositorio de Jenkins
    wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -

    # Si el paso anterior no funciona, intenta este método alternativo para agregar la clave:
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5BA31D57EF5975CA

    # Añade el repositorio de Jenkins
    sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

    # Actualiza la lista de paquetes
    sudo apt-get update

    # Instala Jenkins
    sudo apt-get install jenkins -y

    # Inicia y habilita Jenkins
    sudo systemctl start jenkins
    sudo systemctl enable jenkins

    #Mostrar el initialAdminPassword de Jelkins
    #Copiar para ingresar a la direccion ip 0.0.0.0:8080

    sudo su -
    echo "La clave de Jenkins es:"
    cat /var/lib/jenkins/secrets/initialAdminPassword
  SHELL
end
