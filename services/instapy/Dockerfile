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
# ENV INSTAPY_WORKSPACE="/code/InstaPy/"
ENV INSTAPY_USER="${APP_INSTAPY_USER}"
ENV INSTAPY_PASSWORD="${APP_INSTAPY_PASSWORD}"

WORKDIR /usr/instapy

COPY . .

RUN sed -i "s#deb http://deb.debian.org/debian buster main#deb http://deb.debian.org/debian buster main contrib non-free#g" /etc/apt/sources.list \
	&& apt-get update && apt-get install -y --no-install-recommends \
	wget gcc g++ curl unzip xvfb bzip2 \
	fonts-liberation libappindicator3-1 libasound2 libatk-bridge2.0-0 \
	libnspr4 libnss3 lsb-release xdg-utils libxss1 libdbus-glib-1-2 \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

RUN GECKODRIVER_VERSION=`curl https://github.com/mozilla/geckodriver/releases/latest | grep -Po 'v[0-9]+.[0-9]+.[0-9]+'` && \
    wget https://github.com/mozilla/geckodriver/releases/download/$GECKODRIVER_VERSION/geckodriver-$GECKODRIVER_VERSION-linux64.tar.gz && \
    tar -zxf geckodriver-$GECKODRIVER_VERSION-linux64.tar.gz -C /usr/local/bin && \
    chmod +x /usr/local/bin/geckodriver && \
    rm geckodriver-$GECKODRIVER_VERSION-linux64.tar.gz

RUN FIREFOX_SETUP=firefox-setup.tar.bz2 && \
    # apt-get purge firefox && \
    wget -O $FIREFOX_SETUP "https://download.mozilla.org/?product=firefox-latest&os=linux64" && \
    tar xjf $FIREFOX_SETUP -C /opt/ && \
    ln -s /opt/firefox/firefox /usr/bin/firefox && \
    rm $FIREFOX_SETUP
	
RUN pip3 install -r requirements.txt;

CMD ["python3", "-u", "start.py"]
