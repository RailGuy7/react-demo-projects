FROM node:16.8-alpine3.13 as builder
COPY . /dmachine/
WORKDIR /dmachine
RUN npm config set fetch-retry-mintimeout 20000
RUN npm config set fetch-retry-maxtimeout 120000
RUN npm install
RUN npm run build

FROM nginx:alpine3.20-slim
COPY --from=builder /dmachine/build /usr/share/nginx/html/
EXPOSE 8084
