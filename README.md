# Monitor System Resources Using Netdata

Netdata is a free, open-source, real-time monitoring tool that collects, visualizes, and alerts on system and application performance metrics.

Think of it as a health dashboard for computer or server — it constantly watches CPU, memory, disk, network, Docker containers, databases, and more, then shows you live, interactive charts in a web UI.

  ## Key Features

- Real-time metrics (updates every second or less)
      
- Web-based dashboard at http://<host>:19999
      
- System & app monitoring (CPU, RAM, disk, network, processes, containers, databases, web servers, etc.)
      
- Built-in alerts & notifications for performance issues
      
- Lightweight (low resource usage)
      
- Works anywhere (Linux, Docker, Kubernetes, cloud servers, Raspberry Pi)

  
## Install and Run Netdata via Docker

      docker run -d --name=netdata \
        -p 19999:19999 \
        --cap-add SYS_PTRACE \
        --security-opt apparmor=unconfined \
        -e NETDATA_CLOUD_DISABLE=1 \
        netdata/netdata

## Install and Run Netdata via Docker gives Netdata access to the Docker API when running it.

            docker run -d --name=netdata \
              -p 19999:19999 \
              --cap-add SYS_PTRACE \
              --security-opt apparmor=unconfined \
              -v /var/run/docker.sock:/var/run/docker.sock \
              -v /proc:/host/proc:ro \
              -v /sys:/host/sys:ro \
              -v /etc/os-release:/host/etc/os-release:ro \
              -e NETDATA_CLOUD_DISABLE=1 \
              netdata/netdata

"-e NETDATA_CLOUD_DISABLE=1" tells Netdata to skip Cloud and load the full local dashboard.

The "-v /var/run/docker.sock:/var/run/docker.sock" part lets Netdata read Docker stats.

### To list only the running Docker containers:

            docker ps

Then open:

            http://localhost:19999

we will see the screen:
<img width="960" height="504" alt="Screen-1" src="https://github.com/user-attachments/assets/a8ecab4f-6914-4148-b2c0-c980dda7196c" />

Look at the bottom of the right panel — you should see:

            Skip and use the dashboard anonymously
            
Click that link.

<img width="960" height="504" alt="Screen-2" src="https://github.com/user-attachments/assets/a64cb86b-a9f6-48b4-ba9a-bc05bcae82c1" />

Scroll the System Overview menu and click:

- Compute → CPU (to show detailed CPU charts)

  <img width="960" height="504" alt="screen-3" src="https://github.com/user-attachments/assets/e245bc66-7ba1-4be3-bcc5-053132efbabd" />

- Memory → Used RAM & Swap

  <img width="960" height="504" alt="screen-4" src="https://github.com/user-attachments/assets/4d4380cf-5d80-404f-97d9-47afd682519a" />

- Storage → Disk Utilization

  <img width="960" height="504" alt="screen-5" src="https://github.com/user-attachments/assets/6eb9f26b-49d4-43d2-938a-79a6e89a520f" />

- Network → Network Interfaces

  <img width="960" height="504" alt="image" src="https://github.com/user-attachments/assets/55fe08b1-b70c-4b8c-862e-0cd5ccd59444" />

- Containers & VMs → Container metrics

  <img width="960" height="504" alt="screen-7" src="https://github.com/user-attachments/assets/0a3cc133-f8c7-41dd-b1c0-02de5595d776" />






