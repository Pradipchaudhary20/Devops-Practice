Vagrant.configure("2") do |config|
  # Web server configuration
  config.vm.define "web" do |web|
    web.vm.box = "ubuntu/bionic64" 
    web.vm.hostname = "webserver" 
    web.vm.network "private_network", ip: "192.168.56.10" 

    # Forwarded port for Apache
    web.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

    
    web.vm.synced_folder "E:/vagrant_project/web_data", "/var/www/html", create: true

    web.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048"  
      vb.cpus = 1         
    end
    web.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      apt-get install -y apache2
    SHELL
  end

  # Database server configuration
  config.vm.define "db" do |db|
    db.vm.box = "ubuntu/bionic64" 
    db.vm.hostname = "database"
    db.vm.network "private_network", ip: "192.168.56.11" 

    db.vm.synced_folder "E:/vagrant_project/db_data", "/var/db_data", create: true

    db.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048" 
      vb.cpus = 1         
    end
    db.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      apt-get install -y mysql-server
    SHELL
  end
end
