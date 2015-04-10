VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "jonludlam/xs-centos-6.5"
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :xenserver do |xs|
    xs.memory = 2048
    xs.xs_host = "gandalf.uk.xensource.com"
    xs.xs_username = "root"
    xs.xs_password = "xenroot"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "build.yml"
    ansible.raw_ssh_args = "-o ProxyCommand=\"ssh -W %h:%p root@gandalf.uk.xensource.com\""
  end
end
