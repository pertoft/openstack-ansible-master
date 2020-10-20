FROM ubuntu:20.04

#Update ubuntu repo to danish mirror
RUN sed -i 's|http://archive.ubuntu.com|http://dk.archive.ubuntu.com|g' /etc/apt/sources.list
#Update locales
RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

#Install openstack ansible requried packages
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
   aptitude build-essential git chrony openssh-server python3-dev sudo git vim nano inetutils-ping tcpdump

RUN mkdir -p /opt/openstack-ansible

#Clone OpenstackAnsible repo

RUN git clone -b 21.0.1 https://opendev.org/openstack/openstack-ansible /opt/openstack-ansible

#Bootstrap 
RUN cd /opt/openstack-ansible ; scripts/bootstrap-ansible.sh

#Dummy entryp - Access to the container is done with 'docker exec -it container bash'
ENTRYPOINT tail -f /dev/null
