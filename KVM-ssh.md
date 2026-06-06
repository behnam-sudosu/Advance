# install KVM with server
# install server
    sudo apt update
    sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst

set ip static on server
usermod -aG libvirt behnam
usermod -aG kvm behnam

systemctctl start libvirtd
systemctctl enable libvirtd

logout
login

# install client desktop
    apt update
    apt install virt-manager virt-viewer

usermod -aG Libvirt behnam
logout
login
run virt-manager
    file
        add connection
            username USER server
            hostname IP_ADDRESS server
    	check mark to cennect ro remote
        host over shh
        connect
        
copy your ssh_key to server    

# make bridge 
    sudo apt update
    sudo install bridge-utils
    vim /etc/network/interfaces
    	auto enp2s0
        iface enp2so inet manual

        auto br0
        iface br0 inet static
        address 192.168.1.10
        netmask 255.255.255.0
        gateway 192.168.1.1
        bridge_ports enp2s0
        bridge_stp pff
        bridge_fd 0
        
    sudo systemctl restart networking.service
    
    in virtual machine
    go to show virtual hardware details
    NIC
    	Network source: Bridge device
    	Device name: br0
    	apply
    	
# error
    ~/.ssh/config
        Host 192.168.1.90
            Port 4012
            User debian