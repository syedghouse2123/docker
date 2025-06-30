
## 🚀 What it Does

- Uses Jenkins pipeline to:
  - Checkout code from GitHub
  - Build a Docker image with Nginx serving `index.html`
  - Tag and push the image to Docker Hub

## 🐳 Docker Image

- **Base Image:** `nginx:latest`
- **Final Image:** `syedghouse21/docker-demo:v1` (example)

## 📦 How to Run

```bash
docker run -d -p 8080:80 syedghouse21/docker-demo:v1
