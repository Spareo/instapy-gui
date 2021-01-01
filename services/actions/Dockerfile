FROM python:3-alpine

ARG APP_MONGO_URL

ENV MONGO_URL="${APP_MONGO_URL}"

WORKDIR /usr/instapy

COPY . .

RUN apk add --update --no-cache --virtual .build-dependencies \
  alpine-sdk \
	gcc \
	musl-dev \
	libffi-dev \
  openssl-dev \
  && pip3 install -r requirements.txt \
  && apk del .build-dependencies

CMD ["python3", "-u", "main.py"]