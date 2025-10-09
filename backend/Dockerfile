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