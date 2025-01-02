# Assignment2.14CE8

# AWS Messaging Services: SNS, SQS, EventBridge, and Dead-Letter Queue (DLQ)

This document provides answers to key questions about AWS messaging services, specifically regarding **SNS (Simple Notification Service)**, **Dead-Letter Queues (DLQs)**, and notifications for DLQs.

---

## Questions Addressed:

1. Does SNS guarantee exactly-once delivery to subscribers?  
2. What is the purpose of the Dead-Letter Queue (DLQ)?  
3. How would you enable a notification to your email when messages are added to the DLQ?  

---

## 1. Does SNS Guarantee Exactly-Once Delivery to Subscribers?

- **Answer**:  
  SNS (Simple Notification Service) **does not guarantee exactly-once delivery** to subscribers for standard topics. Messages sent to standard SNS topics can sometimes be delivered more than once, as the service operates with an at-least-once delivery guarantee.  

  However, SNS **FIFO (First-In-First-Out)** topics do support exactly-once message delivery. FIFO topics ensure that messages are delivered in order and are not duplicated, which is critical for use cases requiring strict message sequencing and accuracy.

---

## 2. What is the Purpose of the Dead-Letter Queue (DLQ)?

- **Answer**:  
  A **Dead-Letter Queue (DLQ)** is a special type of message queue used to store messages that a system cannot process or deliver.  

  **Key Purposes**:  
  - Provides temporary storage for undeliverable or unprocessable messages.  
  - Helps isolate problematic messages for troubleshooting and debugging.  
  - Prevents message loss by ensuring that failed messages are retained for further examination.  

  DLQs are available for **Amazon SQS**, **Amazon SNS**, and **Amazon EventBridge**, offering resilience in messaging workflows.

---

## 3. How Would You Enable a Notification to Your Email When Messages Are Added to the DLQ?

- **Answer**:  
  To enable a notification to your email when messages are added to the DLQ, follow these steps:  

  1. **Create an Amazon SNS Topic**:  
     - Create a new SNS topic to serve as the notification channel.  

  2. **Subscribe Your Email to the SNS Topic**:  
     - Add your email address as a subscriber to the SNS topic. Confirm the subscription via the email confirmation link.  

  3. **Enable DLQ Monitoring**:  
     - Set up an **Amazon CloudWatch Alarm** to monitor the DLQ for the number of messages (`ApproximateNumberOfMessagesVisible`).  

  4. **Trigger the SNS Notification**:  
     - Configure the CloudWatch alarm to trigger the SNS topic when the number of visible messages in the DLQ exceeds a specified threshold.  

By following this setup, you'll receive an email notification whenever new messages are added to the DLQ.

---

This README aims to clarify the nuances of SNS delivery guarantees, the role of DLQs, and setting up notifications for DLQs. 
