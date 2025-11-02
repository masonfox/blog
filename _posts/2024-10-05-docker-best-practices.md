---
layout: post
title: "Docker Best Practices for Development"
date: 2024-10-05 16:45:00 -0500
author: Mason Fox
tags: [docker, devops, containers, best-practices]
---

# Docker Best Practices for Development

Docker has revolutionized how we develop, ship, and run applications. However, there are some best practices that can make your Docker experience even better. Let's dive in!

## Writing Better Dockerfiles

### 1. Use Official Base Images

Always start with official images from Docker Hub:

```dockerfile
FROM python:3.11-slim
```

These images are:
- Well-maintained
- Regularly updated for security
- Optimized for size

### 2. Minimize Layers

Combine RUN commands to reduce the number of layers:

```dockerfile
# Bad
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y vim

# Good
RUN apt-get update && \
    apt-get install -y curl vim && \
    rm -rf /var/lib/apt/lists/*
```

### 3. Use .dockerignore

Just like `.gitignore`, create a `.dockerignore` file:

```
node_modules
.git
.env
*.log
__pycache__
```

This prevents unnecessary files from being copied into your image.

### 4. Order Matters

Place commands that change less frequently at the top:

```dockerfile
FROM node:18-alpine

# This rarely changes
WORKDIR /app
COPY package*.json ./
RUN npm install

# This changes frequently
COPY . .

CMD ["npm", "start"]
```

## Multi-Stage Builds

Multi-stage builds help keep your production images small:

```dockerfile
# Build stage
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Production stage
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY package*.json ./
RUN npm install --production
CMD ["node", "dist/index.js"]
```

This separates build dependencies from runtime dependencies.

## Docker Compose Tips

### Use Environment Variables

Create a `.env` file for your configuration:

```env
DB_HOST=postgres
DB_PORT=5432
DB_NAME=myapp
```

Reference it in `docker-compose.yml`:

```yaml
version: '3.8'

services:
  web:
    build: .
    env_file: .env
    ports:
      - "3000:3000"
    depends_on:
      - db
  
  db:
    image: postgres:15
    env_file: .env
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

### Use Named Volumes

Named volumes are easier to manage and persist data correctly:

```yaml
volumes:
  db_data:
  redis_data:
```

## Security Best Practices

1. **Don't run as root**
   ```dockerfile
   RUN useradd -m appuser
   USER appuser
   ```

2. **Scan for vulnerabilities**
   ```bash
   docker scan myimage:latest
   ```

3. **Use specific versions**
   ```dockerfile
   # Bad
   FROM python:latest
   
   # Good
   FROM python:3.11-slim
   ```

## Development Workflow

### Hot Reloading with Volumes

Mount your source code for development:

```yaml
services:
  web:
    build: .
    volumes:
      - ./src:/app/src
    environment:
      - NODE_ENV=development
```

### Useful Commands

```bash
# View logs
docker-compose logs -f web

# Execute commands in running container
docker-compose exec web sh

# Rebuild after changing Dockerfile
docker-compose up --build

# Clean up everything
docker system prune -a
```

## Performance Tips

1. **Use BuildKit**
   ```bash
   DOCKER_BUILDKIT=1 docker build .
   ```

2. **Cache dependencies**
   ```dockerfile
   # Copy only package files first
   COPY package*.json ./
   RUN npm install
   # Then copy source code
   COPY . .
   ```

3. **Optimize image size**
   - Use alpine variants when possible
   - Remove build dependencies after installation
   - Squash layers in final image

## Conclusion

Docker is a powerful tool, but using it effectively requires following best practices. These tips will help you create faster, more secure, and more maintainable containers.

What Docker practices do you follow? Share your tips!

---

*Resources:*
- [Docker Documentation](https://docs.docker.com/)
- [Docker Best Practices](https://docs.docker.com/develop/dev-best-practices/)
