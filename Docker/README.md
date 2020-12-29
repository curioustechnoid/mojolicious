
This docker image has all the tools and libraries required to run Mojolicious Web Framework. You can read more about Mojolicious [here](https://www.mojolicious.org).

This uses alpine linux as base image, hence the small size. The default command for this image is a shell(/bin/sh).

# Included Modules in the image

* Mojo::mysql
* LWP::Protocol::https
* Crypt::Eksblowfish::Bcrypt
* Mojolicious::Plugin::SecurityHeader
* JSON


# Supported tags and respective Dockerfile links

* [1.1, 1.0, latest](https://github.com/curioustechnoid/mojolicious/blob/main/Docker/Dockerfile)


# How to use this image


1. Create your mojolicious project using:

    `mojo generate app mojoproject`

2. Run it in docker:

   #### Method 1: Manual

* Create your own Dockerfile for your project, you can use [this sample file](https://github.com/curioustechnoid/mojolicious/blob/main/Docker/sample/Dockerfile). Once the dockerfile is created run the below commands:

    `docker build -t myprojectimage .`

   Then run the your docker image using:

    `docker run --rm --name mojoproject -p 3000:3000 myprojectimage morbo script/mojoproject`

   #### Method 2: Using Compose

* Create your own docker-compose file to build and run your application, you can use [this sample file](https://github.com/curioustechnoid/mojolicious/blob/main/Docker/sample/docker-compose.yml). First create the [Dockerfile](https://github.com/curioustechnoid/mojolicious/blob/main/Docker/sample/Dockerfile) using the Method 1 and then create docker-compose, after which run the below command:

```
    docker-compose up
    docker-compose down
    docker-compose up -d
```


# Source

The source of this image on [GitHub](https://github.com/curioustechnoid/mojolicious/blob/main/Docker).

