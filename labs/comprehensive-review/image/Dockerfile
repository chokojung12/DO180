FROM ubi7/ubi:7.7

MAINTAINER minki kook chokojung12@gmail.com

LABEL description="Comprehensive test" 


ENV NEXUS_VERSION="2.14.3-02" \
    NEXUS_HOME="/opt/nexus"
	
COPY ./training.repo /etc/yum.repos.d/
	
RUN yum install -y --setopt=tsflags=nodocs java-1.8.0-openjdk-devel && \
    yum clean all -y && \
	groupadd -r nexus -f -g 1001 && \
	useradd -u 1001 -r -g nexus -m -d ${NEXUS_HOME} \
    -s /sbin/nologin \
    -c "Nexus User" nexus


ADD ./nexus-2.14.3-02-bundle.tar ${NEXUS_HOME}/ && \
    ./get-nexus-bundle.sh ${NEXUS_HOME}/

RUN ln -s ${NEXUS_HOME}/nexus-${NEXUS_VERSION} ${NEXUS_HOME}/nexus2 && \
    chown -R nexus:nexus ${NEXUS_HOME}/

USER nexus

WORKDIR /opt/nexus

VOLUME ["/opt/nexus/sonatype-work"] 
