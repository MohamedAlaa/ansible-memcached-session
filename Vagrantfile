# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 tw=0 et :

hosts = {
  "session" => {
    ip: "192.168.50.11",
    :port => "2210",
    :ram => "256",
    :cpu => "50",
    :url => "https://github.com/holms/vagrant-centos7-box/releases/download/7.1.1503.001/CentOS-7.1.1503-x86_64-netboot.box"
  },
}

Vagrant.configure("2") do |config|
  hosts.each do |name, host_config|
    config.vm.define name do |machine|
      machine.vm.box = "centos7"
      machine.vm.box_url = host_config[:url]
      machine.vm.hostname = "%s.my-staging.com" % name
      machine.vm.network :private_network, ip: host_config[:ip]
      config.vm.network :forwarded_port, guest: 22, host: host_config[:port], id: "ssh", auto_correct: true
      machine.vm.provider "virtualbox" do |v|
          v.name = name
          v.customize ["modifyvm", :id, "--cpuexecutioncap", host_config[:cpu]]
          v.customize ["modifyvm", :id, "--memory", host_config[:ram]]
      end
    end
  end
end
