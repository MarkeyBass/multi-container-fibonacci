# BUILD PHASE
FROM node:16-alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

# RUN PHASE
FROM nginx
EXPOSE 3000
# copying from the local filesystem
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# copying from the builder, temporary build phase, to the current and final run phase
COPY --from=builder /app/build /usr/share/nginx/html