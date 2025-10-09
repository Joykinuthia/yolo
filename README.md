**Yolo E-Commerce App**

This is a fully containerized full-stack e-commerce platform built with MongoDB, Express (Node.js), and React, orchestrated using Docker and Docker Compose.

**Local Set-up**
To run this project locally on your machine follow these steps :

1. Fork this repository to your GitHub account.

2. Open your terminal.

3. Clone the repository using the SSH URL:

    git clone <your-forked-repo-ssh-url>

4. Navigate into the project directory:

    cd yolo

5. Open the project in VS Code:

    code .

6. Start writing the code as per the requirements

**Base Image Selection**

The Yolo E-Commerce App uses optimized, secure, and minimal Docker base images to ensure fast builds, small image sizes, and better security.

**1. Backend – Node.js Server**

| Stage   | Base Image      | Rationale |
|---------|-----------------|-----------|
| Build   | `node:18-alpine`  | - Lightweight and secure Node.js image<br>- Optimized for faster builds and dependency installation<br>- Includes essential build tools for compiling native modules<br>- Regularly updated with the latest security patches<br>- Ideal for CI/CD and production-ready builds |
| Runtime | `alpine:3.18`     | - Extremely small image size (~5 MB) for faster deployment<br>- Minimal packages reduce the attack surface<br>- Perfect for lightweight applications and microservices<br>- Compatible with multi-stage builds for smaller, cleaner final images<br>- Low memory footprint improves performance and scalability |

**2. Frontend – React Application**

| Stage   | Base Image      | Rationale |
|---------|-----------------|-----------|
| Build   | `node:18-alpine`  | - Efficiently compiles and bundles the React application<br>- Lightweight image that minimizes build container size<br>- Includes necessary tools for dependency installation and optimization |
| Runtime | `nginx:alpine`    | - Serves static React files quickly and reliably<br>- Minimal image size ensures faster startup and deployment<br>- Optimized for high performance and low resource consumption |

**3. Database – MongoDB**

| Container   | Base Image | Rationale |
| ----------- | ---------- | --------- |
| MongoDB | `mongo:6`  | <ul><li>Official and stable MongoDB image</li><li>Supports volume persistence</li><li>Great for local development</li></ul> |


**Dockerfile Breakdown**

The application uses multi-stage builds to separate build and runtime stages, keeping the final image small, fast, and secure.

**Backend – Node.js API (./backend/Dockerfile)**

FROM node:18-alpine AS build

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

FROM alpine:3.18

WORKDIR /app

RUN apk add --no-cache nodejs

COPY --from=build /usr/src/app /app

ENV NODE_ENV=production
ENV PORT=5000

EXPOSE 5000

CMD ["node", "server.js"]

