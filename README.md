![image](http://images.cnitblog.com/i/607542/201403/141558148063393.gif)

Pyspark Streaming Consume Kafka Data and Put into Hbase  
===================================  
  The project is for use Pyspark Streaming to real-time consumption of Kafka data<br />  
    
  
1.The Implementation Process Of Project  
-----------------------------------  
  Include the priciple of frame and code<br />   
    
### 1.1Framework of Porject  
 Spark2.1 , kafka1.0 , python2.7 ,hbase0.98<br />
 
### 1.2Theory of Porject
 Spark-Streaming have two method to cunsume kafka data<br />   

    （1）first is Receive-base method as same as Storm,real-time read cache_data to memory， that‘s it after extract  
    kafka_data ,to put data into memory,then timing handle. but this way has some disadvantage such as if clony   
    out，data will be losed ，this also can be void for start WAL and setting Storagelevel，so will hava a receiver 
    to real-time consume data
    
    （2）second is Direct method at regular time  to read data ，this way is delayed. That is, when action really
    triggers it,only goes to kafka to receive data . it mapping kafka_partition_data to kafka_rdd

     
### 1.3Core_Code of Project
```javascript
    lines = KafkaUtils.createDirectStream(ssc,topic,kafkaParams={"metadata.broker.list":brokers})
    with table.batch(batch_size=1000) as b:
            b.put((line.label),{
                b'label:itemtype': (line.label),
                b'infomation:url': (str(line.value)),})
```

    
    
2.The conclusion Of Project  
----------------------------------- 

    the project is failed when submit spark on yarn

 
### 链接  
1.[click this connect to www.google.com](http://www.google.com)<br />  
2.[click this connect to www.baidu.com](http://www.baidu.com)<br />  
