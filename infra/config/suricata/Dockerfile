FROM ubuntu:18.04
MAINTAINER JREY
RUN apt-get update
RUN apt-get install -y suricata ethtool net-tools
RUN cd /home/ 
RUN wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz 
RUN tar zxf emerging.rules.tar.gz 
RUN cp -r rules /etc/suricata/
ENTRYPOINT [ "suricata", "-c", "/etc/suricata/suricata.yaml", "-i", "eth0", "-k", "none" ]

