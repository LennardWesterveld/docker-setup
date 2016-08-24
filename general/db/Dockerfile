FROM percona:5.6

# Fix permissions
RUN usermod -u 1000 mysql
RUN groupmod -g 1000 mysql

EXPOSE 3306
CMD ["mysqld"]