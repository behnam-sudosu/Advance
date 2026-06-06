# router linux

## active linux as a router
### server side
sudo vim /etc/sysctl.conf  

    net.ipv4.ip_forward=1

save the file  
sudo sysctl -p  

### set firewall

#### nftables
sudo vim /etc/nftables.conf

###################################################################    
    #!/usr/sbin/nft -f
    flush ruleset
    table inet filter {
        chain input {
                type filter hook input priority 0;
                policy accept;
        }

        chain forward {
                type filter hook forward priority 0;
                policy accept;
        }

        chain output {
                type filter hook output priority 0;
                policy accept;
        }
    }

    table ip nat {
            chain postrouting {
                    type nat hook postrouting priority 100;
                    oif "enp1s0" masquerade
            }
    }
##################################################################
save the file  
sudo systemctl restart nftables  
sudo systemctl enable nftables === >> if dosn't enable  


################################################################
#!/usr/sbin/nft -f ===>> origin file

flush ruleset

table inet filter {
        chain input {
                type filter hook input priority filter;
        }
        chain forward {
                type filter hook forward priority filter;
        }
        chain output {
                type filter hook output priority filter;
        }
}
#################################################################


#!/usr/sbin/nft -f ===>> test done

flush ruleset

table inet filter {
    chain input {
            type filter hook input priority 0;
            policy accept;
    }

    chain forward {
            type filter hook forward priority 0;
            iif "enp11s0" oif "enp1s0" accept
            iif "enp1s0"  oif "enp11s0" ct state related,established accept
            drop
    }

    chain output {
            type filter hook output priority 0;
            policy accept;
    }
}

table ip nat {
        chain postrouting {
                type nat hook postrouting priority 100;
                    oif "enp1s0" masquerade
            }
    }


#### iptables

### client side  

change gateway to ip server 

##### ubuntu  
    sudo vim /etc/netplan/*.yaml  
    sudo netplan try  

##### debian  
    sudo vim /etc/network/interfaces  
    sudo systemctl restart networking  

##### centos  
    sudo vim /etc/sysconfig/network-script/ifcfg-ens37  
    sudo systemctl restart network

 
 




