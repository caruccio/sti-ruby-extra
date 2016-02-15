FROM openshift/base-centos7

# This image provides a Ruby 2.0 environment you can use to run your Ruby
# applications.

MAINTAINER SoftwareCollections.org <sclorg@redhat.com>

EXPOSE 8080

ENV RUBY_VERSION 2.0

LABEL io.k8s.description="Platform for building and running Ruby 2.0 applications" \
      io.k8s.display-name="Ruby 2.0" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,ruby,ruby20"

RUN INSTALL_PKGS="ruby200 ruby200-ruby-devel ruby200-rubygem-rake v8314 ror40-rubygem-bundler nodejs010" && \
    EXTRA_INSTALL_PKGS="ImageMagick ImageMagick-devel cronie crontabs nss_wrapper uid_wrapper" && \
    yum install -y centos-release-scl && \
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS $EXTRA_INSTALL_PKGS && rpm -V $INSTALL_PKGS $EXTRA_INSTALL_PKGS && \
    yum clean all -y

# Setup for run crond as user
RUN chmod 777 /var/spool/cron/ && \
    chmod -s /usr/bin/crontab && \
    sed -i -s 's/^\(account\s\+include\s\+password-auth\)$/#\1/' /etc/pam.d/crond

COPY nss-wrapper-setup $STI_SCRIPTS_PATH/

# Copy the S2I scripts from the specific language image to $STI_SCRIPTS_PATH
COPY ./s2i/bin/ $STI_SCRIPTS_PATH

# Each language image can have 'contrib' a directory with extra files needed to
# run and build the applications.
COPY ./contrib/ /opt/app-root

RUN chown -R 1001:0 /opt/app-root

USER 1001

# Set the default CMD to print the usage of the language image
CMD $STI_SCRIPTS_PATH/usage
