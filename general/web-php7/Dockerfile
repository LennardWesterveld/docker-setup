FROM centos:6

# Extra packages
RUN yum install -y epel-release
RUN rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm

# Install NodeJS v5 and NPM
RUN curl --silent --location https://rpm.nodesource.com/setup_5.x | bash -
RUN yum install nodejs -y

# Install tools
RUN yum install -y yum-utils \
	python-setuptools \
	inotify-tools \
	unzip \
	sendmail \
	tar \
	mysql \
	sudo \
	wget \
	telnet \
	rsync \
	git \
	vim \
	redis \
	jpegtran \
	pngquant \
	optipng \
	vixie-cron

# Install php-fpm and php extensions
RUN yum install -y httpd \
	php70w \
	php70w-opcache \
	php70w-common \
	php70w-cli \
	php70w-pdo \
#	php70w-mysql \
	php70w-gd \
	php70w-mbstring \
	php70w-mcrypt \
	php70w-xml \
	php70w-imap \
	php70w-intl \
	php70w-soap \
	php70w-tidy \
	php70w-bcmath \
	php70w-xmlrpc \
	php70w-pecl-xdebug \
	php70w-mysqlnd \
	mod_fastcgi

# Clean up yum repos to save spaces
RUN yum update -y && yum clean all

RUN mkdir -p /var/lib/php/session && \
    mkdir -p /var/lib/php/wsdlcache && \
    chmod -R 777 /var/lib/php/session && \
    chmod -R 777 /var/lib/php/wsdlcache

RUN mkdir /usr/lib/cgi-bin/
RUN mkdir /etc/httpd/vhosts.d

# start apache at boot
RUN /sbin/chkconfig --add httpd
RUN /sbin/chkconfig httpd on --level 235

# Restart httpd
RUN /etc/init.d/httpd restart

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
# Fix permissions
RUN usermod -u 1000 apache
RUN groupmod -g 1000 apache

#ENTRYPOINT ["/bin/bash"]
ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
