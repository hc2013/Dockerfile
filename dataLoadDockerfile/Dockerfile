FROM ubuntu_baseimage:0.10.2

RUN mkdir -p /usr/software/jdk1.8.0_191/ && echo 'export JAVA_HOME=/usr/software/jdk1.8.0_191' >> /etc/profile \
    && echo 'export PATH=$JAVA_HOME/bin:$PATH' >> /etc/profile && echo 'export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar' >> /etc/profile \
    && /bin/bash -c "source /etc/profile"

COPY jdk1.8.0_191/  /usr/software/jdk1.8.0_191/

RUN mkdir -p /usr/src/app

COPY ./geo_hbase-1.0-SNAPSHOT.jar /usr/src/app
COPY ./load.sh /usr/src/app

ENTRYPOINT ["/bin/bash", "/usr/src/app/load.sh"]

RUN cp /etc/hosts /tmp/hosts
RUN mkdir -p -- /lib-override && cp /lib/x86_64-linux-gnu/libnss_files.so.2 /lib-override
RUN sed -i 's:/etc/hosts:/tmp/hosts:g' /lib-override/libnss_files.so.2
ENV LD_LIBRARY_PATH /lib-override
