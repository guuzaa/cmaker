FROM mcr.microsoft.com/devcontainers/cpp:1-ubuntu-22.04

# Optionally install the cmake for vcpkg
COPY ./package.sh /tmp/

RUN chmod +x /tmp/package.sh \
    && /tmp/package.sh \
    && rm -f /tmp/package.sh

# [Optional] Uncomment this section to install additional vcpkg ports.
# RUN su vscode -c "${VCPKG_ROOT}/vcpkg install <your-port-name-here>"

# [Optional] Uncomment this section to install additional packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
