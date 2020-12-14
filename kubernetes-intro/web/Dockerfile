FROM nginx:1.18.0-alpine

COPY nginx-default.conf /etc/nginx/conf.d/default.conf

RUN addgroup -g 1001 appuser \
    && adduser -u 1001 -G appuser -s /bin/sh -D appuser \
    && rm -f /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh \
    && chown -R appuser:appuser /run \
    && chown -R appuser:appuser /var/cache/nginx

COPY ./app /app/

USER appuser

CMD ["nginx", "-g", "daemon off;"]
