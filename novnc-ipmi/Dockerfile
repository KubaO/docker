FROM alpine:3.7

# Setup the environment variables
ENV HOME=/root \
	DEBIAN_FRONTEND=noninteractive \
	LANG=en_US.UTF-8 \
	LANGUAGE=en_US.UTF-8 \
	LC_ALL=C.UTF-8

# Install git & supervisor packages
RUN apk --update --upgrade add \
	bash \
	git \
	supervisor

# Clone noVNC from github
RUN git clone --branch bmc-support-old --depth 1 https://github.com/kelleyk/noVNC.git /root/noVNC \
	&& git clone --depth 1 https://github.com/novnc/websockify /root/noVNC/utils/websockify \
	&& rm -rf /root/noVNC/.git \
	&& rm -rf /root/noVNC/utils/websockify/.git \
	&& apk del git

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Modify the launch script 'ps -p' for docker
RUN sed -i -- "s/ps -p/ps -o pid | grep/g" /root/noVNC/utils/launch.sh

EXPOSE 8080

ENTRYPOINT ["/bin/sh", "-c", "export ARGS=\"$0 $@\"; /usr/bin/supervisord -c /etc/supervisor/conf.d/supervisord.conf"]
CMD ["--listen", "8080"]