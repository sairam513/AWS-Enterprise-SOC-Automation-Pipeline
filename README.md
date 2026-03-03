# AWS-Enterprise-SOC-Automation-Pipeline
A real-time, event-driven cloud security system that automatically detects and responds to threats in an AWS environment using fully managed, serverless services.
------------------------------------------------------------------------------------------------------------------------------------------------------------------
*Project Description:*
This project shows how to build a production-level security pipeline that can detect activity on AWS, use machine learning to detect threats, and send instant, human-readable alerts, all without having to manage a single server.
The scenario shows how to detect a compromised EC2 instance that makes outbound connections to a known malicious (blackhole) IP, which is a known threat pattern classified by AWS as Trojan:EC2/BlackholeTraffic.

# Architcture:

<img width="1282" height="1020" alt="image" src="https://github.com/user-attachments/assets/1630b0df-b941-4a13-ab09-e43a9c1caa51" />


# AWS Service Used

| Service | Role |
|---|---|
| **Amazon GuardDuty** | AI/ML-powered continuous threat detection |
| **AWS CloudTrail** | Captures all API calls and account activity |
| **Amazon EventBridge** | Routes specific GuardDuty findings to downstream targets |
| **AWS Lambda** | Parses raw GuardDuty JSON and formats a readable alert |
| **Amazon SNS** | Delivers the formatted email notification to the security team |
| **AWS IAM** | Enforces least-privilege permissions across services |

# Why This Architecture

**GuardDuty** eliminates the burden of implementing threat rules. Instead, GuardDuty utilizes Amazon's proprietary machine learning algorithms, as well as threat intelligence feeds, to automatically analyze CloudTrail logs, VPC Flow Logs, and DNS requests.

**EventBridge** serves as a zero-latency router for events. Instead of having to poll for results, events are pushed the moment GuardDuty sends the alert.

**Lambda** connects the dots between machine-generated events and human-readable notifications. GuardDuty findings are machine-generated JSON messages. Lambda extracts the meaningful information from the finding (instance ID, remote IP, finding type, region, timestamp), providing a human-readable message.

**SNS** sends the message to any subscriber, providing the simplicity of sending the message to the appropriate people.

**CloudTrail** provides the foundation for the data. Without CloudTrail, GuardDuty has no visibility at the API level. Enabling CloudTrail ensures that all activity within the account is recorded.

# Sample Alert Email:


🚨 GuardDuty Alert: Trojan Activity Detected

🔍 Type: Trojan:EC2/BlackholeTraffic
💡 Description: The EC2 instance i-99999999 is communicating with a blackholed IP address 198.51.100.0 on port 80. Compromised IP addresses are often blackholed, and hence communication with such an IP could be an indication of a compromised EC2 instance.

🖥 Instance ID: i-99999999
🔐 Instance Profile: arn:aws:iam::9--------6:instance-profile/generated
🌐 Public IP: ---
➡️ Remote IP: ---
📍 Region: us-east-1
🕒 Time: 2026-03-03 17:18:00 UTC

🧠 Recommendation:
Isolate or stop the EC2 instance and investigate for malware or unauthorized traffic.

📘 Learn more: https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings.html


--
If you wish to stop receiving notifications from this topic, please click or visit the link below to unsubscribe:
https://sns.us-east-1.amazonaws.com/unsubscribe.html?SubscriptionArn=arn:aws:sns:us-east-1:911593386236:GuardDuty-Threat-Alerts:cd1afc88-6c64-4cb7-b3e4-b78d9287af9f&Endpoint=sai513ram@gmail.com

Please do not reply directly to this email. If you have any questions or comments regarding this email, please contact us at https://aws.amazon.com/support

# CloudTrail Configuration

<img width="2878" height="1558" alt="Screenshot 2026-03-03 165345" src="https://github.com/user-attachments/assets/1009fd55-ae92-4391-a1d3-cc3f75d4d502" />

# GuardDuty Configurations

<img width="2876" height="1571" alt="Screenshot 2026-03-03 165310" src="https://github.com/user-attachments/assets/7112116a-2823-4081-9f98-dc55a203b23a" />

# GuardDuty Findings

<img width="2879" height="1559" alt="Screenshot 2026-03-03 165216" src="https://github.com/user-attachments/assets/b8fc0bd6-93e3-4ce6-82a4-f331e0fec83d" />

# Email Alert


<img width="2311" height="1188" alt="image" src="https://github.com/user-attachments/assets/7fa0166b-3656-4e71-9ae1-522c2980b29d" />
