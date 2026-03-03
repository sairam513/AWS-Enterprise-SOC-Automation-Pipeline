# AWS-Enterprise-SOC-Automation-Pipeline
A real-time, event-driven cloud security system that automatically detects and responds to threats in an AWS environment using fully managed, serverless services.
------------------------------------------------------------------------------------------------------------------------------------------------------------------
*Project Description:*
This project shows how to build a production-level security pipeline that can detect activity on AWS, use machine learning to detect threats, and send instant, human-readable alerts, all without having to manage a single server.
The scenario shows how to detect a compromised EC2 instance that makes outbound connections to a known malicious (blackhole) IP, which is a known threat pattern classified by AWS as Trojan:EC2/BlackholeTraffic.

# Architcture:

<img width="1282" height="1020" alt="image" src="https://github.com/user-attachments/assets/1630b0df-b941-4a13-ab09-e43a9c1caa51" />

#AWS Services Used
ServiceRoleAmazon GuardDutyAI/ML-powered continuous threat detectionAWS CloudTrailCaptures all API calls and account activityAmazon EventBridgeRoutes specific GuardDuty findings to downstream targetsAWS LambdaParses raw GuardDuty JSON and formats a readable alertAmazon SNSDelivers the formatted email notification to the security teamAWS IAMEnforces least-privilege permissions across services
