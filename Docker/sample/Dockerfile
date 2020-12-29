#
# # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
#
# AUTHOR  :  The Curious Technoid
# DATE    :  28-Dec-2020
# PURPOSE :
#       This Docker File is used to create image for your project using curioustechnoid/mojolicious image.
#
# USAGE:
#           docker build -t myprojectimage .
#
# UPDATES:
#           AUTHOR                    DATE           VERSION      COMMENTS
#           The Curious Technoid      28-Dec-2020    1.0          Initial Version
#
#
# # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
#

# Use the mojolicious image as base image
FROM curioustechnoid/mojolicious:latest

# Setting the mojo parent directory name where our project resides
# ***** PLACEHOLDER ******
ARG SRC_DIR='mojoproject'

# Push the source files to mojolicious directory
COPY $SRC_DIR/ .

# Setting the correct permissions for all the folders
RUN chmod 755 /var/www/mojolicious \
    && chown -R apache:apache /var/www/mojolicious \
    && find /var/www/mojolicious/ -type d -exec chmod 755 {} \; \
    && find /var/www/mojolicious/ -type f -name *.* -exec chmod 644 {} \; \
    && find /var/www/mojolicious/public/ -type f -name *.* -exec chmod 444 {} \; \
    && chmod 744 /var/www/mojolicious/script/$SRC_DIR

# You can install any additional perl modules that you want, if required
# RUN cpanm Passwords

# Tell docker that all future commands should run as the appuser user
USER apache

CMD ["/bin/sh", "-c"]


