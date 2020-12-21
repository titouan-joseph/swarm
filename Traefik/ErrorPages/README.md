# Server for error pages

 docker run --name test p 8080:80 -v ${}PWD/pages/:/usr/share/nginx/html:ro -d nginx:alpine