simple-kafka-sink
=================

flume与kafka集成，kafka的生产者作为flume的sink，用于flume向kafka集群发送数据

工具依赖：
apache-flume 1.4.0
apache-kafka_2.9.2 0.8.1.1

使用方式：
1.将本工具打成jar包，如xxx.jar
2.将xxx.jar放到 $FLUME_HOME/plugins.d/flume-kafka/lib/目录下
3.将$KAFKA_HOME/lib下的
  jopt-simple-3.2.jar
  kafka_2.8.0-0.8.0.jar
  metrics-annotation-2.2.0.jar
  metrics-core-2.2.0.jar
  scala-compiler.jar
  scala-library.jar
  snappy-java-1.0.4.1.jar
  拷贝到
   $FLUME_HOME/plugins.d/flume-kafka/libext/目录下
4.配置flume的properties（只列出sink部分）
  agent.sinks = kafkaSink
  agent.sources.avroSrc.channels = memoryChannel

  //kafka中topic名字
  agent.sinks.kafkaSink.topic = log_website
  agent.sinks.kafkaSink.type = cn._23hours.KafkaSink
  //kafka集群的机器及端口号
  agent.sinks.kafkaSink.metadata.broker.list = server-166:9092
  agent.sinks.kafkaSink.channel = memoryChannel

  agent.channels.memoryChannel.type = memory
  agent.channels.memoryChannel.capacity = 100