FROM node:10-alpine

ARG APP_SOCKET_ENDPOINT
ARG APP_CONFIG_ENDPOINT
ARG APP_AUTH_ENDPOINT
ARG APP_GA_TRACKING_ID="NA"

ENV ENV_FILE='/site/.env'
ENV PORT=80

WORKDIR /site

COPY ../../src/ ./src
COPY ../../package.json .
COPY ../../webpack.common.config.js .
COPY ../../webpack.dev.config.js .
COPY ../../webpack.docker.config.js .
COPY ../../webpack.prod.config.js .
COPY ../../postcss.config.js .

RUN echo SOCKET_ENDPOINT=${APP_SOCKET_ENDPOINT} >> /site/.env
RUN echo CONFIG_ENDPOINT=${APP_CONFIG_ENDPOINT} >> /site/.env
RUN echo AUTH_ENDPOINT=${APP_AUTH_ENDPOINT} >> /site/.env
RUN echo GA_TRACKING_ID=${APP_GA_TRACKING_ID} >> /site/.env

RUN npm install
EXPOSE 80

CMD ["npm", "run", "start:docker"]