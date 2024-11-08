FROM kalilinux/kali-rolling

# Set noninteractive environment and user
ENV DEBIAN_FRONTEND=noninteractive
ENV USER=root

# Update, upgrade, install utilities, core pentesting tools, and minimal GUI in one RUN command
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        sudo \
        curl \
        wget \
        git \
        vim \
        nano \
        unzip \
        net-tools \
        iputils-ping \
        dnsutils \
        lsof \
        procps \
        tmux \
        python3 \
        python3-pip \
        man-db \
        nmap \
        netcat-openbsd \
        sqlmap \
        hydra \
        nikto \
        metasploit-framework \
        john \
        hashcat \
        aircrack-ng \
        wireshark \
        tcpdump \
        burpsuite \
        gobuster \
        dirb \
        ftp \
        ssh \
        openssl \
        openjdk-11-jre \
        xfce4 \
        xfce4-terminal && \
    # Clean up to reduce image size
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN echo '#!/bin/bash\napt-get update && apt-get upgrade -y\nexec "$@"' > /usr/local/bin/startup.sh && \
    chmod +x /usr/local/bin/startup.sh

# Optional: Add a default command
CMD ["/bin/bash"]

# Start-up container using: docker run --cap-add=NET_RAW --cap-add=NET_ADMIN <image_name>
# This is to allow for the Container to access devices on internal/external network. 