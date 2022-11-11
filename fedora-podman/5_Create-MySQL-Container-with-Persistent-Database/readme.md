# Create MySQL Container with Persistent Database

## Instructions

1. Create the working directory.
```
mkdir -p /home/vagrant/local/mysql
```

2. Add the appropiate SELinux Context.
```
sudo semanage fcontext -a -t container_file_t '/home/vagrant/local/mysql(/.*)?'
```

3. Next thing to do is the restorecon.
```
sudo restorecon -R /home/vagrant/local/mysql/
```

4. Validate the context in the directory. Given context must be listed.
```
ls -Zd /home/vagrant/local/mysql
```

5. Change the owner of the created directory to the MySQL user and group.
```
podman unshare chown 27:27 /home/vagrant/local/mysql
```

Note: Alternatively you can run the same command with podman unshare to check numeric user ID (UID) from the container
```
podman unshare ls -ld /home/student/local/mysql/items
```


6. If not previously looged into  Red Hat registry, do it.
```
podman login registry.redhat.io
```

7. Pull MySQL image down.
```
podman pull registry.redhat.io/rhel8/mysql-80:1
```

8. Deploy now the database as follows.
```
podman run --name persist-db -d -v /home/vagrant/local/mysql:/var/lib/mysql/data \
    -e MYSQL_USER=user1 -e MYSQL_PASSWORD=redhat -e MYSQL_DATABASE=items \
    -e MYSQL_ROOT_PASSWORD=redhat registry.redhat.io/rhel8/mysql-80:1
```

9. Take a look of what is being created.
```
podman ps 
ls -l /home/vagrant/local/mysql
```
