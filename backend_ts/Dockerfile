FROM node:lts-slim
WORKDIR /var/backend-ts
COPY backend-time-manager .
RUN npm install
RUN npm run build
CMD ["npm", "run", "start:prod"]
