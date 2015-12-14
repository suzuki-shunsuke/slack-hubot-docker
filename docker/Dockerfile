FROM debian:8.2
COPY locale.gen /etc/locale.gen
RUN apt-get update
RUN apt-get install -y sudo python python3 wget locales supervisor
RUN rm -rf /var/lib/apt/lists/*
RUN locale-gen
RUN update-locale LANG=ja_JP.UTF-8
RUN wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py
RUN python3 get-pip.py
RUN python get-pip.py
RUN rm get-pip.py
RUN useradd -m debian
RUN gpasswd -a debian sudo
WORKDIR /root
RUN wget https://nodejs.org/dist/v5.2.0/node-v5.2.0-linux-x64.tar.gz
RUN tar xvzf node-v5.2.0-linux-x64.tar.gz
RUN rm node-v5.2.0-linux-x64.tar.gz
RUN mv node-v5.2.0-linux-x64/ /usr/local/lib/node
RUN ln -s /usr/local/lib/node/bin/node /usr/local/bin/node
RUN ln -s /usr/local/lib/node/bin/npm /usr/local/bin/npm
RUN npm install -g hubot coffee-script yo generator-hubot
ENV LANG=ja_JP.UTF-8 TERM=xterm
COPY supervisord.conf /etc/supervisor/
EXPOSE 80
ONBUILD COPY . /usr/local/lib/hubot
ONBUILD CMD /usr/bin/supervisord -c /etc/supervisor/supervisord.conf
