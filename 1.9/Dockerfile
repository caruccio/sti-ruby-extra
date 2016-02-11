FROM getupcloud/ruby-19-centos7:latest

USER root

RUN INSTALL_PKGS="ImageMagick ImageMagick-devel crontabs nss_wrapper" && \
    yum install -y --setopt=tsflags=nodocs --enablerepo=centosplus $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y

COPY nss-wrapper-setup /usr/bin/

USER 1001
