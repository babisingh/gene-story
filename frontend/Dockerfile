# Stage 1: Build the React app
FROM node:22-alpine AS builder

ARG HTTP_PROXY
ARG HTTPS_PROXY
ARG NO_PROXY
ENV HTTP_PROXY=$HTTP_PROXY
ENV HTTPS_PROXY=$HTTPS_PROXY
ENV NO_PROXY=$NO_PROXY

WORKDIR /app
COPY package.json .
RUN npm install --strict-ssl=false
COPY . .
RUN npm run build

# Stage 2: Serve with Nginx (tiny, fast static file server)
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
