# Monitor System Resources Using Netdata

Netdata is a free, open-source, real-time monitoring tool that collects, visualizes, and alerts on system and application performance metrics.

Think of it as a health dashboard for computer or server — it constantly watches CPU, memory, disk, network, Docker containers, databases, and more, then shows you live, interactive charts in a web UI.

# Install and Run Netdata via Docker

      docker run -d \
        --name=netdata \
        -p 19999:19999 \
        --cap-add SYS_PTRACE \
        --security-opt apparmor=unconfined \
        netdata/netdata
