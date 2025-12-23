Error: Docker containers were not getting created due to insufficient space.

Troubelshooting steps:
1) Checked disk space: df -h
   -> /dev/root was 100% used
2) Then to find what is consuming the space ran: du -xh / --max-depth=1 | sort -rh
   -> This command checks in root (/) which directories are consuming highest size and lists them
3) .minikube and .kube were consuming the most space. Almost 90%.
   -> I was not actively using minikube hence deleted it, removed its dependent directories.
4) Then containerd in /var/lib folder was consuming lot of space around 2.9G, deleted it using - docker system prune -a --volumes
   -> THis freed lot of space.

Note: To get into var , containerd, etc root permissions are needed. You can go into root using : sudo -i

