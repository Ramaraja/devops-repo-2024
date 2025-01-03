
### **1. Getting Started with Docker**
- **Exercise:** Install Docker and run your first container.
  1. Install Docker on your system.
  2. Run the `hello-world` container using `docker run hello-world`.
  3. Inspect the output to understand how Docker works.

---

### **2. Working with Docker Images**
- **Exercise:** Explore Docker Hub and manage images.
  1. Search for an image (e.g., Nginx) on Docker Hub: `docker search nginx`.
  2. Pull the Nginx image: `docker pull nginx`.
  3. List available images: `docker images`.
  4. Remove an image: `docker rmi <image-id>`.

---

### **3. Running Containers**
- **Exercise:** Run a container and explore basic options.
  1. Start an Nginx container: `docker run -d --name my-nginx -p 8080:80 nginx`.
  2. Check running containers: `docker ps`.
  3. Stop and restart the container: `docker stop my-nginx`, `docker start my-nginx`.
  4. Remove the container: `docker rm my-nginx`.

---

### **4. Building Custom Images**
- **Exercise:** Create a custom Docker image.
  1. Create a `Dockerfile` for a simple Python application:
     ```Dockerfile
     FROM python:3.9
     COPY app.py /app.py
     CMD ["python", "/app.py"]
     ```
  2. Write the `app.py` script:
     ```python
     print("Hello, Docker!")
     ```
  3. Build the image: `docker build -t my-python-app .`.
  4. Run the container: `docker run my-python-app`.

---

### **5. Managing Volumes**
- **Exercise:** Use Docker volumes to persist data.
  1. Create a volume: `docker volume create my-volume`.
  2. Run a MySQL container with the volume:
     ```bash
     docker run -d --name my-mysql -e MYSQL_ROOT_PASSWORD=root -v my-volume:/var/lib/mysql mysql
     ```
  3. Inspect the volume: `docker volume inspect my-volume`.
  4. Remove the container and verify the volume persists.

---

### **6. Networking with Docker**
- **Exercise:** Create a custom network and connect containers.
  1. Create a custom network: `docker network create my-network`.
  2. Run two containers on the same network:
     ```bash
     docker run -d --name web1 --network my-network nginx
     docker run -d --name web2 --network my-network nginx
     ```
  3. Use `docker exec` to test connectivity between the containers:
     ```bash
     docker exec -it web1 ping web2
     ```

---
### **7. Custom Image creation**
### **Container Creation**
1. **Run a Container from a Public Image:**
   ```bash
   docker run -d --name my-nginx -p 8080:80 nginx
   ```
   - This runs an Nginx container in detached mode.
   - `-p 8080:80` maps port 8080 on your host to port 80 in the container.

2. **Verify the Container is Running:**
   ```bash
   docker ps
   ```

3. **Access the Container’s Service:**
   - Open a browser and visit `http://localhost:8080` to see the default Nginx page.

4. **Stop the Container:**
   ```bash
   docker stop my-nginx
   ```

5. **Remove the Container:**
   ```bash
   docker rm my-nginx
   ```


### **Create a Custom Docker Image**
1. **Create a Custom HTML File:**
   - Create a directory and navigate into it:
     ```bash
     mkdir custom-nginx && cd custom-nginx
     ```
   - Create an `index.html` file:
     ```html
     echo "<h1>Welcome to My Custom Nginx</h1>" > index.html
     ```

2. **Write a Dockerfile:**
   - Create a `Dockerfile` in the same directory:
     ```Dockerfile
     FROM nginx
     COPY index.html /usr/share/nginx/html/index.html
     ```

3. **Build the Docker Image:**
   ```bash
   docker build -t my-nginx-image .
   ```

4. **Verify the Image:**
   ```bash
   docker images
   ```

5. **Run a Container from the Custom Image:**
   ```bash
   docker run -d --name custom-nginx -p 8080:80 my-nginx-image
   ```

6. **Access the Custom Page:**
   - Visit `http://localhost:8080` in your browser to see the custom HTML page.


### **Push the Image to Docker Hub**
1. **Log in to Docker Hub:**
   ```bash
   docker login
   ```
   - Enter your Docker Hub username and password.

2. **Tag the Image for Docker Hub:**
   ```bash
   docker tag my-nginx-image <your-dockerhub-username>/my-nginx-image:1.0
   ```

3. **Push the Image to Docker Hub:**
   ```bash
   docker push <your-dockerhub-username>/my-nginx-image:1.0
   ```

4. **Verify the Image on Docker Hub:**
   - Log in to your Docker Hub account and check the repository to see the uploaded image.


### **Pull and Run the Pushed Image**
1. **Pull the Image from Docker Hub:**
   ```bash
   docker pull <your-dockerhub-username>/my-nginx-image:1.0
   ```

2. **Run the Pulled Image:**
   ```bash
   docker run -d --name pulled-nginx -p 8081:80 <your-dockerhub-username>/my-nginx-image:1.0
   ```

3. **Access the Running Container:**
   - Visit `http://localhost:8081` to confirm the custom HTML page is served.

---

### **8. Multi-Container Applications with Docker Compose**
- **Exercise:** Deploy a web application with Docker Compose.
  1. Create a `docker-compose.yml` file for a simple WordPress setup:
     ```yaml
     version: '3.7'
     services:
       db:
         image: mysql:5.7
         environment:
           MYSQL_ROOT_PASSWORD: root
           MYSQL_DATABASE: wordpress
       wordpress:
         image: wordpress
         ports:
           - "8080:80"
         environment:
           WORDPRESS_DB_HOST: db
           WORDPRESS_DB_PASSWORD: root
     ```
  2. Start the application: `docker-compose up`.
  3. Access the WordPress site at `http://localhost:8080`.

---

### **9. Inspecting and Debugging Containers**
- **Exercise:** Use Docker commands to inspect and debug.
  1. Inspect a container’s metadata: `docker inspect <container-id>`.
  2. Check container logs: `docker logs <container-id>`.
  3. Access a running container’s shell: `docker exec -it <container-id> bash`.

---

### **10. Scaling with Docker Compose**
- **Exercise:** Scale a service using Docker Compose.
  1. Modify the `docker-compose.yml` file to add `replicas`.
  2. Scale up a service: `docker-compose up --scale web=3`.
  3. Verify running containers: `docker ps`.

---

### **11. Deploying with Docker Swarm**
- **Exercise:** Set up and manage a Docker Swarm cluster.
  1. Initialize a Docker Swarm: `docker swarm init`.
  2. Deploy a service to the swarm:
     ```bash
     docker service create --name web-service -p 8080:80 nginx
     ```
  3. Scale the service: `docker service scale web-service=5`.
  4. Check the service status: `docker service ls`.

---

### **12. Docker Security**
- **Exercise:** Explore security features in Docker.
  1. Scan a Docker image for vulnerabilities: `docker scan <image-name>`.
  2. Run a container with limited permissions: `docker run --read-only nginx`.
  3. Configure secrets management using `docker secret`.

---