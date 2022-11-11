# A simple MYSQL database lab

## Instructions

1. Sign up to Red Hat Quay.io [https://quay.io/]
   ![This is an image](images/quay.io)
2. On the vagrant machine (fedora-podman), execute the following command followed by the user and password

```
podman login registry.redhat.io
```

3. Start a container from the Red Hat catalog MYSQL image

```
podman run --name mysql-basic -e MYSQL_USER=user1 \
    -e MYSQL_PASSWORD=mypa55 -e MYSQL_ROOT_PASSWORD=rootpa55 \
    -e MYSQL_DATABASE=items -d registry.redhat.io/rhel8/mysql-80:1
```

4. Access to the container

```
podman exec -it mysql-basic /bin/bash
```

5. Add data to the database
   - Connect to the database
   ```
   mysql -u root
   ```
   - Select the "items" databse
   ```
   SHOW DATABASES;
   USE items;
   ```
   - Create a table called Projects in the items database
   ```
   CREATE TABLE Projects (id int NOT NULL,
    name varchar(255) DEFAULT NULL,
    code varchar(255) DEFAULT NULL,
    PRIMARY KEY (id));
   ```
   - Insert data to the database
   ```
   INSERT INTO Projects (id, name, code) VALUES (1,'DevOps','DO180');
   ```
   - Verify the data
   ```
   SELECT * FROM Projects;
   ```
6. Exit from MYSQL prompt and the container

   ```
   mysql> exit
   Bye
   bash-4.4$ exit
   exit
   ```

7. We can filter the output from the podman ps command as follows

   ```
   $ podman ps --format "{{.ID}} {{.Image}} {{.Names}}"
   ```

   The output will be something like this:

   ```
   [vagrant@fedora-podman ~]$ podman ps --format "{{.ID}} {{.Image}} {{.Names}}"
   06dbd6d189a5 registry.redhat.io/rhel8/mysql-80:1 mysql-basic
   ```

8. Stop and delete the pod using the name or the ID

   ```
   $ podman stop [ID or NAME]
   $ podman rm [ID or NAME]
   ```

9. Now if you list the pods, no one will be displayed
   ```
   $ podman ps -a
   ```
