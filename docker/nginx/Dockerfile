FROM nginx:1.16

ADD 'ssl/frontend.local+7.pem' /etc/nginx/frontend_server.crt
ADD 'ssl/frontend.local+7-key.pem' /etc/nginx/frontend_server.key
ADD 'ssl/backend.local+7.pem' /etc/nginx/backend_server.crt
ADD 'ssl/backend.local+7-key.pem' /etc/nginx/backend_server.key
ADD project.conf /etc/nginx/conf.d/default.conf
ADD timeout.conf /etc/nginx/conf.d/timeout.conf
