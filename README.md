1. add /certs dir 
2. add /dist dir with front build
3. set your cert names in nginx.conf && configure root path

if prod: 

        location / {
            try_files $uri $uri/ /index.html;
        }
if dev:

		location / {
            proxy_pass http://host.docker.internal:5173;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-Proto https;
            proxy_set_header X-Forwarded-For $remote_addr;
        }

4. docker compose up
5. go to https://HOSTNAME//identity, change redirect url`s in realms setting to your hostname
