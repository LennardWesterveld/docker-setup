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
	php55w \
	php55w-opcache \
	php55w-common \
	php55w-cli \
	php55w-pdo \
	php55w-mysql \
	php55w-gd \
	php55w-mbstring \
	php55w-mcrypt \
	php55w-xml \
	php55w-imap \
	php55w-intl \
	php55w-soap \
	php55w-tidy \
	php55w-bcmath \
	php55w-xmlrpc \
	php55w-pecl-xdebug \
	mod_fastcgi

# Clean up yum repos to save spaces
RUN yum update -y && yum clean all

RUN mkdir /usr/lib/cgi-bin/
RUN mkdir /etc/httpd/vhosts.d

# start apache at boot
RUN /sbin/chkconfig --add httpd
RUN /sbin/chkconfig httpd on --level 235

# Restart httpd
RUN /etc/init.d/httpd restart

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install drush
RUN wget http://files.drush.org/drush.phar && \
		chmod +x drush.phar && \
		mv drush.phar /usr/local/bin/drush

# Install modman
RUN curl -Ss https://raw.githubusercontent.com/colinmollenhour/modman/master/modman-installer | bash && \
		mv /root/bin/modman /usr/local/bin/modman

# Install Magerun
RUN wget https://files.magerun.net/n98-magerun.phar && \
		chmod +x ./n98-magerun.phar && \
		mv ./n98-magerun.phar /usr/local/bin/magerun

# Install Magerun addons
RUN mkdir -p ~/.n98-magerun/modules/ && \
	cd ~/.n98-magerun/modules/ && \
	# causes issues with APC
	# git clone https://github.com/peterjaap/magerun-addons.git pj-addons && \
	git clone https://github.com/Hypernode/hypernode-magerun.git && \
	git clone https://github.com/kalenjordan/magerun-addons.git && \
	git clone https://github.com/LimeSoda/LimeSoda_EnvironmentConfiguration.git && \
	git clone https://github.com/Zookal/HarrisStreet-ImpEx.git

# Fix permissions
RUN usermod -u 1000 apache
RUN groupmod -g 1000 apache

# Run bash profile
RUN source ~/.bash_profile

#ENTRYPOINT ["/bin/bash"]
ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
