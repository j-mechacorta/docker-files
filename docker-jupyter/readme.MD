# create the container
#
#
```bash
$ podman run -d --name jupy1 -p 8080:8888 -p 4040:4040 -v /home/papalanis/Nextcloud/papas-stuff/framework-working-directory/docker/jupyterlab/workspace:/workspace:z localhost/jupy-fed39:latest

> podman run -d --name jupy1 -p 8082:8888 -p 4040:4040 -v /home/papalanis/Nextcloud/papas-stuff/framework-working-directory/docker/jupyterlab/workspace:/workspace:z -v /tmp/datalake:/tmp/datalake:z localhost/jupy-fed39:20240812

```
