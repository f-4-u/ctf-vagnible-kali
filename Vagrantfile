Vagrant.configure("2") do |config|
    config.vm.box = "kalilinux/rolling"

    config.vm.define "kali_ctf_box" do |vm|
        # Mount shared folders
        config.vm.synced_folder "~/pentest/", "/opt/pentest", create: true
        config.vm.synced_folder "~/pentest/bin", "/opt/bin", create: true
        config.vm.synced_folder "~/pentest/tools", "/opt/tools", create: true
        config.vm.synced_folder "~/pentest/wordlists", "/opt/wordlists", create: true
        config.vm.synced_folder "~/pentest/vpn", "/opt/vpn", create: true

        config.vm.provision "file", source: "./assets/censored.env", destination: "/tmp/censored.env"

        # Use static IP address to avoid DHCP conflicts
        config.vm.network "private_network", ip: "192.168.56.10"

        config.vm.provider "virtualbox" do |vb|
            vb.memory = "8192"
            vb.cpus = 6

            vb.name = "CTF___kali"

            # Disable drag and drop
            vb.customize ["modifyvm", :id, "--draganddrop", "disabled"]
        end

        # Provision with Ansible
        config.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "ansible/provision.yml"
        end
    end
end
