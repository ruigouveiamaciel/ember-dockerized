FROM node:12

RUN apt-get update && apt-get install -y jq unzip netcat

VOLUME /app
WORKDIR /app
EXPOSE 3000

# Entrypoint and Caddyfile
COPY discord-entrypoint /usr/local/bin/
RUN chmod +x /usr/local/bin/discord-entrypoint
ENTRYPOINT [ "discord-entrypoint" ]
