FROM centos/systemd

LABEL maintainer="Kuba Ober <kuba@mareimbrium.org>"

#VOLUME ~/wc/docker-c7-foreman/c7-foreman:/mnt/host

RUN yum -y upgrade
RUN yum -y install https://yum.puppetlabs.com/puppet5/puppet5-release-el-7.noarch.rpm
RUN yum -y install http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum -y install https://yum.theforeman.org/releases/1.20/el7/x86_64/foreman-release.rpm
RUN yum -y install centos-release-scl-rh foreman-release-scl
RUN yum -y install foreman foreman-cli foreman-postgresql foreman-proxy foreman-debug foreman-installer
RUN yum -y install \
	apr apr-util centos-logos copy-jdk-configs efivar-libs file freetype gettext \
	grub2-efi-x64 grub2-efi-x64-modules grub2-tools grub2-tools-extra httpd httpd-tools initscripts \
	iproute iptables java javapackages-tools \
	libcroco libeio libev libgomp libjpeg-turbo libmnl libnetfilter_conntrack \
	libnfnetlink libunistring libxslt \
	lksctp-tools mailcap make mod_passenger mod_ssl mokutil mtools openssl os-prober passenger \
	postgresql postgresql-server puppet-agent-oauth puppetserver python-javapackages python-lxml \
	rubygem-daemon_controller shim shim-x64 syslinux sysvinit-tools tcp_wrappers-libs \
	tfm-rubygem-passenger-native tftp-server tzdata-java xinetd
RUN rm -rf /var/cache/yum
RUN yum clean all

#RUN yum -y install wget
#RUN wget https://copr.fedorainfracloud.org/coprs/jsynacek/systemd-backports-for-centos-7/repo/epel-7/jsynacek-systemd-backports-for-centos-7-epel-7.repo -O /etc/yum.repos.d/jsynacek-systemd-centos-7.repo
#RUN yum -y upgrade systemd

COPY system/* /etc/systemd/system/
RUN chmod 0444 /etc/systemd/system/foreman-*
RUN systemctl enable foreman-installer.service

EXPOSE 443 8443 8140

CMD ["/usr/sbin/init", "--unit", "foreman-install.target"]