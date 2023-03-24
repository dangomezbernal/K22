FROM debian
LABEL version="1.0"
LABEL author="@dan ASIX-M11 22-23"
LABEL subject="Kerberos Server"
ARG DEBIAN FRONTEND=noninteractive
RUN apt-get update
RUN apt-get -y install vim procps tree nmap iproute2 krb5-user krb5-config krb5-admin-server
RUN mkdir /opt/docker
COPY * /opt/docker/
WORKDIR /opt/docker
EXPOSE  88 749 464
