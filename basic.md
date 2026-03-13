### Notes

#### IAM : Users and groups

    - Can create users in groups
    - Allows policies to define permission to the users
    - least privilege principle - Never allow permissions to a user more than he requires

#### IAM Roles 
    - Some AWS services will need to perform actions on your behalf and for that we will assign permissions to those 
    AWS Services with IAM Roles
    - Examples : EC2 Instance Roles, Lambda Function Roles

#### EC2 User Data Script
    - Runs when a machine starts and like a initialiser script for EC2
    - It runs with the root user (Cautious)

#### Using IAM roles for EC2
    - We can assign IAM roles with our permissions on an EC2 instance, so whenver we run a aws command within our
    EC2 instance it would have by default the IAM permission we setup within our custom IAM role.

#### EBS (Elastic Block Store)
    - Is a network drive accessed over network to give EC2 features of hard drive but over network
    - Can only be bound to a instance one at a time and bound to a single Availibily Zone.

#### AMI (Amazon Machine Image)
    - Custom OS with prebuild binaries  
    - We can build them using one EC2 instance in one AZ and copy over to another AZ

#### EC2 Instance Store
    - Physical drives attached to your EC2
    - Ec2 with instance stored, the data will be deleted whenever instance is destroyed.

#### EFS - Elastic File System
    - Expensive but faster I/O operations
    - Need to setup security groups

#### S3 Encryption
    - SSE-S3 : Encryption using keys handled by AWS and object is encrypted server side. Encryption Type is AES256.
    - SSE-KMS : Leverage AWS KMS (Key Management Service) to manage encryption keys
    - SSE-C : When we want to manage our own encryption keys

#### MFA on Delete S3
    - We can set MFA on critical actions such as objects delete on s3

#### S3 Logs
    - Any requests to S3 (any logs authorized or unauthorized) will be logged as a file in another S3 bucket.

#### Cloudfront
    - CDN , caches

#### SQS Queue
    - Standard Queue - Unlimited thoroughput and retention is upto 14 days

#### Post exploitation

##### Understanding the user identity
aws sts get-caller-identity
This is always your FIRST command when enumerating credentials. It tells you:
  - UserId: Your user ID
  - Account: The AWS account ID
  - Arn: The full ARN of your identity (user/role)
 
##### Enumerating permissions on a user account
aws iam <action> --user-name <username>

For listing policies attached to a user, you'd use:
  - list-attached-user-policies (for managed policies)
  - list-user-policies (for inline policies)
 
#### Enumerating permissions on a policy
aws iam get-policy-version --policy-arn <arn> --version-id <version>

By default, this gets the default version of the policy:

    aws iam get-policy-version --policy-arn arn:aws:iam::123456789012:policy/SomePolicy --version-id v1
This returns the policy document with all the Effect: Allow and Effect: Deny statements.

#### Enumeration permission of a policy of a inline policy

aws iam get-user-policy --user-name USER --policy-name POLICYNAME


#### More about IAM
    - The "action" field determines what the user is allowed
    - The "resource" field tells where are these perms allowed.

#### Difference b/w IAM , policies , permissions and roles

- IAM Policies : JSON documents that can tell what you are allowed and cannot.
- IAM Users = People/Programs = A user or applications that needs to access AWS.
- IAM Roles : Roles are like temporary access that you could give to IAM users or applications.
- Permissions : Permissions are the result of evaluating all policies attached to your identity.

#### AWS Cognito
    - Login system , allows uers to build authentication systems and allows custom attributes

#### Aws Cloudwatch
    - CloudWatch is a service where every logs from multiple AWS services can be accumulated and reviewed and based on that we can create certain alarms. So for example an alarm can be triggered if EC2 resource is consuming a lot of memory and we can combine multiple alarms together to build a single alarm and use and , OR  conditions on top of that.


#### CloudTrail
    - CloudTrail is enabled by default and it aggregates the history of events and API calls made by an account. It could be anything from console or CLI and we can export the logs from CloudTrail into CloudWatch.
    - We can utilize CloudTrail insights to detect unusual activities. So for example, using our general activity and normal management event, it creates a baseline and if a pattern is breached then it will detect and mark it as malicious or suspicious.
    - Can integrate with eventbridge and can have org level trails

#### AWS Config
    - While services like CloudTrail tell you who made a change, AWS Config tells you what the resource actually looks like now compared to how it looked in the past.
    - AWS Config monitors your infrastructure configuration and checks it against rules. AWS Config marks the resource as: "NON COMPLAINT" It only detects violations.

#### KMS (key management service)
    - Key is managed by AWS
    - Can be integrated with other services like S3 , EBS etc.

#### SSM Parameter Store
    - SSM Parameter Store is a AWS service that stores configuration data and secrets (passwords, API keys, database strings, etc.) as key-value pairs.
    - Basically used for storing simple secrets like API keys, which does not require rotation

#### Secrets Manager
    -  Used for storing sensitive data that requires rotation like database passwords.

#### AWS Shield
    - Protect from DDOS attack

#### AWS Firewall manager
    - Manage rules for all accounts in AWS

#### AWS GuardDuty
    - It uses AI/ML for detecting anomalies within certain API events or DNS or VPC logs.
    - Inputs for GuardDuty can include VPC flow logs, CloudTrail logs which is like all the history of all the API calls and DNS logs. Apart from that optional features can include S3 logs and EBS volume etc. Apart from that we can create automation on top of the R-duty by integrating with EventBridge which can send notification to SNS and can trigger Lambda function.

#### AWS  Inspector
    - Amazon Inspector evaluates security of EC2 instances, container images and lambda functions.
    - For EC2 instances, it analyzes running OS against known vulnerabilities or unintended network accessibility. For container, it does assessment of container images and for lambda function, it identifies vulnerabilities in the function code and package dependencies.

#### AWS macie
    - It utilizes AI for detecting data security and data privacy by discovering and protecting sensitive data in AWS so that your PII details are not clear anywhere in the AWS infrastructure.
    - Can identify finding such as S3 bucket encryption is visible or S3 bucket is public

#### AWS Subnets
    - They are CIDR range within VPC range

#### Public ROute table and internet gateway
    - If we create a public VPC, we want to make sure that we give it Internet access. So when we are creating an Ec2 instance with the VPC, we just created. Even though we have set the inbound rules, the Internet connectivity will not be there. so what we have to do is that we have to create an internet gateway allowing the traffic to flow in and then we need to create a route table and connect it with the internet gateway that we created to enable that if any incoming request is coming we need to route it to the Internet gateway.

#### Bastion Hosts
    - The concept of Bash and Host is that we can allow the public EC2 instance to SSH into the private based EC2 instances. I use SSH within the public and make sure that we allow SSH into the private EC2 instances.

#### Internet Gateway and route table
    - RouteTable is basically a book where we define the destination and where the traffic should redirect to. For example, if you are trying to access a particular IP then it will check against the route table where the network should redirect to.
    – Internet gateway is a component within AWS that allows private or public VPCs to talk to the internet.

#### Network access control list (NACL)
    - They are like a firewall where we can define the inbound and outbound rules. So even if there is a security group assigned to an H2 instance, where we define incoming and outgoing traffic rules, we can on top of that create a NACL which is like a firewall with some control traffic torment to subnets.

#### KMS Grants
    - Whenever using KMS key policy we need to mention the resource manually that would be utilising the keys for a task
    - We could use KMS grants that would grant KMS permission to an account without modifying the KMS key policy itself.

#### Cloudformation and Stack set
    - Using AWS CloudFormation, you can define and update IAM roles, policies, and permissions for many resources at once by modifying the template and updating the stack, so changes propagate automatically.
    - Services deployed using cloudformation are called stack set

#### CloudFront OAC (Origin Access Control)
    - Policy to restrict access 

#### Automation Runbooks
    - Automation runbooks are predefined, executable procedures that automatically perform operational or security tasks in your cloud environment. Instead of a human following a manual checklist during an incident or maintenance event, the system runs the steps automatically.

#### EventBridge
    - We can create cron jobs like for example, for every hour we can create a script on lambda function.
    - We can also create event pattern where we are reacting to certain services doing some action. So for example if a user is trying to login to the root user, he can initiate SMS topic to trigger any notification.
    - You can send events to EventBridge and can trigger automations like SNS notifications or lambda functions.

- Guardduty can detect cloudtrail loggin disabled events and raise as finding, SSH brute-force

- GuardDuty Multi Account - You can create one dedicated admin across multiple Org to manage the findings.

#### Security Hub
    - Central Dashboard to aggregate all findings from various AWS Services like Config, GuardDuty, Inspector, Macie etc. 
    - To enable you must first enable AWS Config
    - Can aggregate data from multiple regions and ORG integration
    - Custom actions within Security Hub allows to create actions with eventbridge

#### AWS Inspector
    - Used to detect security vulnerablities in EC2, lambda functions, and ECS.
    - Use Amazon Linux in EC2 since SSM agent comes pre-installed in it. 

#### Service Logs
    - CloudTrail trails - Trace all API calls
    - Config Rules - Logs for changes
    - CloudWatch Logs - aggregates logs from multiple services
    - VPC Flow logs - Traffic logs within VPC
    - ELB access logs - meta data of req made to ur load balancer
    - CloudFront Logs - Web logs
    - WAF logs - full logging of requsets handled by WAF
    (IMPORTANT) - Can use Athena to analyse logs if stored in S3.

#### Unified Cloudwatch Agent
    - For virtual servers like EC2
    - Collecting addtitional system - level like cpu usage, ram usage etc.
    - To enable , we need to install the cloudwatch agent on the EC2 instances and create an IAM role and attach it to the instance. Once done we need to upload the policy for the agent to SSM store and from there we can watch the logs.
    
#### Cloudwatch Logs
    - The events that flows into CloudWatch Logs are not real-time and happens over a certain period of time. So for having a real-time log event, you can use something called Log Subscriptions.

#### CloudWatch alarm : EC2 Instance Recovery
    - We can create alarm for the filter like instance check where we are checking EC2BM, system status where we are checking the underlying hardware and lastly we can check eBS status where we are checking the health of eBS volume. and if the status check returns unhealthy then we can trigger SNS alarm which will notify us.
    - Based on these alarms, we can create recovery plans like for example auto scaling, termination of EC2N scans or SNS notifications as well as system manager action.

- IMDS
    - IMDS provides credentials automatically to aws ec2 instances
    - You create IAM role and attach to a policy and then attach that policy to the EC2 instance so that it inherits the IAM policy assignment.

- AWS Elastic Beanstalk is a service that lets you deploy and run applications without manually managing the infrastructure.

#### Amazon Athena
    - Serverless , Used to analyze zeta stored in Amazon history and uses SQL language to query the files.
    - For any logs, generally we use it. First we transfer the logs to s3 and then use athena on it.

#### CLoudtrail Insights
    - CloudTrails insights detect unusual activities based on observation of the events that are happening in the account and they try to detect it. and the detection can detect issues like inaccurate resource provisioning, bursts of AWS IAM roles and gaps in maintenance activities

#### Compromised EC2

Given a setup where there are two main centers in auto scraping group and the auto scraping group is then connected to a load balancer, if one of the instances within the auto scraping group is compromised how do we deal with that?

So the answer to this scenario is . The first thing and few things that we need to remember is that when an instance is in an auto scaling group, if one instance is mild and healthy then auto scaling will automatically delete and spawn a new instance. So we don't want that and we want to preserve all the evidence that we can. So the first step is that we want to take the instance that is unhealthy or malicious out of the autoscaling group. And then also we want the traffic to not reach the infected instance. So we want to remove the instance from the load balancer as well. then we want to isolate the instance so that there is no inbound and mobile traffic and we want to preserve all the evidences. So for example, we can create a snapshot of the bus using AWS Elastic Block Store where we are taking the snapshot of the bus and we can also snapshot the block from cloud trail, VPC logs etc. and finally we would let the auto scaling group replace the infected instance

1 Remove from load balancer
2 Stop auto scaling termination
3 Isolate instance
4 Snapshot disks
5 Investigate logs
6 Replace instance
7 Fix root cause

#### Compromised AWS User or IAM role

Generally the steps taken for both the cases remains the same. So, the first step starts with revoking the access to console and access key which is submitted by STS. It could be temporary keys and formal keys as well. So we need to disable them and also as an additional method we can also disable the MFA device. Apart from that we need to keep all the evidences so we do not want to delete the user directly and furthermore we want to check the CloudTrail logs if there was some actions taken by the infected user and take it actions accordingly.

#### Compromised EC2 Keys

If we get our EC2 instances compromised, so we need to remove the public key within the EC2 instances. And that's just it but if we want to automate it, we can use SSM run commands to automate the process of adding and deleting the public keys on EC2 instances.

#### Accesss booting issues in EC2

We can troubleshoot boot, troubleshoot the network configuration and analyze the reboot issues using serial console which is turned off by default but we can activate it. And we can have only one active session for EC2 instance. One important thing to remember is that we need to set up OS user in password.

#### System Manager

Remote control + automation for servers
AWS Systems Manager is a centralized tool for managing, automating, and accessing servers without directly logging into them.

- The concept of SSM documents and SSM commands are basically scripts that are made in JSON that you can run on entirety of the EC2 instances.

#### SSM Inventory and State manager

SSM inventory collects metadata from your managed instance, it could be from any region or multiple accounts. And the metadata includes details like software that is installed, OS drivers configuration installed update, running services etc.

State manager is the process of automating your managed instances in a state that you define. It could be bootstrapping instances with a software or OS update. and uses SSM documents which is like the concept of running an automation one fleet of instances.

#### SSM patch manager

We can apply patches to all the suite of in-c2 instances by grouping them and using the SSM document and run command.

#### SSM Session manager

Session Manager is a way to execute command on EC2 instances without having the formal access like SSH keys or signing with support 22. It just allows a user with correct IAM role to execute shell command on any EC2 instance running SSM agent.


> Which is the best solution to help you automatically revoke unused and expired IAM Access Keys?

AWS Config Remediation with SSM Automation Document is the correct choice because it allows for automated compliance checks and remediation actions, ensuring that unused and expired IAM Access Keys are promptly revoked in a reliable and efficient manner.

#### IMPORTANT DISTINCTION B/w SSM automation and run command
    - SSM run command runs inside the EC2 instances and it is used to run commands on the instance OS.
    - SSM automation do not run inside EC2 necessarily. They are workflow engine that can call AWS API.

#### S3 and cloudfront
    - In order to protect and user to directly access S3 bucket content directly, and we want to make sure that only CloudFront instances are allowed to access the objects in a bucket. Then we apply a concept which is called OAC, which stands for Origin Access Control, which basically blocks anything within a tree that tries to directly access the objects but rather only allows a path where a user requests data from CloudFront and CloudFront signs a request and sends it to bucket and bucket checks the origin and then return back.

#### AWS WAF
    - It can be deployed on the following resources. CloudFront, API Gateway, Application Load Balancer, AppSync which is GraphQL API, Cognito User Pool, AppRunner, Verified Access, Amplify
    - WAF cannot be used for DDoS protection. We should use AWS Shield 

#### AWS Firewall manager
    - It is in dashboard where all the aggregated resources can be managed for example, load balancer, WAF setting, AWS need, security group, Amazon route 53.

#### AWS SES (Simple email service)
    - It gives you ability to send emails, mark emails and check the metrics whether how many emails were opened and responded.

#### IAM permission boundaries
    - We can use elevated permission boundaries to restrict a higher authorized admin to have certain boundaries in terms of permissions so that he or she cannot escalate their permission.

#### IAMPASS role
    - Allows a IAM user to pass roles to an AWS services

#### IAM Access analyser
    - It's used to find which resources are shared externally from your own account or organization. So you basically define a zone of trust where you define your AWS account or AWS organization and anything that is accessible outside is a finding in itself.

#### AWS Cognito User Pools
    - It is the service that can have a database of users and we can allow users to sign in with their username and password.


#### MISC

  - IAM user = permanent identity with long-term credentials
  - IAM role = temporary identity that anyone (human, service, external user) can borrow if the trust policy allows it

  - So, when we want to consider a user to allow assuming a role, we want to make sure that we are setting the principle on the trust policy. And secondly, that we want to make sure that the user who wants to assume has relative assume role permission set on his identity policy.

`
  STS tokens are not stored anywhere. AWS has no list of "active sessions" to delete. So you can't revoke them directly.                                                                                                                                                                                                         
  The trick is: every STS token contains a TokenIssueTime — the timestamp of when it was issued. You can add a deny policy to the role that says:                                                                                                                                                                                                                                         
  "Deny any request where the token was issued BEFORE right now."

  {
    "Effect": "Deny",
    "Action": "*",
    "Resource": "*",
    "Condition": {
      "DateLessThan": {
        "aws:TokenIssueTime": "2026-03-11T18:00:00Z"
      }
    }
  }

  This inline policy says: any token issued before 6pm today is denied. Bob's stolen tokens were issued before that time → they stop working immediately. New tokens issued after that timestamp work fine.

  In the AWS console, this is the "Revoke active sessions" button on a role — it does exactly this automatically, setting the timestamp to right now.
`

> Trust Policy is basically defining who is allowed to assume a role.


-----

Question : You're building a mobile game. Players log in with their Google account. After login, they need to read/write their save data in a personal S3 folder. Each player should only see their own folder.
What AWS services would you use, and how would you ensure each player only accesses their own data? Hint — one of the IAM condition keys we listed is the key to the S3 restriction.

Answer : 

  {
    "Effect": "Allow",
    "Action": ["s3:GetObject", "s3:PutObject"],
    "Resource": "arn:aws:s3:::game-saves/${cognito-identity.amazonaws.com:sub}/*"
  }

  The ${cognito-identity.amazonaws.com:sub} is a policy variable — it gets replaced at evaluation time with the actual Cognito Identity ID of the authenticated user. So player A's token can only access game-saves/us-east-1:abc123/* and player B can only access their own prefix.

  This is ABAC in practice — access controlled by the user's identity attribute, not by creating separate policies per user.

------

>  External ID = the secret handshake between you and the SaaS. The SaaS knows it, you embedded it in the lock. Nobody else can open the door.

>   Any scenario asking "how do you ensure AWS service X only has minimum permissions" → service-linked roles are the answer. AWS manages them, you can't accidentally over-permission them.

RBAC = "Alice gets the Developer role" — someone made a decision
ABAC = "whoever has team=payments gets payments resources" — tags make the decision automatically
