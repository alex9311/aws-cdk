# The correct AWS SAM build image based on the runtime of the function will be
# passed as build arg. The default allows to do `docker build .` when testing.
ARG IMAGE=amazon/aws-sam-cli-build-image-nodejs12.x
FROM $IMAGE

# Install yarn
RUN npm install --global yarn@1.22.5

# Install parcel 2 (fix the version since it's still in beta)
# install at "/" so that node_modules will be in the path for /asset-input
ARG PARCEL_VERSION=2.0.0-beta.1
RUN cd / && npm install parcel@$PARCEL_VERSION --no-package-lock

# Ensure all users can write to npm cache
RUN mkdir /tmp/npm-cache && \
    chmod -R 777 /tmp/npm-cache && \
    npm config --global set cache /tmp/npm-cache

# Disable npm update notifications
RUN npm config --global set update-notifier false

# create non root user and change allow execute command for non root user
RUN /sbin/useradd -u 1000 user && chmod 711 /

CMD [ "parcel" ]
