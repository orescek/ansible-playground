ENV["LC_ALL"] = "en_US.UTF-8"

# ----- Variables --------

DOMAIN = ".vat.si"


Vagrant.configure(2) do |config|
  config.ssh.forward_agent=true
  config.vm.define "vat01", primary: true do |vat01|
    
    vat01.vm.box =  "ubuntu/xenial64"
    vat01.vm.hostname = "vat01"
    vat01.vm.network "private_network", ip:"192.168.101.10"
    vat01.vm.network "forwarded_port", guest: 8080, host: 8080, auto_correct: false
    vat01.vm.hostname = "vat01" + DOMAIN
    vat01.vm.provision "shell" do |s|
      s.path = "run.sh"
    end
      
    vat01.vm.provision "ansible" do |ansible|
      ansible.inventory_path="ansible/provision/inventory"
      ansible.playbook = "ansible/playbook.yml"
      ansible.groups = {
                        "build" => ["vat01"],
      }
      
    end
  end
end
