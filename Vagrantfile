Vagrant.configure("2") do |config|
    
        config.vm.box = "ubuntu/focal64"
        config.vm.box_check_update = false
        # gitlab server
        config.vm.define "gitlab-server" do |gitlabserver|
            gitlabserver.vm.network "private_network", ip: "10.32.4.111"
            gitlabserver.vm.provider "gitlab-virtualbox" do |vb_gitlab|
                vb_gitlab.name = "gitlabserver.xtl"
                vb_gitlab.cpus = 2
                vb_gitlab.memory = "2048"
            end
            gitlabserver.vm.provision "shell", path: "./docker-install.sh"
            gitlabserver.vm.provision "shell", inline: <<-SHELL
                echo "root:hoang" | chpasswd
                sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
                systemctl reload sshd
        SHELL
        end 
        

        # gitlab runner and registry
end  
