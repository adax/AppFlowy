FROM oven/bun:latest

WORKDIR /app

RUN apt-get update && \
    apt-get install -y nginx

RUN bun install cheerio pino axios pino-pretty

COPY . .

RUN addgroup --system nginx && \
    adduser --system --no-create-home --disabled-login --ingroup nginx nginx

RUN apt-get clean && rm -rf /var/lib/apt/lists/*


COPY dist/ /usr/share/nginx/html/

COPY nginx.conf /etc/nginx/nginx.conf

COPY nginx-signed.crt /etc/ssl/certs/nginx-signed.crt
COPY nginx-signed.key /etc/ssl/private/nginx-signed.key

RUN chown -R nginx:nginx /etc/ssl/certs/nginx-signed.crt /etc/ssl/private/nginx-signed.key

COPY start.sh /app/start.sh

RUN chmod +x /app/start.sh


EXPOSE 80 443

CMD ["/app/start.sh"]
