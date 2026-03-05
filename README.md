Detecting EC2 IAM Role Abuse using AWS CloudTrail

#Overview

This project demonstrates how attackers can abuse IAM role credentials obtained from an EC2 instance and how such activity can be detected using AWS CloudTrail logs.

The goal of this project is to simulate a real-world cloud security scenario where an attacker gains access to temporary AWS credentials and performs suspicious API actions.

#Attack Scenario

1. An EC2 instance is configured with an IAM role.
2. An attacker exploits an application vulnerability (for example SSRF).
3. The attacker accesses the EC2 metadata service.
4. Temporary IAM role credentials are retrieved.
5. The attacker uses these credentials to perform AWS API actions.

#Example Suspicious Actions

Some API calls that may indicate abuse include:

- CreateUser
- AttachUserPolicy
- CreateAccessKey
- ListBuckets
- StopLogging

These actions are unusual for most application roles and can indicate privilege escalation or persistence attempts.

#CloudTrail Detection Strategy

Detection can be based on identifying abnormal API activity from an assumed role.

Key signals include:

- userIdentity.type = AssumedRole
- High-risk IAM API calls
- Source IP outside expected infrastructure
- Role performing actions outside its normal behavior

#Security Impact

If an attacker successfully abuses an EC2 role, they may be able to:

- Create new IAM users
- Escalate privileges
- Access sensitive data
- Disable security monitoring

#Mitigation Strategies

Recommended security practices include:

- Apply least privilege to IAM roles
- Restrict metadata access using IMDSv2
- Monitor CloudTrail logs for suspicious activity
- Use detection rules for high-risk IAM actions

#Learning Outcome

This project demonstrates how cloud attackers abuse IAM roles and how security engineers can detect such activity using AWS logging mechanisms.
