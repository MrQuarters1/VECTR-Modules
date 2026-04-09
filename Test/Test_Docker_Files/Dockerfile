FROM matrixregistry.azurecr.io/base_images/kali_base:latest
# The base image pulled from our container registry exposes ports 6080, and 5901, creates the vncuser and installs only needed base packages 

# Sets the Debian conmfiguration frontend to a non-interactive mode so it doesn't ask questions during package installation or configuration and accepts default answers for all prompts
ENV DEBIAN_FRONTEND=noninteractive

# Keep-awake screensaver config
RUN mkdir -p /home/vncuser/.config/xfce4/xfconf/xfce-perchannel-xml

COPY xfce4-screensaver.xml /home/vncuser/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-screensaver.xml

# Copy lab content files to vncuser downloads directory
COPY --chown=vncuser:vncuser Content/ /home/vncuser/Downloads/

# Become root to install packages \ use this instead of sudo when installing packages
USER root

# Install packages to meet requirements
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      wireshark iputils-ping traceroute dnsutils nmap snort && \
      cp -r /usr/lib/nmap /opt/nmap && \
      chmod +x /opt/nmap/nmap && \
      rm /usr/bin/nmap && \
      printf '#!/bin/sh\nexec /opt/nmap/nmap "$@"' > /usr/bin/nmap && \
      chmod +x /usr/bin/nmap \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Ping requires capabilities in K8s
RUN setcap cap_net_raw+p /usr/bin/ping

# Return to vncuser
USER vncuser

# Start services
CMD ["/bin/zsh", "/home/vncuser/command_watch/start_services.sh"]
