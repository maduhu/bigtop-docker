# Creates Bigtop base docker image
#
# 

FROM bigtop-base-x86_64
MAINTAINER Amir Sanjar
USER root

# install dev tools
RUN apt-get update && \
    RUNLEVEL=1 apt-get install -y hadoop-hdfs* hadoop-yarn* hadoop-mapred* hadoop-conf*

ADD start_bigtop_services.sh /etc/start_bigtop_services.sh
RUN chown root:root /etc/start_bigtop_services.sh
RUN chmod 700 /etc/start_bigtop_services.sh

RUN echo "export JAVA_HOME=` find /usr/ -name java-8-openjdk-*`" |  tee -a  /etc/environment $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh $HADOOP_PREFIX/etc/hadoop/yarn-env.sh && \
    echo "export HADOOP_CONF_DIR=/etc/hadoop/conf"  |  tee -a $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh $HADOOP_PREFIX/etc/hadoop/yarn-env.sh && \
    echo "export HADOOP_PREFIX=/usr/lib/hadoop"  |  tee -a $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh $HADOOP_PREFIX/etc/hadoop/yarn-env.sh  && \
    echo "export HADOOP_LIBEXEC_DIR=/usr/lib/hadoop/libexec" | tee -a $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh $HADOOP_PREFIX/etc/hadoop/yarn-env.sh && \
    echo "export HADOOP_LOGS=/usr/lib/hadoop/logs"  |  tee -a $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh $HADOOP_PREFIX/etc/hadoop/yarn-env.sh && \
    echo "export HADOOP_COMMON_HOME=/usr/lib/hadoop" |  tee -a  $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh $HADOOP_PREFIX/etc/hadoop/yarn-env.sh && \
    echo "export HADOOP_HDFS_HOME=/usr/lib/hadoop-hdfs" |  tee -a  $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh $HADOOP_PREFIX/etc/hadoop/yarn-env.sh && \
    echo "export HADOOP_MAPRED_HOME=/usr/lib/hadoop-mapreduce" |  tee -a $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh $HADOOP_PREFIX/etc/hadoop/yarn-env.sh && \
    echo "export HADOOP_YARN_HOME=/usr/lib/hadoop-yarn" |  tee -a $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh $HADOOP_PREFIX/etc/hadoop/yarn-env.sh
    
RUN  sed -i s/localhost/namenode/ /etc/hadoop/conf/core-site.xml && \
     chown -R hdfs:hadoop /usr/lib/hadoop*  && \
     chown -R hdfs:hadoop /var/log/hadoop-hdfs*  && \
     chown -R yarn:hadoop /var/log/hadoop-yarn*  && \
     chown -R mapred:hadoop /var/log/hadoop-mapred*  && \
     chown -R root:hadoop /etc/hadoop 

RUN su hdfs -c "hdfs namenode -format"

CMD ["bash"]
EXPOSE 50020 50090 50070 50010 50075 8031 8032 8033 8040 8042 49707 22 8088 8030
