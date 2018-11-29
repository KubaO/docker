FROM centos/systemd

LABEL maintainer="Kuba Ober <kuba@mareimbrium.org>"

#VOLUME /sys/fs/cgroup:/sys/fs/cgroup
#VOLUME /sys/fs/cgroup/systemd

RUN yum -y install https://yum.puppetlabs.com/puppet5/puppet5-release-el-7.noarch.rpm
RUN yum -y install http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum -y install https://yum.theforeman.org/releases/1.20/el7/x86_64/foreman-release.rpm
RUN yum -y install foreman-installer

#RUN cat /etc/hostname
#RUN echo $(grep $(hostname) /etc/hosts | cut -f1) foreman.local >> /etc/hosts && echo foreman.local >> /etc/hostname && cat /etc/hosts && hostname -f && foreman-installer -i

RUN yum clean all

EXPOSE 8443 8140

CMD ["/usr/sbin/init"]