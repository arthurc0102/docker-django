FROM alpine:3.7

# Change working directory
WORKDIR /usr/src/app

# Posts
EXPOSE 8000

# Install packages
RUN apk add --no-cache \
  python3 \
  python3-dev \
  linux-headers \
  gcc \
  musl-dev \
  mariadb-dev

# Update all packages
ONBUILD RUN apk upgrade --no-cache

# Update pip and setuptools
ONBUILD RUN pip3 install --upgrade --no-cache-dir pip setuptools uwsgi

# Copy Djnago project to working directory
ONBUILD COPY . .

# Install python packages
ONBUILD RUN pip3 install --no-cache-dir -r requirements.txt
