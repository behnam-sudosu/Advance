# CPU alert
    vim /usr/local/bin/cpu-alert-light.sh
        #!/bin/bash
        THRESHOLD=50

        while true; do
            usage=$(top -bn1 | grep "Cpu(s)" | awk '{print int($2 + $4)}')
        if [ "$usage" -gt "$THRESHOLD" ]; then
            echo -e "\a"
            # beep ===>> on server
        fi
        sleep 5
        done
    save file
    sudo chmod +x cpu-alert-light.sh