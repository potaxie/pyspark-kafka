![image](http://images.cnitblog.com/i/607542/201403/141558148063393.gif)

Pyspark Streaming Consume Kafka Data and Put into Hbase  
===================================  
  The project is for use Pyspark Streaming to real-time consumption of Kafka data<br />  
    
  
1.The Implementation Process Of Project  
-----------------------------------  
  Include the priciple of frame and code<br />   
    
### (1) Requirments  
 Spark2.1,kafka1.0,python2.7,hbase0.98<br />
 
### (2) principle of Porject
 PySpark_Streaming have two method to cunsume kafka data<br />   

    <1> one is Receive-base method as same as Storm,real-time read cache_data to memory， that‘s it after extract  
    kafka_data ,to put data into memory,then timing handle. but this way has some disadvantage such as if clony   
    out，data will be losed ，this also can be void for start WAL and setting Storagelevel，so will hava a receiver 
    to real-time consume data
    
    <2> other is Direct method at regular time  to read data ，this way is delayed. That is, when action really
    triggers it,only goes to kafka to receive data . it mapping kafka_partition_data to kafka_rdd
  
  now the second way is more popular
   
### (3) Core_Code of Project
```javascript
    //create streaming receive kafka data
    lines = KafkaUtils.createDirectStream(ssc,topic,kafkaParams={"metadata.broker.list":brokers})
    //get the required data
    lines1=lines.map(lambda x:x[1])
    //get a new rdd like schema data
    parsed_words=lines1.map(lambda data:Row(label=getValue(str,data["identity"]),
                                            value=data))
    //parese each rdd insert into hbase                                       
    parsed_words.foreachRDD(save_to_hbase)   
    def save_to_hbase(parsed_words)
      for line in parsed_rdd.collect():
          with table.batch(batch_size=1000) as b:
              b.put((line.label),{
                  b'label:itemtype': (line.label),
                  b'infomation:url': (str(line.value)),})
```
    
    
2.Problems of Project
-----------------------------------  

    the project is failed when submit spark on yarn maybe caused kafka_version or spark environment,<br />
    the error log shows failed because of the conflict of jar package，however when  submit pyspark_egg，<br />
    i only -jar spark-streaming-kafka-0-8-assembly_2.11-2.1.0.jar,so i guess this jar conflict with yarn jar.<br />
    
3.The conclusion of Project  
----------------------------------- 
    Writing spark with python is simple, provided that there is no problem with the development environment

 
### connection 
1.[click this connect to www.baidu.com](http://www.baidu.com)
