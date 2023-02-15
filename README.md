# spark-history-server-helm
基于spark 3.2.2制作的helm包

# 打印debug信息
helm install spark-history-server-test ./3.2.2/spark-history-server --dry-run --debug

# 安装
helm install -f ./3.2.2/spark-history-server/value.yaml spark-history-server ./3.2.2/spark-history-server

# 参数信息设置
使用hdfs
```
--set s3a.enabled=false
--set hdfs.enabled=ture
--set hdfs.logDirectory=hdfs://xxx:9000/spark/spark-events
```
