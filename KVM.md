# install KVM Virtual Machine

    egrep -c '(vmx|svm)' /proc/cpuinfo ===>> show you can cpu support virtual machine must be show 1
    
# install
    sudo apt update
    sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager

# add user
    sudo usermod -aG libvirt $USER
    sudo usermod -aG kvm $USER
    log out and log in
    systemctl status libvirtd ===>> must running

# make virtual machine
    open virt-manager
    new vm
    choose local install media (iso)
    choose cpu and ram
    make storage
    finish

# make bridge 
    sudo apt update
    sudo install bridge-utils
    vim /etc/network/interfaces
    	auto br0
    	iface br0 inet dhcp
    		bridge_ports enp3s0
    		bridge_stp off
    		bridge_fd 0
    		bridge_maxwait 0
    save the file
    sudo systemctl restart networking.service
    
    in virtual machine
    go to show virtual hardware details
    NIC
    	Network source: Bridge device
    	Device name: br0
    	apply
    	
    
    
    
    
    
