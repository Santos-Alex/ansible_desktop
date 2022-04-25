#Vagrant.configure("2") do |config|
#  config.vm.box = "generic/rocky8"
#  config.vm.hostname = "master"
#  config.vm.box_check_update = false
#  config.vm.network "private_network", ip: "192.168.56.110"
#  config.vm.synced_folder ".", "/vagrant", disabled: true
#  config.ssh.username = "vagrant"
#  config.ssh.private_key_path=["~/.vagrant.d/insecure_private_key"]
#  config.ssh.insert_key = false
#  config.vm.provider "virtualbox" do |vb|
#    vb.gui = false
#    vb.memory = "2048"
#    vb.cpus = "2"
#    vb.name = "master"
#  end
#  config.vm.provision "shell", inline: <<-SHELL
#    apt-get update
#  SHELL
#end


Vagrant.configure("2") do |config|
# Declaring servers variables: Name, Distribution, Ip, SSH port  
  servers=[
    # Server 1
      {
        :hostname => "master",
        :box => "generic/rocky8",
        :ip => "192.168.56.110",
        :ssh_port => '2200'
      },
    # Server 2  
      {
        :hostname => "node1",
        :box => "generic/rocky8",
        :ip => "192.168.56.120",
        :ssh_port => '2201'
      },
    # Server 3  
      {
        :hostname => "node2",
        :box => "generic/rocky8",
        :ip => "192.168.56.130",
        :ssh_port => '2202'
      }
    ]
# Creating server loop for server configuration
  servers.each do |machine|                                                                     # Rename variable server to Machine
      config.vm.define machine[:hostname] do |node|                                             # Rename Machine to node 
          node.vm.box = machine[:box]                                                           # Defining linux distro
          node.vm.hostname = machine[:hostname]                                                 # Defining hostname 
          node.vm.network :private_network, ip: machine[:ip]                                    # Defining IP for server
          node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"      # Defining ssh port
          
          node.vm.provider :virtualbox do |vb|                                                  # Module for hardware specification
              vb.customize ["modifyvm", :id, "--memory", 1024]                                  # Alocating RAM memory
              vb.customize ["modifyvm", :id, "--cpus", 2]                                       # Alocating CPU's
              vb.gui = false                                                                    # Disable gui
              vb.name = node.vm.hostname                                                        # Setting name in Vbox

          end
      end
  end
  config.vm.provision "shell", inline: <<-SHELL
   yum update -y
  SHELL

end

