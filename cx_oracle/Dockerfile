FROM tsaiid/ubuntu-py3
MAINTAINER I-Ta Tsai <itsai@gmail.com>

# Oracle Instant Client layer
COPY instantclient/* /tmp/

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y alien && \
    alien -iv /tmp/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm && \
    alien -iv /tmp/oracle-instantclient12.2-devel-12.2.0.1.0-1.x86_64.rpm && \
    apt-get purge -y alien perl perl5 && apt-get -y autoremove && apt-get clean && \
    rm -rf /tmp/oracle-* && rm -rf /usr/share/docs && rm -rf /usr/share/man 

# Environment variables
ENV ORACLE_HOME=/usr/lib/oracle/12.2/client64
ENV LD_LIBRARY_PATH=$ORACLE_HOME/lib
ENV PATH=$ORACLE_HOME/bin:$PATH
ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

# Python3 + cx_Oracle layer
#RUN apt-get install -y python3 python3-dev python3-pip libaio1 
RUN pip3 install cx_Oracle

# Clean
#RUN apt-get -y autoremove && apt-get clean && \
#    rm -rf /usr/share/doc && rm -rf /usr/share/man

