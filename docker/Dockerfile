FROM flink:1.10.0-scala_2.12

ENV FLINK_VERSION 1.10.0

RUN mkdir $FLINK_HOME/plugins/s3-fs-presto && \
  ln -s $FLINK_HOME/opt/flink-s3-fs-presto-$FLINK_VERSION.jar $FLINK_HOME/plugins/s3-fs-presto/

