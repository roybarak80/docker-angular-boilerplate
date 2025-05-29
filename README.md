# Angular 17 Docker App

This project contains an Angular 17 application that can be built and served using Docker with Nginx.

## 📦 Prerequisites

- [Node.js](https://nodejs.org/) (for local development)
- [Docker](https://www.docker.com/)
- Angular CLI installed globally (for local development):
  ```bash
  npm install -g @angular/cli
  ```

---

## 🚀 Local Development

To run the app locally (outside Docker):

```bash
npm install
ng serve
```

Visit: [http://localhost:4200](http://localhost:4200)

---

## 🐳 Docker Setup

### 1. Build the App with Docker

From the project root (where the Dockerfile is located), run:

```bash
docker build -t angular-docker-app .
```

> 🔁 Make sure to update `angular-docker-app` in the Dockerfile with the actual project name from `angular.json`.

### 2. Run the Docker Container

```bash
docker run -d -p 80:80 angular-docker-app
```

Visit: [http://localhost](http://localhost)

---

## 🛠 Project Structure

```
angular-docker-app/
├── src/
├── dist/
├── Dockerfile
├── nginx.conf
├── package.json
└── angular.json
```

---

## 🔧 Custom Nginx Config (Optional)

If you want Angular routing to work (e.g., deep linking), include this file as `nginx.conf`:

```nginx
server {
  listen 80;
  server_name localhost;

  root /usr/share/nginx/html;
  index index.html;

  location / {
    try_files $uri $uri/ /index.html;
  }
}
```

And make sure your Dockerfile contains:

```dockerfile
COPY nginx.conf /etc/nginx/conf.d/default.conf
```

---

## ✅ Final Notes

- This setup uses a **multi-stage build** for minimal image size.
- The Angular app is served using **Nginx** in the final container.
- Use `--project your-app-name` if you have multiple Angular projects.

---

## 🧼 Clean Up

To stop and remove the container:

```bash
docker ps
docker stop <container_id>
docker rm <container_id>
```

To remove the image:

```bash
docker rmi angular-docker-app
```

---

## 📄 License

MIT