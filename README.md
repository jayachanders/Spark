# Spark

# Install Spark in Master Slave Mode

# Add environment variables
add in .bashrc
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
