# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "fedora/25-cloud-base"

  # bootstrap and run with ansible
  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "scenario-template.yml"
      ansible.extra_vars = {
         # The selinuxgame playbook does not work without python3
         ansible_python_interpreter: '/usr/bin/python3'
      }
  end

  # Create the "dev" box
  config.vm.define "dev" do |dev|
    dev.vm.host_name = "dev.example.com"

    dev.vm.provider :libvirt do |domain, override|
        domain.cpus = 4
        # In some cases, the guest gets stuck at "Waiting for domain to get an IP address..." if
        # the default cpu_mode, 'host-model', is used. Using 'host-passthrough' cpu_mode prevents
        # VM migration between hosts with different CPUs. However, development environments are
        # expected to live on a single host for the duration of their existence. Due to this known
        # issue and our use case, the default cpu_mode is overridden.
        domain.cpu_mode = "host-passthrough"
        domain.graphics_type = "spice"
        domain.memory = 2048
        domain.video_type = "qxl"

        # Uncomment this to expand the disk to the given size, in GB (default is usually 40)
        # You'll also need to uncomment the provisioning step below that resizes the root partition
        # do not set this to a size smaller than the base box, or you will be very sad
        # domain.machine_virtual_size = 80

        # Uncomment the following line if you would like to enable libvirt's unsafe cache
        # mode. It is called unsafe for a reason, as it causes the virtual host to ignore all
        # fsync() calls from the guest. Only do this if you are comfortable with the possibility of
        # your development guest becoming corrupted (in which case you should only need to do a
        # vagrant destroy and vagrant up to get a new one).
        #
        # domain.volume_cache = "unsafe"

        # Uncomment this to resize the root partition and filesystem to fill the base box disk
        # This script is only guaranteed to work with the default official fedora image, and is
        # only needed it you changed machine_virtual_size above.
        # For other boxen, use at your own risk
        # override.vm.provision "shell", path: "scripts/vagrant-resize-disk.sh"
    end
  end
end
