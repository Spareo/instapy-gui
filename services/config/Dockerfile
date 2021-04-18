FROM python:3-alpine

ARG APP_MODE="development"
ARG APP_MONGO_URL
ARG APP_JWT_SECRET
ARG APP_CIPHER_SECRET

ENV MODE=${APP_MODE}
ENV MONGO_URL="${APP_MONGO_URL}"
ENV JWT_SECRET="${APP_JWT_SECRET}"
ENV CIPHER_SECRET "${APP_CIPHER_SECRET}"

WORKDIR /usr/instapy

COPY . .

RUN apk add --update --no-cache --virtual .build-dependencies \
  gcc g++ \
  musl-dev \
  libffi-dev \
  openssl-dev \
  python3-dev \
  cargo \
  && python -m pip install -r requirements.txt \
  && apk del .build-dependencies

EXPOSE 80

CMD ["python3", "-u", "start.py"]
