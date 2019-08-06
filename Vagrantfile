require 'yaml'
settings = YAML.load_file 'ansible/group_vars/all.yml'

Vagrant.configure("2") do |config|

  config.vm.define "moodle-vm" do |srv|
    srv.vm.box = "debian/stretch64"
    srv.ssh.insert_key = false
    srv.vm.hostname = "moodle.box"
    srv.vm.network :private_network, ip: settings['moodle_host']

    srv.vm.provider :virtualbox do |vb|
      vb.name = "moodle"
      vb.memory = 2024
      vb.cpus = 2
    end
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    ansible.install_mode = "pip"
    # fix pip installation
    ansible.pip_install_cmd = "curl https://bootstrap.pypa.io/get-pip.py | sudo python"
    ansible.version = "latest"
#  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "ansible/system.yml"
    ansible.groups = {
      "moodle" => ["moodle-vm"],
      "all:vars" => {
        "timezone" => "Europe/Berlin"
      }
    }
    # comment/uncomment next line to activate/deavtivate pre-installation of edu-sharing-plugin (=> has to be finished manually, see README)
    ansible.skip_tags = [ "edu-sharing-plugin" ]
  end
end
