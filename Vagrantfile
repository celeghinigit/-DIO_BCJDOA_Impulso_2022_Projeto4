machines = {
  "master" => {"memory" => "1024", "cpu" => "1", "image" => "bento/ubuntu-22.04", "ip" => "192.168.100.10"},
  "node01" => {"memory" => "1024", "cpu" => "1", "image" => "bento/ubuntu-22.04", "ip" => "192.168.100.11"},
  "node02" => {"memory" => "1024", "cpu" => "1", "image" => "bento/ubuntu-22.04", "ip" => "192.168.100.12"},
  "node03" => {"memory" => "1024", "cpu" => "1", "image" => "bento/ubuntu-22.04", "ip" => "192.168.100.13"}
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "public_network", ip: "#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        
      end
      machine.vm.provision "shell", path: "instalar-docker.sh"

      if "#{name}" == "master"
        machine.vm.provision "shell", path: "master.sh", args: "#{conf["ip"]}"
      else
        machine.vm.provision "shell", path: "worker.sh"
      end
    end
  end
end