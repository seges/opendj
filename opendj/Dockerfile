FROM ubuntu:trusty

RUN DEBIAN_FRONTEND=noninteractive apt-get -y update && apt-get -y upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install openjdk-7-jre-headless unzip

ADD OpenDJ-2.6.0.zip /opt/
RUN cd /opt/ && unzip OpenDJ-2.6.0.zip

ENV ROOT_USER_DN cn=Directory\ Manager
ENV ROOT_USER_PASS passpass
ENV BASE_DN dc=example,dc=org

WORKDIR /opt/opendj
RUN ./setup --cli -v \
  --ldapPort 1389 \
  --ldapsPort 1636 \
  --adminConnectorPort 4444 \
  --rootUserDN "$ROOT_USER_DN" \
  --rootUserPassword $ROOT_USER_PASS \
  --generateSelfSignedCertificate \
  --no-prompt --noPropertiesFile \
  --doNotStart --acceptLicense

ADD start /start
ENTRYPOINT ["/start"]
CMD ["start"]
EXPOSE 1389 1636 4444
