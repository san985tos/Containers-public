# Rootless containers

## Instructions

1. Running a root container

   - Run a temporal container using "sudo"

   ```
   sudo podman run --rm --name asroot -it registry.access.redhat.com/ubi8:latest /bin/bash
   ```

   - Notice that once inside the container, the root user is used, execute the following commands:

   ```
   whoami
   id
   ```

   - Run sleep command as follows:

   ```
   sleep 10000
   ```

   - Open another terminal, and look for the container using ps command (notice the user on which the container is running)

   ```
   ps -aux | grep sleep
   ```

   - The output must be something similar to the following out put (notice is being executed as root)

   ```
   [vagrant@fedora-podman ~]$ ps -aux | grep sleep
   root       14434  0.0  0.0  30228  1424 pts/0    S+   03:14   0:00 /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 10000
   vagrant    14461  0.0  0.0   6140   840 pts/1    S+   03:15   0:00 grep --color=auto sleep
   [vagrant@fedora-podman ~]$
   ```

   - Go back to the first terminal ctrl + c and exit the container

   ```
   exit
   ```

2. Run a rootless container

- Run a temporal container without using "sudo"
  ```
  podman run --rm --name noroot -it registry.access.redhat.com/ubi8:latest /bin/bash
  ```
  - Notice that once inside the container, the root user is used, execute the following commands:
  ```
  whoami
  id
  ```
  - Run sleep command as follows:
  ```
  sleep 10000
  ```
  - Open another terminal, and look for the container using ps command (notice the user on which the container is running)
  ```
  ps -aux | grep sleep
  ```
  - The output must be something similar to the following out put (notice is being executed as other user than root)
  ```
   [vagrant@fedora-podman ~]$ ps -aux | grep sleep
   vagrant    14647  0.0  0.0  30228  1484 pts/0    S+   03:19   0:00 /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 10000
   vagrant    14649  0.0  0.0   6140   768 pts/1    S+   03:19   0:00 grep --color=auto sleep
   [vagrant@fedora-podman ~]$
  ```
  - Go back to the first terminal and exit the container
  ```
  exit
  ```
