1. add ./nginx/certs dir in 
2. add ./nginx/dist dir with front build. Change env file in front project (NEED FIX THIS)
3. set your cert names in nginx.conf && configure root path.
4. if self-hosted cert, build new backend image (mkcert example)
bindings/
    /ca-certificates/
        type 
        rootCA.pem

5. Change nginx root domain conf
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

4. set env in .env or system and docker compose up
5. go to identity.${DOMAIN}, change redirect url`s in realms setting to your hostname

