servers=[
{
  :hostname => "server3",
  :ip => "192.168.70.10",
  :box => "gusztavvargadr/windows-10",
  :ram => 512,
  :cpu => 1,
  :provisions => []
},
{
  :hostname => "server4",
  :ip => "192.168.70.11",
  :box => "gusztavvargadr/windows-10",
  :ram => 512,
  :cpu => 1,
  :provisions => []
}
]

Vagrant.configure(2) do |config|
  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
        machine [:provisions].each do |script|
           node.vm.provision :shell, :path => script
        end
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
      node.vm.network "private_network", ip: machine[:ip]
      node.vm.provider "virtualbox" do |vb|
        vb.customize [ "modifyvm", :id, "--uartmode1", "file", File::NULL ]
        vb.memory = machine[:ram]
        vb.cpus = machine[:cpu]
      end
    end
  end
end


