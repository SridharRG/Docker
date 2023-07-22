# DOCKER

### Explanation and Purpose:

- The Dockerfile is used to create a custom Docker image for your Nginx web server. It starts with the official Nginx base image, copies your index.html file into the container, and sets up the web server to serve the HTML content.

- The docker-compose.yml file is used to define and manage the Docker containers for your application. It specifies that there is one service, named "web," which is built from the current directory (where the Dockerfile is located). The ports configuration allows you to access the Nginx web server running inside the container from your host machine.

- By using Docker and docker-compose, you can easily package your web server and its required files into a container, making it portable and reproducible across different environments. Docker containers provide isolation, allowing you to run your application consistently, regardless of the underlying host system's configuration.

**1. Dockerfile:**
```Dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
```

- `FROM nginx:alpine`: This line specifies the base image for our Docker container. Here, we are using the official Nginx image that is built on Alpine Linux. Alpine is a lightweight Linux distribution, making it a popular choice for Docker images due to its small size.

- `COPY . /usr/share/nginx/html`: This line copies the contents of the current directory (where the Dockerfile is located) into the `/usr/share/nginx/html` directory inside the container. In this case, you would typically have an `index.html` file in the current directory, which will be copied to the Nginx HTML root directory. This means that the static files needed to serve your website will be copied into the Nginx web server's document root.

**2. docker-compose.yml:**
```yaml
services:
  web:
    build: .
    ports:
      - "80:80"
```

- `services`: This section defines the services (containers) that make up your application.

- `web`: This is the name of the service, and it represents the Nginx container that we'll be creating based on the Dockerfile.

- `build: .`: This tells `docker-compose` to build the Docker image for the service using the current directory (where the Dockerfile is located) as the build context. It means it will use the Dockerfile to create the image for the Nginx container.

- `ports: - "80:80"`: This line maps the host machine's port 80 to the container's port 80. It allows you to access the Nginx web server running inside the container from your host machine's browser. The format is `"host_port:container_port"`, and in this case, it allows you to access the web server using `http://localhost` or `http://<your_host_ip>`.

**3. index.html:**
This is your actual HTML file, which will be served by the Nginx web server. It can contain the content you want to display on your website.


When you run `docker-compose build` and `docker-compose up`, it will build the Docker image based on the Dockerfile and start the Nginx container with the specified port mapping. As a result, you should be able to access your website by visiting `http://localhost` or `http://<your_host_ip>` in your web browser.
