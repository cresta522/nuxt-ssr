FROM node:16.14.2-alpine
RUN mkdir -p /var/www/nuxt
# timezone
ARG TZ
WORKDIR /var/www/nuxt
COPY ./nuxt/ /var/www/nuxt/

RUN apk update && \
    apk upgrade && \
    apk add --no-cache make gcc g++ python3 && \
    npm install

EXPOSE 3000

ENTRYPOINT ["npm", "run", "dev"]