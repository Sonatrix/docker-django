# develop stage
FROM node:12.16.3-alpine as develop-stage
WORKDIR /app
COPY package.json ./
RUN yarn global add @quasar/cli
COPY . .
# build stage
FROM develop-stage as build-stage
RUN npm install
RUN quasar build -m pwa
# production stage
FROM nginx:1.17.5-alpine as production-stage
COPY --from=build-stage /app/dist/pwa /usr/share/nginx/html
COPY nginx/default.conf /etc/nginx/conf.d/default.conf
COPY nginx/default.conf /etc/nginx/sites-available/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
