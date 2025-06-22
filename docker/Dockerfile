# Start with a minimal base with OpenJDK (required by Facto)
ARG ASSET_FILENAME
FROM openjdk:11-slim

# Metadata
LABEL description="Docker image for Facto using prebuilt binaries"

RUN mkdir /opt/facto-install && \
    mkdir /opt/facto && \
    mkdir /opt/facto/conf

# Install dependencies
RUN apt-get update && \
    apt-get install -y tar bash sed perl default-mysql-client && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Default working directory
WORKDIR /opt/facto

# Setup facto from release assets
COPY release-assets/${ASSET_FILENAME} ./release.tar.gz
RUN tar xzf release.tar.gz -C /opt/facto-install && \
    cp -r /opt/facto-install/bin /opt/facto/ && \
    cp -r /opt/facto-install/lib /opt/facto/

# Expose the default Facto port
EXPOSE 9000

COPY docker/entrypoint.sh entrypoint.sh
RUN chmod +x entrypoint.sh

ENTRYPOINT ["/opt/facto/entrypoint.sh"]
