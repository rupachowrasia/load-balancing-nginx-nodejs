if Vagrant::VERSION < "2.0.0"
  $stderr.puts "Must redirect to new repository for old Vagrant versions"
  Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')
end

Vagrant.configure("2") do |config|
  config.vm.define :testenv1 do |testenv1|
    testenv1.vm.box = "ubuntu/xenial64"
    testenv1.vm.network :private_network, ip: "192.168.31.101"
    testenv1.vm.hostname = "box1.me"
    testenv1.vm.provision :shell, path: "provision-box1", args: ENV['ARGS']
	testenv1.vm.network :forwarded_port, guest: 3000, host: 3000, id: "node", host_ip: "localhost", auto_correct: true
	testenv1.vm.network :forwarded_port, guest: 3001, host: 3001, id: "node", host_ip: "localhost", auto_correct: true
	testenv1.vm.network :forwarded_port, guest: 3002, host: 3002, id: "node", host_ip: "localhost", auto_correct: true
	testenv1.vm.network :forwarded_port, guest: 3003, host: 3003, id: "node", host_ip: "localhost", auto_correct: true
	testenv1.vm.network :forwarded_port, guest: 3004, host: 3004, id: "node", host_ip: "localhost", auto_correct: true
	testenv1.vm.network :forwarded_port, guest: 3005, host: 3005, id: "node", host_ip: "localhost", auto_correct: true
	testenv1.vm.network "forwarded_port", guest: 80, host: 8080, id: "nginx"
    testenv1.vm.synced_folder "shared/", "/home/vagrant/shared", create: true

    testenv1.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--cpus", "1", "--memory", 20000]
    end
  end
  
  config.vm.define :testenv2 do |testenv2|
    testenv2.vm.box = "ubuntu/xenial64"
    testenv2.vm.network :private_network, ip: "192.168.31.102"
    testenv2.vm.hostname = "box2.me"
    testenv2.vm.provision :shell, path: "provision-box2", args: ENV['ARGS']
	testenv2.vm.network :forwarded_port, guest: 3000, host: 3000, id: "node", host_ip: "localhost", auto_correct: true
	testenv2.vm.network :forwarded_port, guest: 3001, host: 3001, id: "node", host_ip: "localhost", auto_correct: true
	testenv2.vm.network :forwarded_port, guest: 3002, host: 3002, id: "node", host_ip: "localhost", auto_correct: true
	testenv2.vm.network :forwarded_port, guest: 3003, host: 3003, id: "node", host_ip: "localhost", auto_correct: true
	testenv2.vm.network :forwarded_port, guest: 3004, host: 3004, id: "node", host_ip: "localhost", auto_correct: true
	testenv2.vm.network :forwarded_port, guest: 3005, host: 3005, id: "node", host_ip: "localhost", auto_correct: true
    testenv2.vm.synced_folder "shared/", "/home/vagrant/shared", create: true

    testenv2.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--cpus", "1", "--memory", 20000]
    end
  end
  
  config.vm.define :testenv3 do |testenv3|
    testenv3.vm.box = "ubuntu/xenial64"
    testenv3.vm.network :private_network, ip: "192.168.31.103"
    testenv3.vm.hostname = "box3.me"
    testenv3.vm.provision :shell, path: "provision-box3", args: ENV['ARGS']
	testenv3.vm.network :forwarded_port, guest: 3000, host: 3000, id: "node", host_ip: "localhost", auto_correct: true
	testenv3.vm.network :forwarded_port, guest: 3001, host: 3001, id: "node", host_ip: "localhost", auto_correct: true
	testenv3.vm.network :forwarded_port, guest: 3002, host: 3002, id: "node", host_ip: "localhost", auto_correct: true
	testenv3.vm.network :forwarded_port, guest: 3003, host: 3003, id: "node", host_ip: "localhost", auto_correct: true
	testenv3.vm.network :forwarded_port, guest: 3004, host: 3004, id: "node", host_ip: "localhost", auto_correct: true
	testenv3.vm.network :forwarded_port, guest: 3005, host: 3005, id: "node", host_ip: "localhost", auto_correct: true
    testenv3.vm.synced_folder "shared/", "/home/vagrant/shared", create: true

    testenv3.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--cpus", "1", "--memory", 20000]
    end
  end
  
  config.vm.define :testenv4 do |testenv4|
    testenv4.vm.box = "ubuntu/xenial64"
    testenv4.vm.network :private_network, ip: "192.168.31.104"
    testenv4.vm.hostname = "box4.me"
    testenv4.vm.provision :shell, path: "provision-box4", args: ENV['ARGS']
	testenv4.vm.network :forwarded_port, guest: 3000, host: 3000, id: "node", host_ip: "localhost", auto_correct: true
	testenv4.vm.network :forwarded_port, guest: 3001, host: 3001, id: "node", host_ip: "localhost", auto_correct: true
	testenv4.vm.network :forwarded_port, guest: 3002, host: 3002, id: "node", host_ip: "localhost", auto_correct: true
	testenv4.vm.network :forwarded_port, guest: 3003, host: 3003, id: "node", host_ip: "localhost", auto_correct: true
	testenv4.vm.network :forwarded_port, guest: 3004, host: 3004, id: "node", host_ip: "localhost", auto_correct: true
	testenv4.vm.network :forwarded_port, guest: 3005, host: 3005, id: "node", host_ip: "localhost", auto_correct: true
    testenv4.vm.synced_folder "shared/", "/home/vagrant/shared", create: true

    testenv4.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--cpus", "1", "--memory", 20000]
    end
  end

end
