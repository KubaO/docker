FROM centos/systemd

LABEL maintainer="Kuba Ober <kuba@mareimbrium.org>"

#VOLUME ~/wc/docker-c7-foreman/c7-foreman:/mnt/host

COPY preinstall /root/preinstall
RUN chmod 0500 /root/preinstall && /root/preinstall 1

#RUN yum -y install wget
#RUN wget https://copr.fedorainfracloud.org/coprs/jsynacek/systemd-backports-for-centos-7/repo/epel-7/jsynacek-systemd-backports-for-centos-7-epel-7.repo -O /etc/yum.repos.d/jsynacek-systemd-centos-7.repo
#RUN yum -y upgrade systemd

COPY system/* /etc/systemd/system/
RUN chmod 0444 /etc/systemd/system/foreman-*
RUN systemctl enable foreman-installer.service

EXPOSE 443 8443 8140

CMD ["/usr/sbin/init", "--unit", "foreman-install.target"]