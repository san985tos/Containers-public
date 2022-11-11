# A quick http application

## Instructions

1. Create the following container

```
podman run -d -p 8080:80 --name httpd-basic quay.io/redhattraining/httpd-parent:2.4
```

2. Check conatiner is running

```
podman ps
```

3. Open a browser and navegate to localhost:8080
4. Curl can be used as well

```
curl http://localhost:8080
```

5. An output example:

```
[vagrant@fedora-podman ~]$ curl http://localhost:8080
Hello from the httpd-parent container!
[vagrant@fedora-podman ~]$
```

6. modify the index.html

```
podman exec -it httpd-basic /bin/bash
echo "hola mundo**" > /var/www/html/index.html
```

7. Run curl command once again:

```
curl http://localhost:8080
```

8. An output example:

```
[vagrant@fedora-podman ~]$ curl http://localhost:8080
hola mundo**
[vagrant@fedora-podman ~]$
```
