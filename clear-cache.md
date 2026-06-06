# cear-cache

## add new line
    vim /etc/sysctl.conf
        vm.swappiness=10
        vm.vfs_cache_pressure=300
    save file

    sudu sysctl -p

## script
    sudo vim /usr/local/bin/clear-cache
        #!/bin/bash
        sync
        sh -c "echo 3 > /proc/sys/vm/drop_caches"
    save file
    sudo chmod +x /usr/local/bin/clear-cache

## cronjob
    vim /etc/crontab
        */5 * * * * /usr/local/bin/clear-cache