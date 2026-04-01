# Dockerfile pour le front-end VitalSync
# Sert le fichier static index.html via Nginx
# Cette image copie le site statique et configure Nginx

FROM nginx:alpine

COPY nginx.conf /etc/nginx/nginx.conf

COPY . /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]