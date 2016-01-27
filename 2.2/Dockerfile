FROM openshift/ruby-22-centos7:latest

USER root

RUN INSTALL_PKGS="ImageMagick ImageMagick-devel" && \
    yum install -y --setopt=tsflags=nodocs --enablerepo=centosplus $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y

USER 1001
