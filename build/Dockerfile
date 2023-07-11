FROM php:alpine

ENV PLEX_URL="http://localhost:32400"
ENV PLEX_SECTIONS=all
ENV PLEX_SORT_SKIP_WORDS="a,an,the,el,la"
ENV PLEX_TOKEN=
ENV PLEX_INTERVAL=1d

#Updates everything
RUN apk update && apk add --no-cache git

#Clones git repo (content) into /var/www/html
WORKDIR /app
RUN git clone https://github.com/treyturner/Plex-Export.git . \
    #&& git clone https://github.com/dpDesignz/plex-export-responsive-skin \
    #&& cp -rf plex-export-responsive-skin/* ./ \
    && rm LICENSE README.md

#Copies entrypoint-script for modifying .env-file
COPY entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
