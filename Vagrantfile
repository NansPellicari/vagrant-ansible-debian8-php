Vagrant.configure("2") do |config|
    # Configure the box to use
    config.vm.box       = 'thoughtbot/debian-jessie-64'
#    config.vm.box_url   = 'https://atlas.hashicorp.com/ARTACK/boxes/debian-jessie'

    config.ssh.forward_agent = true

    # Configure the network interfaces
    config.vm.network :private_network, ip:    "10.10.15.150"
    config.vm.network :forwarded_port,  guest: 80,    host: 8080
    config.vm.network :forwarded_port,  guest: 8081,  host: 8081
    config.vm.network :forwarded_port,  guest: 3306,  host: 3306
    config.vm.network :forwarded_port,  guest: 27017, host: 27017

    # Configure shared folders
    config.vm.synced_folder ".",  "/vagrant", id: "vagrant-root", :nfs => true
    config.vm.synced_folder "..", "/var/www", id: "application",  :nfs => true

    # Configure VirtualBox environment
    config.vm.provider :virtualbox do |v|
        v.name = (0...8).map { (65 + rand(26)).chr }.join
        v.customize [ "modifyvm", :id, "--memory", 2048 ]
    end

    # Provision the box
    config.vm.provision :ansible do |ansible|
        ansible.playbook = "ansible/site.yml"
        ansible.extra_vars = "@../ansible_vars.yml"
  #      ansible.start_at_task = "projects provision"
    end
end
