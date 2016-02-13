FROM getupcloud/ruby-19-centos7:latest

USER root

RUN INSTALL_PKGS="ImageMagick ImageMagick-devel nss_wrapper uid_wrapper" && \
    yum install -y --setopt=tsflags=nodocs --enablerepo=centosplus $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y && \
    chmod +s /usr/lib64/libnss_wrapper.so && \
    mkdir -p /etc/cron.d && \
    chmod 777 /var/spool/cron/ && \
    sed -i -s 's/^\(account\s\+include\s\+password-auth\)$/#\1/' /etc/pam.d/crond && \
    chmod -s /usr/bin/crontab

COPY nss-wrapper-setup $STI_SCRIPTS_PATH

USER 1001
