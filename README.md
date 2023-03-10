# Spark

## Install Spark in Master Slave Mode (On all nodes)

Download and Extract required version of Spark on Master and Slaves
```
wget https://www.apache.org/dyn/closer.lua/spark/spark-3.2.3/spark-3.2.3-bin-without-hadoop.tgz
tar xvf spark-3.2.3-bin-without-hadoop.tgz
mv spark-3.2.3-bin-without-hadoop /usr/local/spark

```

Add environment variables in .bashrc
```
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export SPARK_HOME=/usr/local/spark
export PATH=$PATH:$SPARK_HOME/bin
export LD_LIBRARY_PATH=$HADOOP_HOME/lib/native:$LD_LIBRARY_PATH
export SPARK_DIST_CLASSPATH=$(hadoop classpath)
```

Then source .bashrc 
```
source .bashrc
```

On spark-env.sh workers file add the required details.

/usr/local/spark/bin/spark-env.sh
```
export SPARK_MASTER_HOST=namenode
```

/usr/local/spark/bin/workers
```
datanode1
datanode2
datanode3
```

# Only on namenode (Spark Master)
Start and Stop Spark cluster
```
/usr/local/spark/sbin/start-all.sh
jps
/usr/local/spark/sbin/stop-all.sh
```

Spark Master UI avilable at http://namenode:8080/

Sample Program :
Save program as samplecode.py on namenode.

```
from pyspark import SparkContext, SparkConf

master_url = "spark://namenode:7077"

conf = SparkConf()
conf.setAppName("Hello Spark")
conf.setMaster(master_url)
sc = SparkContext(conf = conf)

list = range(10000)
rdd = sc.parallelize(list, 4)
even = rdd.filter(lambda x: x % 2 == 0)
print(even.take(5))
```

Run the program and check Spark Master UI.
```
/usr/spark/bin/spark-submit --master spark://namenode:7077 samplecode.py
```
