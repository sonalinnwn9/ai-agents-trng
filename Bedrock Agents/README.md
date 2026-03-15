# Bedrock Agents

## Product Recommendation Agent
This document outlines the technical configuration and testing procedures for 
a product recommendation agent developed using Amazon Bedrock. The system 
integrates AWS Lambda functions to handle logic and DynamoDB tables to manage 
product inventories and customer shopping carts. By leveraging a Knowledge 
Base stored in an S3 bucket, the assistant provides users with personalised gift
wrapping suggestions through Retrieval-Augmented Generation. During the testing 
phase, the agent demonstrates its ability to filter products by category or occasion, 
manage user identification via email, and suggest related items based on collective 
consumer data. Finally, essential troubleshooting steps are captured to ensure the 
agent functions reliably. 
---

### System Overview and Agent Config :
![Input](assets/SystemOverview_Agent.png)

### High Level Serverless Architcture
![Input](assets/HL_Serverless_Arch.png)

**Features :**
• Dynamic filtering 
• Cart management 
• Contextual Assistance 
---

### 1.Agent Configuration: 

**Agent Name, Agent ARN**

![Input](assets/1AgentOverview.png)

**Action Groups for Lambda call**
![Input](assets/2ActionGroups.png)

 
**KB for RAG**
![Input](assets/KB.png)

**S3 bucket location for uploaded gift wrapping file**
![Input](assets/KB_giftwrapping.png)

**DynamoDB table**
- Product table
   ![Input](assets/Table_product.png)

- Cart table
   ![Input](assets/CartTable.png) 

---

### 2.Tesing the AGent functionality 

---

** Initiating the product discovery flow**
**asks for  filter – occasion or category** 
   ![Input](assets/prompt1_test.png)



**Parses the occasion parameter and calls the lambda function to generate a tailored 
product recommendation from the database **
   ![Input](assets/parses_prodrecom.png)

   ![Input](assets/parses_prodrecom2.png)



**Establishes User Identity for Cart persistence **
    ![Input](assets/userid.png)



**Recommends a related product after adding the selected product. It shows executing 
cross-user collaborative filtering **

   ![Input](assets/recom_related.png)

   ![Input](assets/GET_personalise_recom.png)

   ![Input](assets/finalisecart_state.png)

   

(**Finalising Cart additions and displaying State**)

   ![Input](assets/finalisecart_postcart.png)

   ![Input](assets/showcart_aterbothadded.png)


**Enhances the Experience with RAG and Knowledge Bases as it asks about gift wrapping**

   ![Input](assets/RAG_KB_Giftwrappingsuggest.png)
  
**Retrieval from KB which has s3 bucket as Data Source **
    
   ![Input](assets/fromKB1.png)
 
 
**Concludes the conversation with a polite message and wishes them**
    ![Input](assets/concludeconversation.png)


### Verifying the Backend DynamoDB State :

For the current user sonali@bb.com , 2 products are added. To provide personalise 
recommendation, it refers another user’ cart details snn@yy.com 

   ![Input](assets/verfiying.png)
---
### 3.Troubleshooting checklist : 
1) Lambda function permissions to enable the agent to do function call

   ![Input](assets/troubleshooting1.png)

2) Check table name in the lambda function code 
3) IAM user permissions  
4) To Make sure the KB is used to retrieve the information, syncing  the Data Source 
   is important 
   ![Input](assets/troubleshooting4.png) 

### 4.Project summary and Technical Outcome :

   ![Input](assets/Tech%20Outcomes.png)
