FROM debian:11
LABEL version="1.0"
LABEL author="@edt ASIX-M11 20-21"
LABEL subject="Kerberos Server"
ARG DEBIAN FRONTEND=noninteractive
RUN apt-get update
RUN apt-get -y install vim procps tree nmap iproute2 krb5-user krb5-config krb5-admin-server
RUN mkdir /opt/docker
COPY * /opt/docker/
RUN chmod +x /opt/docker/startup.sh /opt/docker/install.sh
WORKDIR /opt/docker
EXPOSE  88 749 464
CMD [ "/opt/docker/startup.sh" ]
