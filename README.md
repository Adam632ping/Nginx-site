Чтобы создать контейнер NGINX с веб-сайтом по умолчанию, выполните следующую команду:
docker run -p 8080:80 nginx# Nginx-site

Сохраните следующий HTML-код в файл с именем index.html:

<html>
    <body>
        Hello from DockerHosting!
    </body>
</html>
Затем выполните следующую команду, чтобы смонтировать текущий каталог под /usr/share/nginx/html внутри контейнера NGINX с доступом только для чтения:

docker run -v $(pwd):/usr/share/nginx/html:ro -p 8080:80 nginx

nano docker-compose.yml
services:
  nginx:
    image: lscr.io/linuxserver/nginx:latest
    container_name: nginx
    environment:
      - PUID=1000
      - PGID=1000
    volumes:
      - /path/to/nginx/config:/config
    ports:
      - 8080:80
    restart: unless-stopped
nginx.conf
server{
        listen 80;
        server_name _;

        location / {
                root /srv;
        }
}

404.html
server {
    listen 80 default_server;



    . . .

    error_page 404 /custom_404.html;
    location = /custom_404.html {
        root /usr/share/nginx/html;
        internal;
    }
}

    
