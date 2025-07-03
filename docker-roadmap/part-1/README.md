# Docker Roadmap: Dockerfile Guide and Comparison

This guide explains the Dockerfile found in `1-simple-app`, breaking down each instruction and showing how to use it. It also compares it to the more minimal Dockerfile in `3-solution-2` to help you understand the impact of different base images.

---

## 1. `1-simple-app/Dockerfile` (Step-by-Step Explanation)

### 1. Base Image
```dockerfile
FROM node:20
```
- **What it does:** Uses the official Node.js 20 image as the starting point for your container. This image is based on Debian/Ubuntu, so it includes many system utilities and libraries.

### 2. Set Working Directory
```dockerfile
WORKDIR /usr/src/app
```
- **What it does:** Sets the working directory inside the container. All subsequent commands will run from this directory.

### 3. Copy Application Files
```dockerfile
COPY . .
```
- **What it does:** Copies all files from your project directory into the container's working directory.

### 4. Install Dependencies
```dockerfile
RUN npm install
```
- **What it does:** Installs all Node.js dependencies listed in your `package.json`.

### 5. Expose Port
```dockerfile
EXPOSE 3000
```
- **What it does:** Informs Docker that the app will listen on port 3000.

### 6. Start the Application
```dockerfile
CMD ["node", "index.js"]
```
- **What it does:** Sets the default command to run your app using Node.js when the container starts.

---

### How to Build and Run

**Build the Docker image:**
```sh
docker build . -t test-app
```

**Run the Docker container:**
```sh
docker run -p 3000:3000 test-app
```
This start the container and map the port 3000 to the container.

---

## Comparison: `1-simple-app` vs `3-solution-2`

- The `3-solution-2/Dockerfile` uses this as its main difference:
  ```dockerfile
  FROM mhart/alpine-node
  ```
  - This uses an Alpine Linux-based Node.js image, which is much smaller and more efficient than the Debian/Ubuntu-based `node:20` used in `1-simple-app`.
  - The rest of the steps (WORKDIR, COPY, RUN, EXPOSE, CMD) are the same as in `1-simple-app`.
- **Result:**
  - The image built from `3-solution-2` is much smaller in size, making it faster to download and deploy.
  - Use Alpine-based images for production when you want minimal size, unless you need extra system utilities or libraries only available in larger images.

### Reference: Actual Image Sizes

Below is a real output from `docker images` showing the difference in image sizes:

```sh
REPOSITORY        TAG       IMAGE ID       CREATED          SIZE
alpine_test_app   latest    9e6e11cf034d   30 seconds ago   169MB
test_app          latest    e0667b8006d6   4 hours ago      1.59GB
mongo             latest    5941949d3887   5 days ago       1.21GB
postgres          latest    6cf6142afacf   3 weeks ago      621MB
hello-world       latest    940c619fbd41   5 months ago     20.4kB
ubuntu            16.04     1f1a2d56de1d   3 years ago      195MB
```
- `alpine_test_app` (from 3-solution-2): **169MB**
- `test_app` (from 1-simple-app): **1.59GB**

This demonstrates how much smaller the Alpine-based image is compared to the standard Node image.

---

## Additional Useful Docker Commands

```sh
# Log in to Docker Hub
docker login

# Push an image to Docker Hub
docker push <tag_name>

# Pull an image from Docker Hub
docker pull <tag_name>
```

---

> **Tip:** Use Alpine-based images for smaller, faster containers in production, unless you need specific tools or libraries only available in larger images. 