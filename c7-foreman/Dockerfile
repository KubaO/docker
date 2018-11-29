FROM centos/systemd

LABEL maintainer="Kuba Ober <kuba@mareimbrium.org>"

#VOLUME ~/wc/docker-c7-foreman/c7-foreman:/mnt/host

RUN yum -y install https://yum.puppetlabs.com/puppet5/puppet5-release-el-7.noarch.rpm
RUN yum -y install http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum -y install https://yum.theforeman.org/releases/1.20/el7/x86_64/foreman-release.rpm
RUN yum -y install centos-release-scl-rh
RUN yum -y install foreman-installer
RUN yum -y install foreman foreman-cli foreman-postgresql foreman-proxy foreman-debug foreman-release-scl
RUN yum clean all

#RUN yum -y install wget
#RUN wget https://copr.fedorainfracloud.org/coprs/jsynacek/systemd-backports-for-centos-7/repo/epel-7/jsynacek-systemd-backports-for-centos-7-epel-7.repo -O /etc/yum.repos.d/jsynacek-systemd-centos-7.repo
#RUN yum -y upgrade systemd

COPY system/* /etc/systemd/system/
RUN systemctl enable foreman-installer.service

EXPOSE 8443 8140

CMD ["/usr/sbin/init", "--unit", "foreman-install.target"]