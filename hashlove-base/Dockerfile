FROM ruby:2.6.2
LABEL maintainer "tanukiti1987 <tanukiti1987@gmail.com>"

# シェルスクリプトとしてbashを利用
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# 必要なライブラリインストール
RUN apt-get update -qq \
    && apt-get install -y build-essential libpq-dev curl wget unzip python3-selenium libxml2 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# chromeをインストール
RUN sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN apt-get update -qq \
    && apt-get install -y google-chrome-stable \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# chrome driver をインストール
RUN wget https://chromedriver.storage.googleapis.com/2.31/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip -d ~/bin/

# 日本語フォントをインストール
RUN wget --content-disposition http://ipafont.ipa.go.jp/old/ipafont/IPAfont00303.php -O IPAfont00303.zip
RUN unzip IPAfont00303.zip -d /usr/share/fonts/
RUN fc-cache -fv

# Install Node.js
# https://nodejs.org/en/download/package-manager/
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN apt-get install -y nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Yarn
# https://yarnpkg.com/lang/en/docs/install/
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install jsonnet
RUN git clone https://github.com/google/jsonnet.git
RUN cd jsonnet && make libjsonnet.so
RUN cp jsonnet/libjsonnet.so /usr/local/lib/libjsonnet.so
RUN cp jsonnet/include/libjsonnet.h /usr/local/include/libjsonnet.h
