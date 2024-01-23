ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'
IMAGEN = "generic/ubuntu2004"
HOSTNAME = "master.home.local"
NODOS = 2

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/home/vagrant", type: "rsync", disabled: true

  config.vm.define :server do |s|
    s.vm.box = IMAGEN
    s.vm.hostname = HOSTNAME
    s.vm.box_check_update = false
    s.vm.provider :libvirt do |v|
      v.memory = 2048
      v.cpus = 2
      v.graphics_type = "none"
    end
  end

  (1..NODOS).each do |i|
    config.vm.define :"cliente-0#{i}" do |s|
      s.vm.box = IMAGEN
      s.vm.hostname = "cliente-0#{i}.home.local"
      s.vm.provider :libvirt do |v|
        v.memory = 1024
        v.cpus = 2
        v.graphics_type = "none"
      end
    end
  end
end
