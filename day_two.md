# How to build a docker image
## As last step of day one we have deploy an static website by docker command, today I will try to build my own image to easy deploy step.
```
$ docker run --name static-web -p 8080:80 -v ~/workspaces/docker-learn-by-doing/static:/usr/share/nginx/html:ro -d nginx:stable-alpine
```

## Create docker image base on nginx:stable-alpine
Create `Dockerfile` with content
```
FROM nginx:stable-alpine
LABEL maintainer="ledinhchung.it@gmail.com"
```
Build docker image from `Dockerfile`
```
$ docker build -t static-image:dev dockerizing/day_two
```
- `docker build`
- `-t static-image:dev` is telling that we want to build a imange name `static-web` and tag is `dev`
- `dockerizing/day_two` is the directory of `Dockerfile`

List all image to confirm is the exist the image we just build.
```
$ docker images
```

## Now how can we deploy static contain to our custome image on build.
Now we update the `Dockerfile` by adding
```
COPY static/ /usr/share/nginx/html
```
This will copy all content inside folder `static` to `/usr/share/nginx/html` the root web directory of nginx.

### Now rebuild docker image
```
docker build -t static-image:dev dockerizing/day_two
```

## Run docker by custom image we just build.
```
$ docker run -d --name static-web -p 8080:80 static-image:dev
```

Confirm is anything run the same as the day one by enter `localhost:8080` to browser.

## Final `Dockerfile`
```
FROM nginx:stable-alpine
LABEL maintainer="ledinhchung.it@gmail.com"

COPY static/ /usr/share/nginx/html
```