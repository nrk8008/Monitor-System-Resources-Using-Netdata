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

- Memory → Used RAM & Swap

- Storage → Disk Utilization

- Network → Network Interfaces

- Containers & VMs → Container metrics






