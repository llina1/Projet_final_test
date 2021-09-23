Vagrant.configure(2) do |config|

	# Set some variables
  etcHosts=""
  common = <<-SHELL
  sudo apt update -qq 2>&1 >/dev/null
  sudo apt install -y -qq git vim tree net-tools telnet 2>&1 >/dev/null
  sudo echo "autocmd filetype yaml setlocal ai ts=2 sw=2 et" > /home/vagrant/.vimrc
  sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/g' /etc/ssh/sshd_config
  sudo systemctl restart sshd
  SHELL

	# set vagrant image
	config.vm.box = "ubuntu/focal64"
	config.vm.box_url = "ubuntu/focal64"

	# set servers list and their parameters
	NODES = [
  	{ :hostname => "USRHapMain", :ip => "172.16.254.252", :cpus => 1, :mem => 1024 },
  	{ :hostname => "USRHapFail", :ip => "172.16.254.251", :cpus => 1, :mem => 1024 },
  	{ :hostname => "MasterNode", :ip => "172.16.250.254", :cpus => 1, :mem => 2048 },
  	{ :hostname => "BackupNode", :ip => "172.16.250.253", :cpus => 1, :mem => 2048 },
  	{ :hostname => "WorkersNode", :ip => "172.16.249.254", :cpus => 2, :mem => 2048 },
	]

	# define /etc/hosts for all servers
  NODES.each do |node|
   	etcHosts += "echo '" + node[:ip] + "   " + node[:hostname] + "' >> /etc/hosts" + "\n"
  end #end NODES

	# run installation
  NODES.each do |node|
    config.vm.define node[:hostname] do |cfg|
			cfg.vm.hostname = node[:hostname]
      cfg.vm.network "private_network", ip: node[:ip]
      cfg.vm.provider "virtualbox" do |v|
				v.customize [ "modifyvm", :id, "--cpus", node[:cpus] ]
        v.customize [ "modifyvm", :id, "--memory", node[:mem] ]
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
        v.customize ["modifyvm", :id, "--name", node[:hostname] ]
      end #end provider
			
			#for all
      cfg.vm.provision :shell, :inline => etcHosts
			cfg.vm.provision :shell, :inline => common

    end # end config
  end # end nodes
end 
