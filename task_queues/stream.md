## [Kafka To ES Pipeline](http://www.plantuml.com/plantuml/uml/bLNVQzim47xtNt7afR2IbVRHf7bfCpQwBQKUxA4DGzXouyMMZIJt1wN_-qwdisIxXRAG4Ej-V7VtVP9yjBUsC-d9ILSBPVkc_fotpOcnmifbKObxBPeaCOTATG8VeMbLc-zrsqYmkfS91S9rNzTIGmhVgrBcptajhuMsLLvrY7cd4Ww3HIRrGvNB6BS0OU8ANXA0sqyxM2xNW3dQzXsWQNXSQhHpCKXU8-wLA0-2iEXfWhF9608ZDraAegxX84e1ya4gYoZHlTZgMWfb8BDQYeO0kPn3nA_xSEoZg2oKhORBodJ2vdkf5-Z5b4Fv6tsJw4EvSTKCScG8-rjnfwW1CqNjUdql8HS8H-LHZQQoAO1t-1GeKG4VDC-kwuLlmVKzTVfSTc_6jI7C1gtA7DcUwWaAhnob1qToC1FZ53q53JE_W-Gzv1XnnIjCy6CFPhzQzlFIiNttYFi1agWbwkwreucbGGc7U1yXpKUQV2orDEFsETot2srP6ccv-WNhQCI3P0_-XS8mWmX2IZCcxgsIOOZ8Hs3bHZQLAgH6oQOmZ8fqobeOFAZHuTUmB9pJp7P9A4REyUIy1D9ec1P6NhQGrzKcfLxTeN8_FrTazoKvsggiptDf347oVaY6SwhWftooy5MAskwVYGc0hIBZQeKzwkUkhPHTh-SfDn9zbE33gPbfIcXeGSw1HahAfDtG08CrvSFOQuqOBEsTqguC26jbqrau7vwEZ_y3-knTR3Y6qxVufmCkei2l5k2oVLIsmdlwHrlugoHOKjYB0Wy4PSpocD6OnGQtdYO6aZAtfRTnitERgOyDOQXkBdI11sUr-ej4epJikhZo_wjLlc_nzO2UmUHkcqog0alV-akPEjl5W3Kmi0kP3BqRyFC_t58iW6q5AnKPZOaux3a_1tSUm23x8xHILFKSozbSBzm0Ok26-uB6NcCZxCT3DLJr0Rp5HzXUrmbui18Ny-rtEzq9AsZ44tZRRfHQl9TyDizUJxAJP7H4M0WskIKBdJ1PpiAg92xIdLeQEnb88Gk19_74E-bUy2tCjtUyOZ1wL1vfYE-J8lZG_Wy0)
#### Preprocessing
 > Kafka Connect 
- Pull head from kafka
- Group by webhook URL [Index by]
- Save To **Elastic**
     
#### Preprocessing
 > Orleans Stream Provider 
- Pull head from kafka
- Group by webhook URL
- Save in **In Memory Stream**
- Commit to **Kafka**
 
#### Each Webhook Group 
> Orleans Stream Subscriber (Dispatcher)
- Pull head from **In Memory Stream**
- Send batch
- Commit to **In Memory Stream**

#### On Failure
> Elastic Consumer  
- Wait a little bit 
- Pull head from **Elastic** from failing offset
- Send batch
- Commit offset to **Elastic**


-------------------------------- 

## [Kafka To Kafka Pipeline](http://www.plantuml.com/plantuml/uml/RLFRQkCm47tNLmnvNEWFXEA7RTYbKDebsP2748egZub9B1b9tYQ4_FlEZEHBcXg3DMVEI6T6n-5GsrPxtK3Zh3Dxxng4w3jKeEW52557X2TdGzUWlqomsKOV4DRj37G0NgzRU7n46_svTRMDHJ5GLsXBDKJclTBraRXcxsg3HG4mtNQ9j8Dikd2VDjOaY8w5Fh_HTPp3zkCCdedGka_qkmd1lAV4xVv3sk8fiivJ7RDCIYaXPCQY3aRxak8BWoa54yAC-u6_3dvH7rYArkWu-9ORuPNFT5KLC0fPulxGzAJwXq9oENFjANrBbCxYvjk4w1YnQQaXQFGfJsJtfQYaicThFEg0CjolnSLzyGsVwddgASChtfBdc90iAKE4NUKw5VIke7fOeYuPaky3Dme_kwf2Vuk9K_eK5_PrCdAAataKz2xYaMIRa2lUhDn9vt4teP2q9zSquXjYh3fZC0Hc95WOV12BvoPo99sCplpZNTaPadKPeE77U5xCOOCVU-SEi5w-o62sFtOixys-zgDAIyB6Ci77CDrMcfiQ1QXy7Bd9_oDFmqjTeJcR8ugVXeYaPTlz9jkjeZwE_suGAk423wWQX5AbZrsR6vObeNS58kWEdUg-gly0)  
#### Preprocessing
 > Main Consumer
- Pull head from kafka
- Group by webhook URL [Topic by] 
- Save to **Kafka**
      
#### Each Webhook Group
> Kafka Consumer 
- Pull head from **Kafka**
- Send batch
- Commit offset to **Kafka**

#### On Failure
> Kafka Consumer 
- Wait a little bit 
- Pull head from **Kafka** from failing offset  
- Send batch
- Commit offset to **Kafka**



 
      
      
      
   