FROM node:10-alpine

ARG APP_SOCKET_ENDPOINT
ARG APP_CONFIG_ENDPOINT
ARG APP_AUTH_ENDPOINT
ARG APP_GA_TRACKING_ID="NA"
ARG APP_PORT="80"

ENV SOCKET_ENDPOINT=${APP_SOCKET_ENDPOINT}
ENV CONFIG_ENDPOINT=${APP_CONFIG_ENDPOINT}
ENV AUTH_ENDPOINT=${APP_AUTH_ENDPOINT}
ENV GA_TRACKING_ID=${APP_GA_TRACKING_ID}
ENV PORT=${APP_PORT}

WORKDIR /site

COPY ../../src/ ./src
COPY ../../package.json .
COPY ../../webpack.common.config.js .
COPY ../../webpack.dev.config.js .
COPY ../../webpack.prod.config.js .
COPY ../../postcss.config.js .

RUN npm install

EXPOSE 80

CMD ["npm", "start"]