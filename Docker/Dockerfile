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
#           The Curious Technoid      29-Dec-2020    1.1          Added JSON perl module
#
#           The Curious Technoid      19-Apr-2021    2.0          Upgraded the OS to alpine:3.13.5
#                                                                 Upgraded Mojolicious to 9.17 (Waffle)
#                                                                 Added Minion and related DB connectors.
#
#           The Curious Technoid      28-Dec-2021    3.0          Upgraded the OS to alpine:3.15
#                                                                 Upgraded Mojolicious to 9.22 (Waffle)
#
# # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
#

# Using Alphine linux as base image
FROM alpine:3.15
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
RUN cpanm Mojo::mysql LWP::Protocol::https Crypt::Eksblowfish::Bcrypt Mojolicious::Plugin::SecurityHeader JSON Minion Minion::Backend::SQLite Minion::Backend::mysql Minion::Backend::Pg

# Set the working directory to mojolicious directory created above
WORKDIR /var/www/mojolicious

# Run a shell as the default command
CMD ["/bin/sh"]
