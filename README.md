# spark-history-server-helm
基于spark 3.2.2制作的helm包

# spark-history-server镜像包打包
```
cd ./3.2.2/image
wget https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/3.2.2/hadoop-aws-3.2.2.jar
wget https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-bundle/1.11.563/aws-java-sdk-bundle-1.11.563.jar
docker build -t umr/spark-history-server:3.2.2 .
```

# helm 打包、调试、安装
```
cd ./3.2.2
helm package ./spark-history-server
helm install -f ./spark-history-server/values.yaml spark-history-server spark-history-server-0.1.0.tgz --dry-run --debug
```

# 部分参数解析
```
# 读取minio的日志文件（默认开启s3a，关闭hdfs）
s3a:
  accessKey: minio
  enabled: true
  endpoint: http://192.168.208.129:32000
  impl: org.apache.hadoop.fs.s3a.S3AFileSystem
  logDirectory: s3a://sparklogs/all
  secretKey: minio123
  simpleAWSCredentialsProvider: org.apache.hadoop.fs.s3a.SimpleAWSCredentialsProvider
  sslEnable: false
  styleAccess: true
hdfs:
  enabled: false
# 读取hdfs的日志文件
s3a:
  enabled: false
hdfs:
  enabled: true
  logDirectory: hdfs://192.168.208.132:9000/spark/spark-events
```