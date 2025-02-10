## meaning of `build.yml` in CI

![[CI_Pipeline.webp]]

## How to create a CI pipeline?

For Github,

- you can add all your pipelines to `.github/workflows`
- - Add `.github/workflows/build.yml` in the root folder
- Create a workflow

```yml
name: Build on PR

on:
  pull_request:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js
        uses: actions/setup-node@v3
        with:
          node-version: "20"

      - name: Install Dependencies
        run: npm install

      - name: Generate prisma client
        run: npm run db:generate

      - name: Run Build
        run: npm run build
```

## How to create a CD pipeline?
we are going to use docker for containerize our app for CD, then deploy the app on server(EC2 for our case)
1. first write a docker file ([[Dockerfile]])
	-  Make sure to add the `dockerhub` secrets to `github secrets` of the repo (DOCKER_USERNAME, DOCKER_PASSWORD)
2. Create a CD pipeline
	- Clones the repo
	- Builds the docker image
	- Pushes the docker image
```yml
name: Build and Deploy to Docker Hub

on:
  push:
    branches:
      - master

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
    - name: Check Out Repo
      uses: actions/checkout@v2

    - name: Log in to Docker Hub
      uses: docker/login-action@v1
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Build and Push Docker image
      uses: docker/build-push-action@v2
      with:
        context: .
        file: ./docker/Dockerfile.user
        push: true
        tags: 100xdevs/week-18-class:latest  # Replace with your Docker Hub username and repository

    - name: Verify Pushed Image
      run: docker pull 100xdevs/week-18-class:latest  # Replace with your Docker Hub username and repository

# ---- Deploy script ----
    - name: Deploy to EC2
      uses: appleboy/ssh-action@master
      with:
        host: ${{ secrets.SSH_HOST }}
        username: ${{ secrets.SSH_USERNAME }}
        key: ${{ secrets.SSH_KEY }}
        script: |
          sudo docker pull 100xdevs/week-18-class:latest
          sudo docker stop web-app || true
          sudo docker rm web-app || true
          sudo docker run -d --name web-app -p 3005:3000 100xdevs/week-18-class:latest
```
3. Point userapp.your_domain.com to the IP of the server
4. Add nginx reverse proxy to forward requests from userapp.your_domain.com to port on which the app is running
```nginx
server {
        server_name userapp.100xdevs.com;

        location / {
            proxy_pass http://localhost:3005;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;


                # Basic Authentication
                auth_basic "Restricted Content";
                auth_basic_user_file /etc/nginx/.htpasswd;
        }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/userapp.100xdevs.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/userapp.100xdevs.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
```
