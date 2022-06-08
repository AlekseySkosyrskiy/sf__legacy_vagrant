VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
  apt-get update"
  apt-get install postgresql
  sudo sed -i "s/#listen_address.*/listen_addresses '*'/" /etc/postgresql/9.1/main/postgresql.conf
  sudo su postgres -c "psql -c \"CREATE ROLE vagrant SUPERUSER LOGIN PASSWORD 'vagrant'\" "
  sudo su postgres -c "createdb -E UTF8 -T template0 --locale=en_US.utf8 -O vagrant wtm"  
  apt-get upgrade -y
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.cache.auto_detect = true
  config.vm.network :forwarded_port, guest: 5432, host: 5433
  config.vm.provision "shell", inline: $script
end
