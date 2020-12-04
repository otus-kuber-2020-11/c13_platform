FROM nginx:alpine

RUN apk update && \
    apk add yarn && \
    rm -f /etc/nginx/conf.d/*

RUN ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log

COPY default.conf /etc/nginx/conf.d/

RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

RUN addgroup -g 1001 node \
    && adduser -u 1001 -G node -s /bin/sh -D node

RUN chown -R node:node /run && \
  chown -R node:node /var/cache/nginx && \
  chown -R nobody.nobody /var/log/nginx

RUN rm -f /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh

USER 1001

CMD ["nginx", "-g", "daemon off;"]
