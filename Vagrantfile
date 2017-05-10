# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "pixelpin/ubuntu-1604-lamp"
  config.vm.box_url = "file:///T:/pixelpin-ubuntu-1604-lamp.box"
# zend2test.pixelpin.co.uk
  config.vm.network "private_network", ip: "192.168.33.11"
  
  

  config.vm.provision "shell", inline: <<-SHELL
  
	apt-get update
	
	cat > "/etc/apache2/sites-available/000-default.conf" <<-'EOF'
	<VirtualHost *:80>
		ServerAdmin callum@pixelpin.co.uk
		DocumentRoot /vagrant/public
		<Directory /vagrant/public>
			DirectoryIndex index.php
			AllowOverride all
			Require all granted
		</Directory>
		ErrorLog ${APACHE_LOG_DIR}/error.log
		CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>
	EOF
	service apache2 restart
	
	echo "CREATE DATABASE zend2;" | MYSQL_PWD=root mysql --user=root
	#zcat /vagrant/zend2.sql.gz | MYSQL_PWD=root mysql --user=root zend2
  SHELL
end
