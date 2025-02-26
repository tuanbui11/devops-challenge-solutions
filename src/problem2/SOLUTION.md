Provide your solution here:

## 📌 Architecture Overview
This system ensures **scalability, high availability, and cost optimization** for **500 requests/sec** with **p99 response time <100ms**.

### 🛠️ Services & Roles
- **S3 + CloudFront** → Serves frontend with caching.  
- **API Gateway + Lambda** → Serverless API processing.  
- **AWS Fargate** → Containerized order processing.  
- **Aurora Serverless** → Auto-scaling relational database.  
- **DynamoDB** → Fast caching and real-time lookups.  
- **SQS + SNS** → Asynchronous messaging.  
- **CloudWatch + X-Ray** → Monitoring and logging.  

## 📌 Why These Services?
| **Service**              | **Reason**                 | **Alternative**      |  
|--------------------------|----------------------------|----------------------|  
| **S3 + CloudFront**      | Fast, global CDN           | EC2 + Nginx          |  
| **API Gateway + Lambda** | Serverless, cost-effective | Nginx on EC2         |  
| **Fargate**              | Auto-scales containers     | EC2 Auto Scaling     |  
| **Aurora Serverless**    | Scalable database          | RDS MySQL/PostgreSQL |  
| **DynamoDB**             | Low-latency data access    | Redis (ElastiCache)  |  
| **SQS + SNS**            | Decouples services         | Kafka                |  
| **CloudWatch + X-Ray**   | Real-time monitoring       | Prometheus + Grafana |  

## 📌 Scaling Strategy
✅ **API & Order Processing** – Auto-scaling Fargate, Lambda provisioned concurrency.  
✅ **Database** – Aurora Read Replicas, DynamoDB Global Tables.  
✅ **Caching** – DynamoDB Accelerator (DAX), CloudFront caching.  
✅ **Messaging** – SQS FIFO for sequential trade execution.  
✅ **Cost Optimization** – AWS Savings Plans, CloudWatch monitoring.  

## 📌 Estimated Cost
💰 **$1,050 - $5,200/month** *(varies by traffic & data usage)*  
