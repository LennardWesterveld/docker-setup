FROM blinkreaction/drupal-cli

RUN git clone https://github.com/LennardWesterveld/kraftwagen.git ~/.drush/kraftwagen

# Fix permissions
RUN usermod -u 1000 docker
RUN sudo groupmod -g 1000 users

COPY startup.sh /opt/startup.sh


RUN ls -la /opt/
RUN sudo chmod 777 /opt/startup.sh
# Starter script
ENTRYPOINT ["/opt/startup.sh"]

# By default, launch supervisord to keep the container running.
CMD ["gosu", "root", "supervisord"]