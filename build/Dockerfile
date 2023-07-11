FROM php:alpine

ENV PLEX_URL="http://localhost:32400"
ENV PLEX_SECTIONS=all
ENV PLEX_SORT_SKIP_WORDS="a,an,the,el,la"
ENV PLEX_TOKEN=
ENV PLEX_INTERVAL=1d

# Updates everything
RUN apk update && apk add --no-cache git

# Clones git repo (content) into /var/www/html
WORKDIR /app
RUN git clone https://github.com/treyturner/Plex-Export.git . && \
    git clone https://github.com/dpDesignz/plex-export-responsive-skin && \
    cp -rf plex-export-responsive-skin/* ./ && \
    rm LICENSE README.md && \
    # Enable dark skin and JS rewrite
    /bin/sed -i '/<!-- <link rel="stylesheet" href="assets\/css\/darkmode.css" \/> -->/ s|<!-- ||' index.html && \
    /bin/sed -i '/<link rel="stylesheet" href="assets\/css\/darkmode.css" \/> -->/ s| -->||' index.html && \
    /bin/sed -i '/<script src="assets\/js\/jquery.1.4.4.min.js"><\/script>/ s|<script src="assets\/js\/jquery.1.4.4.min.js"><\/script>|<!-- <script src="assets\/js\/jquery.1.4.4.min.js"><\/script> -->|' index.html && \
    /bin/sed -i '/<script src="assets\/js\/plex.js"><\/script>/ s|<script src="assets\/js\/plex.js"><\/script>|<!-- <script src="assets\/js\/plex.js"><\/script> -->|' index.html && \
    /bin/sed -i '/<!-- <script src="assets\/js\/vanilla-plex.js"><\/script> -->/ s|<!-- ||' index.html && \
    /bin/sed -i '/<script src="assets\/js\/vanilla-plex.js"><\/script> -->/ s| -->||' index.html

#Copies entrypoint-script for modifying .env-file
COPY entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
