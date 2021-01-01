FROM python:3.7-slim-buster

ARG APP_AUTH_ENDPOINT
ARG APP_CONFIG_ENDPOINT
ARG APP_SOCKET_ENDPOINT
ARG APP_INSTAPY_USER
ARG APP_INSTAPY_PASSWORD
ARG APP_IGPASSWORD
ARG APP_IDENT="wickry1"

ENV AUTH_ENDPOINT=${APP_AUTH_ENDPOINT}
ENV CONFIG_ENDPOINT=${APP_CONFIG_ENDPOINT}
ENV SOCKET_ENDPOINT=${APP_SOCKET_ENDPOINT}
ENV IDENT=${APP_IDENT}
ENV INSTAPY_WORKSPACE="/code/InstaPy/"
ENV INSTAPY_USER="${APP_IGUSERNAME}"
ENV INSTAPY_PASSWORD="${APP_IGPASSWORD}"

WORKDIR /usr/instapy

COPY . .

RUN sed -i "s#deb http://deb.debian.org/debian buster main#deb http://deb.debian.org/debian buster main contrib non-free#g" /etc/apt/sources.list \
	&& apt-get update && apt-get install -y --no-install-recommends \
	wget gcc g++ \
	firefox-esr \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*
	
RUN pip3 install -r requirements.txt;

CMD ["python3", "-u", "start.py"]
