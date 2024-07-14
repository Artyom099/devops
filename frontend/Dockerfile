FROM node:20-alpine as  builder

WORKDIR /app

COPY yarn. lock ./

RUN yarn install

COPY .. .

RUN yarn build

FROM nginx:alpine
COPY --from=builder /app/build usr/share/nginx/html
COPY config/nginx.template.conf /etc/nginx/conf.d/default.conf

ARG PORT
ENV PORT=${PORT}

# открываем порт наружу контейнеру
EXPOSE ${PORT}

# nginx -g 'daemon off;' - запускает nginx как сервис
CMD sed -i -e 's/$PORT/'"$PORT"'/g' /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'


# docker run -d -p 3333:3000 devops - запуск контейнера