![image]          (http://images.cnitblog.com/i/607542/201403/141558148063393.gif)

Pyspark Streaming Consume Kafka Data and Put into Hbase  
===================================  
  The project is for use Pyspark Streaming to real-time consumption of Kafka data<br />  
    
  
The Implementation Process Of Project  
-----------------------------------  
  Include the priciple of frame and code<br />   
    
### Framework of Porject  
 1.Spark2.1 , kafka1.0 , python2.7 ,hbase0.98<br />
 2.Spark-Streaming have two method to cunsume kafka data<br /> 
 ```javascript
  first is Receive-base method as same as Storm,real-time read cache_data to memory   
  second is Direct method at regular time  to read data 
 ```
     
### Core_Code of Project
```javascript
    lines = KafkaUtils.createDirectStream(ssc,topic,kafkaParams={"metadata.broker.list":brokers})
    with table.batch(batch_size=1000) as b:
            b.put((line.label),{
                b'label:itemtype': (line.label),
                b'infomation:url': (str(line.value)),})
```

    
    
The conclusion Of Project  
----------------------------------- 
```javascript
  the project is failed when submit spark on yarn
```
 
### 链接  
1.[点击这里你可以链接到www.google.com](http://www.google.com)<br />  
2.[点击这里你可以链接到www.baidu.com](http://www.baidu.com)<br />  
