# Libre Shop

A comprehensive Docker-based e-commerce solution with multiple microservices.

## Project Overview

This project consists of the following services:

### Core Services

- **CMS**: Strapi headless CMS for product management (port 5555)
- **Shop**: Vue.js frontend for the e-commerce storefront (port 9999)
- **PDF**: Python service for generating PDF documents (port 1111)
- **Mail**: Python email service for notifications (port 2222)
- **Nginx**: Reverse proxy and static file server (ports 80/443)

### Supporting Services

- **cms-db**: PostgreSQL database for the CMS
- **umami**: Web analytics platform (port 3000)
- **certs**: SSL certificate generation service


## Using Docker Hub Images

All services are available on Docker Hub under the `libreshop` organization:

### PDF Service
```shell
docker run -d -p 1111:1111 -v ./data:/app/data libreshop/pdf:latest
```

The PDF service runs on port 1111 and provides endpoints for document generation.

### Mail Service
```shell
docker run -d -p 2222:2222 \
  -e SMTP_RELAY_HOST=smtp.example.com \
  -e SMTP_RELAY_PORT=587 \
  -e SMTP_RELAY_USERNAME=user@example.com \
  -e SMTP_RELAY_PASSWORD=your_password \
  libreshop/mail:latest
```

The mail service runs on port 2222 and handles email dispatch.

### CMS Service
```shell
docker run -d -p 5555:5555 \
  -e DATABASE_HOST=your-db-host \
  -e DATABASE_PORT=5432 \
  -e DATABASE_NAME=strapi \
  -e DATABASE_USERNAME=strapi \
  -e DATABASE_PASSWORD=your_password \
  -e JWT_SECRET=your_jwt_secret \
  -e ADMIN_JWT_SECRET=your_admin_jwt_secret \
  -e API_TOKEN_SALT=your_token_salt \
  -e APP_KEYS=key1,key2,key3,key4 \
  libreshop/cms:latest
```

The CMS is based on Strapi v4.25.21 and runs on port 5555.

### Shop Frontend
```shell
docker run -d -p 9999:9999 \
  -e VITE_SHOP_API_TOKEN=your_api_token \
  libreshop/shop:latest
```

The shop is built with Vue 3 and runs on port 9999.

