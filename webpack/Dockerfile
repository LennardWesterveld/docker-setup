
FROM node:4

#FROM centos:6
#
#RUN curl -sL https://rpm.nodesource.com/setup_4.x | bash -
#RUN yum -y install nodejs ruby
#RUN npm install npm -g

#TODO: searching for a fix of watching changes by mounted directory

CMD cd ${build} && npm install && npm rebuild node-sass && npm ${commando}