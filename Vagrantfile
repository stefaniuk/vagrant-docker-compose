unless Vagrant.has_plugin?("vagrant-docker-compose")
    system("vagrant plugin install vagrant-docker-compose")
    puts "Dependencies installed, please try the command again."
    exit 1
end

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "docker-host"
    config.vm.provider :virtualbox do |vb|
        vb.name = "vagrant-docker-compose"
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
        vb.memory = 4096
        vb.cpus = 4
    end

    config.ssh.username = "vagrant"
    config.ssh.password = "vagrant"
    config.ssh.insert_key = true

    config.vm.provision :docker
    config.vm.provision :docker_compose,
        yml: "/vagrant/docker-compose.yml",
        rebuild: true,
        project_name: "myproject",
        run: "always"

    config.vm.network :forwarded_port,
        guest: 8080, host: 8080,
        auto_correct: true
    config.vm.network :forwarded_port,
        guest: 8443, host: 8443,
        auto_correct: true
    config.vm.network :forwarded_port,
        guest: 5432, host: 5432,
        auto_correct: true
    config.vm.network :forwarded_port,
        guest: 6379, host: 6379,
        auto_correct: true

end
