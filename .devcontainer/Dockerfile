
FROM mcr.microsoft.com/vscode/devcontainers/python:0-3.10

ENV PYTHONUNBUFFERED 1
ENV NODE_EXTRA_CA_CERTS /etc/ssl/certs/ca-certificates.crt

WORKDIR /workspace

# Update args in docker-compose.yaml to set the UID/GID of the "vscode" user.
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN if [ "$USER_GID" != "1000" ] || [ "$USER_UID" != "1000" ]; then groupmod --gid $USER_GID vscode && usermod --uid $USER_UID --gid $USER_GID vscode; fi

#COPY [".devcontainer/extra_CA/*crt", "/usr/local/share/ca-certificates/"]
#RUN update-ca-certificates



RUN apt-get update && apt-get install -y  lsb-release postgresql-client


# [Optional] If your requirements rarely change, uncomment this section to add them to the image.
COPY requirements.txt /tmp/pip-tmp/

RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
    && rm -rf /tmp/pip-tmp

COPY requirements-dev.txt /tmp/pip-tmp/

RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements-dev.txt \
    && rm -rf /tmp/pip-tmp
