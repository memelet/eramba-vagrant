Vagrant.configure("2") do |config|
  config.env.enable

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  config.persistent_storage.enabled = false
  config.persistent_storage.location = ".data/mysql.vdi"
  config.persistent_storage.size = 1000
  config.persistent_storage.mountname = "mysql"
  config.persistent_storage.filesystem = "ext4"
  config.persistent_storage.mountpoint = "/var/lib/mysql"
  config.persistent_storage.use_lvm = true

  config.vm.box = ENV['VAGRANT_BOXNAME']
  config.vm.hostname = ENV['VAGRANT_HOSTNAME']
  config.vm.network :private_network, ip: ENV['VAGRANT_IP']
  #config.vm.synced_folder ".data/mysql", "#{mysql_datadir}", owner: mysql_group_id, group: mysql_user_id

  config.vm.provider :virtualbox do |vb|
    vb.name = ENV['VAGRANT_HOSTNAME']
    vb.memory = 4096
    vb.cpus = 4
    vb.linked_clone = true
  end

  config.vm.provision "os", type: "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "ansible/playbooks/os.yml"
    ansible.extra_vars = {
      ubuntu_upgrade: ENV['UBUNTU_UPGRADE'],
    }
  end

  config.vm.provision "mysql", type: "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "ansible/playbooks/mysql.yml"
    ansible.extra_vars = {
      mysql_vagrant_host_root_access: true
    }
  end

  config.vm.provision "eramba", type: "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "ansible/playbooks/eramba.yml"
    ansible.extra_vars = {
      apache_servername: ENV['VAGRANT_HOSTNAME'],
      eramba_tgz_url: ENV['ERAMBA_TGZ_URL'],
      eramba_version: ENV['ERAMBA_VERSION'],
      eramba_www_dir: ENV['ERAMBA_WWW_DIR'],
      wkhtmltopdf_version: ENV['WKHTMLTOPDF_VERSION']
    }
  end
end
