#
# # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
#
# AUTHOR  :  The Curious Technoid
# DATE    :  28-Dec-2020
# PURPOSE :
#       This Docker File is used to generate a docker image with all the necessarry components
# required for Mojolicious Framework. It also includes modules required to connect to MySQL / 
# MariaDB database.
#
#       This image is published in docker hub with handle: curioustechnoid/mojolicious
#
# USAGE:
#           docker build -t mojolicious .
#
# UPDATES:
#           AUTHOR                    DATE           VERSION      COMMENTS
#           The Curious Technoid      28-Dec-2020    1.0          Initial Version
#
#
# # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
#

# Using Alphine linux as base image
FROM alpine:3.12.3
MAINTAINER The Curious Technoid <thecurioustechnoid@gmail.com>

# Expose all default Mojolicious Ports
EXPOSE 8080 3000

# Create apache group and user
RUN addgroup -S apache && adduser -S apache -G apache

# Creating mojolicious directory for storing the src files
RUN mkdir -p /var/www/mojolicious \
    && chmod -R 755 /var/www/mojolicious \
    && chown -R apache:apache /var/www/mojolicious

# Install all necessary packages required by Mojolicious
RUN apk update && apk add --no-cache curl make gcc perl-app-cpanminus perl-dbd-mysql perl-net-ssleay perl-dev musl-dev

# For getting the latest wget
RUN apk update && apk add ca-certificates && update-ca-certificates && apk add wget

# Install Mojolicious
RUN curl -L https://cpanmin.us | perl - -M https://cpan.metacpan.org -n Mojolicious

# Install popular Perl Modules required for webdevelopment 
RUN cpanm Mojo::mysql LWP::Protocol::https Crypt::Eksblowfish::Bcrypt Mojolicious::Plugin::SecurityHeader

# Set the working directory to mojolicious directory created above
WORKDIR /var/www/mojolicious

# Run a shell as the default command
CMD ["/bin/sh"]
