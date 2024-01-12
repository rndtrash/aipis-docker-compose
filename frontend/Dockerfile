FROM node:lts-slim AS build
COPY ./frontend-time-manager /var/build-frontend
WORKDIR /var/build-frontend
RUN npm install --legacy-peer-deps
ARG VITE_APP_API_AUTH_SERVICE_ADDRESS=http://85.175.194.251:50443/api/auth-service
ARG VITE_APP_API_EVENT_SERVICE_ADDRESS=http://85.175.194.251:50443/api/event-service
RUN npm run build

FROM nginx:latest
RUN mkdir -p /var/frontend
COPY --from=build /var/build-frontend/dist /var/frontend
COPY ./nginx.conf /etc/nginx/nginx.conf
