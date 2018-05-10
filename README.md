# Docker Django

> Build a Django Docker image

> Only Python3!!!  
> Only Python3!!!  
> Only Python3!!!


## Version

- MySQL ([Dockerfile](./mysql/Dockerfile))
- PostgreSQL ([Dockerfile](./postgresql/Dockerfile))


## Use

For MySQL version, your Dockerfile:
```dockerfile
FROM arthurc0102/django:mysql

RUN pip3 install --no-cache-dir -r requirements.txt
```

For PostgreSQL version, your Dockerfile:
```dockerfile
FROM arthurc0102/django:postgresql

RUN pip3 install --no-cache-dir -r requirements.txt
```

And create your own `uwsgi.ini`

If you need more OS package just install it.
```dockerfile
FROM arthurc0102/django:<tag>

RUN apk add --no-cache <packages>

RUN pip3 install --no-cache-dir -r requirements.txt
```

Finally you can build it `docker build -t <repl>:<tag> .`!

## About

> I will not run `pip3 install --no-cache-dir -r requirements.txt` for you, because you many want to install more os packages before python packages install.


### Install Python packages from `requirements.txt`

**Your `Dockerfile` must run `pip3 install --no-cache-dir -r requirements.txt`!**


### Setting for uwsgi

**Create `uwsgi.ini` in your project if you use default CMD** else skip this step.

This is my `uwsgi.ini` file, you can use this as a template or create your own.
```ini
[uwsgi]
chdir = /usr/src/app
module = core.wsgi

master = true
processes = 4
socket = 0.0.0.0:8000
vacuum = true
optmize = true

req-logger = file:./log/access-@(exec://date +%%Y-%%m-%%d).log
logger = djangoerror file:./log/error-@(exec://date +%%Y-%%m-%%d).log
logger = file:./log/info-@(exec://date +%%Y-%%m-%%d).log
log-route = djangoerror (ERROR:django:.*)
log-reopen = true
```


### Volumes

- `/usr/src/app/log` for logs
- `/usr/src/app/media` for media
- `/usr/src/app/assets` for static file online

Feel free to add more if you need.


### Ports

- `8000`

Feel free to add more if you need.


### Entrypoint

For default this image will run [docker-entrypoint.sh](../docker-entrypoint.sh) to collect static and migrate database.

If you need more just define your own `ENTRYPOINT` in your Dockerfile.


### Cmd

For default this image run `CMD [ "uwsgi", "--ini", "uwsgi.ini" ]` to start Django app.

If you do not want to start it this way just define your own `CMD` in your Dockerfile.


## Future

- Use pipenv.
