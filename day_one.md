# Install Docker
We can install docker in several way but in my case I chose the easy way that is install by convenience shell script.
1. Download the script
```bash
$ curl -fsSL https://get.docker.com -o get-docker.sh
```
2. Run script
```bash
$ sudo sh get-docker.sh
```
3. (Optional) in case I don't wan't to run docker as root
```bash
$ sudo usermod -aG docker $USER
```
# Confirm that docker was install successfully
```
$ docker version
```
At this time I get response that my docker version is 19.03.1

```bash
$ docker run hello-world
```

# Deploy a static website to the docker containter.
This time I will deploy an simple static web on nginx alpine image https://hub.docker.com/_/nginx
```
$ docker run --name static-web -p 8080:80 -v ~/workspaces/docker-learn-by-doing/static:/usr/share/nginx/html:ro -d nginx:stable-alpine
```
- `docker run` is there key work to tell that we want to run an docker container.
- `--name stattic-web` is defined that the new container will have name is `static-web`.
- `-p 8080:80` is to telling that we want to mapping from host machine on port `8080` to container port `80`.
- `-v ~/workspaces/docker-learn-by-doing/static:/usr/share/nginx/html:ro` is we tell docker to mount static folder to container `/usr/share/nginx/html` this is there default root directory web of nginx.
- `-d` is tell that we will detach the container then leave docker run as a background task.
- `nginx:stable-alpine` is defined that we run container by image name `nginx` and tag is `stable-alpine`

Now if you open browser then enter localhost:8080 you will got the message `Welcom to docker`. 


# Reference:
  Install docker for Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/
