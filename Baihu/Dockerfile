FROM ghcr.io/engigu/baihu:latest

ENV REMOTE_FOLDER="huggingface:/baihu"

RUN apt-get update && apt-get install -y \
    jq \
    xvfb \
    curl \
    unzip \
    sshpass \
    openssh-client \
    && curl -fsSL https://rclone.org/install.sh | bash \
    && rclone version \
    && ssh -V \
    && sshpass -V \
    && rm -rf /var/lib/apt/lists/*

RUN rclone config -h

COPY ./restore.sh /

RUN sed -i '/^exec baihu server$/d' /app/docker-entrypoint.sh
RUN cat /restore.sh >> /app/docker-entrypoint.sh

RUN mise exec python@3.13.12 -- pip install requests
RUN mise use -g python@3.13.12
RUN mise use -g node@23.11.1
