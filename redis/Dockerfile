FROM centos:8

ENV EPEL=https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm \
REMI=https://rpms.remirepo.net/enterprise/remi-release-8.rpm \
LANG=es_ES.UTF-8 \
LANGUAGE=es_ES.UTF-8 \
LC_COLLATE=C \
LC_CTYPE=es_ES.UTF-8


LABEL autor="Martin Vilche <mfvilche@gmail.com>" \
      io.k8s.description="php s2i images" \
      io.k8s.display-name="php Applications" \
      io.openshift.tags="builder,php,composer,centos" \
      io.openshift.expose-services="8080" \
      io.openshift.s2i.scripts-url="image:///usr/libexec/s2i"
      

RUN echo "LANG=$LANG" > /etc/locale.conf && \
yum install glibc-langpack-en glibc-langpack-es glibc-all-langpacks -y && yum update -y && yum install $EPEL yum-utils -y && yum install $REMI -y && \
yum --enablerepo=remi install redis unzip curl nc which -y && \
yum autoremove -y &> /dev/null && yum clean all &> /dev/null && rm -rf /var/cache/yum &> /dev/null 

RUN mkdir /opt/redis /opt/redis-data /opt/redis-config && usermod -u 1001 redis && usermod -aG 0 redis && touch /etc/localtime /etc/timezone && \
chown  -R 1001 /opt /etc/timezone /etc/localtime /var/lib/redis && \
chgrp -R 0 /opt /etc/timezone /etc/localtime /var/lib/redis && \
chmod -R g=u /opt /etc/timezone /etc/localtime /var/lib/redis
WORKDIR /opt/redis

USER 1001:0

EXPOSE 8080