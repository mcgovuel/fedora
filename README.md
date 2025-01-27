#!/bin/bash

# autor: Alvaro Jim Junior
# version: 1.0
# Cleaner Fedora

echo "Clean cache and packages."
sudo dnf clean all;
sudo yum clean all;

echo "Clean unused flatpaks."
sudo flatpak uninstall --unused;
sudo flatpak repair;
sudo flatpak update;

echo "Clean Temp Files"
sudo rm -rf /var/tmp/*;
sudo rm -rf /tmp/*;

echo "Clean systemd." 
sudo rm /var/lib/systemd/coredump/*;

echo "Clean Trash"
sudo rm -rf /home/$user/.local/share/Trash/files/*;

echo "Clear Buffer/Cache"
sudo sync && echo 1 > /proc/sys/vm/drop_caches;
sudo sync && echo 3 | sudo tee /proc/sys/vm/drop_caches;

echo "DNF Refresh"
sudo dnf upgrade --refresh;

echo $0
