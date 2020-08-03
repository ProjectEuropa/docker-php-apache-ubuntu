FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

# システム更新
RUN apt update && apt -y upgrade && apt-get dist-upgrade

# apacheをインストール
RUN apt -y install apache2 apache2-utils

# add-apt-repositoryを使用可能にする
RUN apt install -y software-properties-common

# 文字コードをUTF8セットしてphp7.2をインストール
RUN apt -y install language-pack-en
RUN update-locale LANG=en_US.UTF-8
RUN LC_ALL=C.UTF-8 add-apt-repository -y -u ppa:ondrej/php
RUN apt install -y php7.2 libapache2-mod-php7.2

# その他PHP拡張パッケージをインストール
RUN apt install -y libapache2-mod-php7.2 php7.2-bcmath php7.2-bz2 php7.2-cli php7.2-common php7.2-curl php7.2-dba php7.2-gd php7.2-gmp php7.2-imap php7.2-intl php7.2-ldap php7.2-mbstring php7.2-mysql php7.2-recode php7.2-snmp php7.2-soap php7.2-tidy php7.2-xml php7.2-xmlrpc php7.2-xsl php7.2-zip

# composerのインストール
RUN apt -y install curl
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN a2enmod rewrite

# apacheをフォアグラウンドで起動
CMD apachectl -D FOREGROUND

WORKDIR /var/www/html