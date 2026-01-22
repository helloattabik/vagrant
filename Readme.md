# Vagrant Quick Reference Guide

This README provides essential commands and the structure overview for managing Vagrant virtual machines efficiently.

---

## Common Vagrant Commands

| Command                 | Description                          |
|-------------------------|------------------------------------|
| `vagrant init .`         | Create a new `Vagrantfile` in the current directory. |
| `vagrant up`             | Start and configure the VM as defined in the `Vagrantfile`. |
| `vagrant destroy`        | Stop and delete the VM completely. |
| `vagrant reload`         | Restart the VM, applying any changes in the configuration. |
| `vagrant provision`      | Re-run the provisioning scripts on the running VM. |

---

## Basic Structure of a `Vagrantfile`

```ruby
Vagrant.configure("2") do |node|
  node.vm.box = "os/distro"                    # Specify the base box OS or distribution
  node.vm.hostname = "hostname"                 # Set the hostname of the VM

  # Network configuration (private network)
  node.vm.network "private_network", type: "static", ip: "ipaddress"

  # VirtualBox provider settings
  node.vm.provider "virtualbox" do |vb|
    vb.name = "vm_name"                         # Name shown in VirtualBox GUI
    vb.memory = 2048                            # RAM allocation in MB (integer)
    vb.cpus = 2                                # Number of CPU cores (integer)
    vb.gui = false                             # Enable GUI (true/false)
  end

  # Shell provisioning - run shell commands/scripts inside the VM
  node.vm.provision "shell", inline: <<-SHELL
    # Your shell script commands here
  SHELL
end
