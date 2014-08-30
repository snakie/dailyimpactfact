FROM centos:centos7
MAINTAINER ***REMOVED***

# ssh
RUN yum install openssh-server netcat sudo -y
RUN mkdir /var/run/sshd
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key

#user
RUN useradd ***REMOVED*** -G wheel
RUN echo '***REMOVED***:secret' | chpasswd
RUN echo '%wheel ALL=(ALL) ALL' >> /etc/sudoers
RUN mkdir -p /home/***REMOVED***/.ssh
ADD conf/authorized_keys /home/***REMOVED***/.ssh/
RUN chown -R ***REMOVED***:***REMOVED*** /home/***REMOVED***/.ssh; chmod 700 /home/***REMOVED***/.ssh
# nginx
COPY conf/nginx.repo /etc/yum.repos.d/nginx.repo
RUN yum install nginx -y
RUN rm /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/example_ssl.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
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

