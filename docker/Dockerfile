FROM centos:centos7
MAINTAINER ***REMOVED***

# ssh
RUN yum install openssh-server telnet -y
# nginx
COPY conf/nginx.repo /etc/yum.repos.d/nginx.repo
RUN yum install nginx -y
RUN rm /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/example_ssl.conf
COPY conf/nginx.conf /etc/nginx/conf.d/dif.conf

# perl and mojolicous
RUN yum install perl-CPAN perl-Time-HiRes perl-Archive-Tar perl-Compress-Zlib perl-Test-More perl-Digest-MD5 -y
COPY conf/cpan.pm /.cpan/CPAN/MyConfig.pm
RUN cpan Test::More
RUN cpan Mojolicious

# supervisor
RUN yum install python-setuptools -y
RUN easy_install pip
RUN pip install supervisor
COPY conf/supervisor.conf /etc/supervisord.conf

EXPOSE 22 80
CMD ["/usr/bin/supervisord"]

