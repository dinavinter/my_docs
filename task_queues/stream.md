## Kafka To ES Pipeline 
#### Preprocessing
 > Kafka Connect 
- Pull head from kafka
- Group by [Index by] webhook URL
- Save To Elastic
     
#### Preprocessing
 > Orleans Stream Provider 
- Pull head from kafka
- Group by webhook URL
- Save in cache
 
#### Each Webhook Group 
> Orleans Stream Subscriber (Dispatcher)
- Pull head from stream 
- Send batch
- Commit to stream 

#### On Failure
> Elastic Consumer  
- Wait a little bit 
- Pull head from Elastic  
- Send batch
- Commit offset to Elastic


-------------------------------- 

## Kafka To Kafka Pipeline  
#### Preprocessing
 > Main Consumer
- Pull head from kafka
- Group by [Topic by] webhook URL
- Save to kafka
      
#### Each Webhook Group
> Kafka Consumer 
- Pull head from kafka
- Send batch
- Commit offset to kafka

#### On Failure
> Kafka Consumer 
- Wait a little bit 
- Pull head from kafka  
- Send batch
- Commit offset to kafka


 
      
      
      
   