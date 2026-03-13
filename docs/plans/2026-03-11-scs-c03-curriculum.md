# SCS-C03 Complete Curriculum

> **Exam:** AWS Certified Security - Specialty (SCS-C03)
> **Effective:** December 2, 2025
> **Questions:** 65 (50 scored + 15 unscored)
> **Types:** Multiple choice, multiple response, ordering, matching
> **Passing:** 750/1000 | **Time:** 170 minutes
>
> Status legend: ✅ covered | 🔶 partially covered | ⬜ not started

---

## Domain 4: Identity & Access Management (20%) — HIGHEST WEIGHT

### 4.1 IAM Fundamentals
- ✅ IAM users — long-term credentials, access keys, password policies
- ✅ IAM groups — policy attachment, no nesting, no trust policies
- ✅ IAM roles — permissions policy + trust policy, temporary credentials
- ✅ IAM policies — managed vs customer-managed vs inline
- ✅ PARC model — Principal, Action, Resource, Condition

### 4.2 All 7 Policy Types (must know every one)
- ✅ Identity-based policies — attached to users, groups, roles
- ✅ Resource-based policies — S3 bucket policies, KMS key policies, SQS queue policies, Lambda resource policies, SNS topic policies, API Gateway resource policies
- ✅ Permission boundaries — ceiling/intersection concept, delegated IAM pattern
- ✅ Service Control Policies (SCPs) — deny vs allow, inheritance through OU tree, cannot grant permissions
- ✅ Resource Control Policies (RCPs) — NEW in C03, permission boundaries for resource types across org
- ✅ Access Control Lists (ACLs) — S3 ACLs, network ACLs
- ✅ Session policies — passed when creating STS sessions, intersection with identity policies

### 4.3 Policy Evaluation Logic
- ✅ Evaluation order — explicit deny → SCPs → RCPs → resource-based → identity-based → boundaries → session
- ✅ Same-account evaluation — identity OR resource policy can grant (OR logic)
- ✅ Cross-account evaluation — BOTH identity AND resource policy must grant (AND logic), deep scenarios
- ✅ VPC endpoint policies — additional filter layer
- ✅ Implicit deny vs explicit deny
- ✅ Policy evaluation with multiple policy types combined

### 4.4 IAM Roles — Deep Mechanics
- ✅ Trust policies — Principal types (AWS service, user, account, federated)
- ✅ AssumeRole flow — two-check handshake (trust policy + identity policy)
- ✅ Cross-account role assumption — trust policy in target + identity policy in source
- ✅ Role chaining — assuming a role from an already-assumed role, 1-hour max session limit
- ✅ Service-linked roles — pre-defined by AWS services, cannot modify permissions
- ✅ Instance profiles — wrapper for EC2 role attachment
- ✅ Execution roles — Lambda, ECS task roles, ECS task execution roles, EKS IRSA (IAM Roles for Service Accounts)
- ✅ Confused deputy problem — External ID in trust policy to prevent cross-account spoofing
- ✅ IAM Roles Anywhere — NEW, X.509 certificate-based role assumption for on-prem workloads

### 4.5 STS (Security Token Service)
- ✅ AssumeRole — cross-account, same-account role switching
- ✅ AssumeRoleWithSAML — SAML 2.0 federation (Active Directory, Okta, etc.)
- ✅ AssumeRoleWithWebIdentity — OIDC federation (Google, Facebook, Cognito)
- ✅ GetSessionToken — MFA enforcement for IAM users
- ✅ GetFederationToken — custom identity broker scenarios
- ✅ Temporary credentials — AccessKeyId + SecretAccessKey + SessionToken
- ✅ Session duration — default 1hr, max 12hr (36hr with config), 1hr max for role chaining
- ✅ Revoking sessions — aws:TokenIssueTime condition, stateless nature of STS tokens

### 4.6 Federation & SSO
- ✅ SAML 2.0 federation — IdP → AWS flow, trust relationship setup, SAML assertion, role mapping
- ✅ Web identity federation — OIDC providers, token exchange flow
- ✅ Custom identity broker — for non-SAML/OIDC environments
- ✅ AWS IAM Identity Center (SSO) — multi-account SSO, permission sets, integration with external IdPs, attribute-based access
- ✅ Amazon Cognito User Pools — user directory, sign-up/sign-in, MFA, SAML/OIDC federation, JWT tokens, hosted UI, custom auth flows
- ✅ Amazon Cognito Identity Pools — temporary AWS credentials for authenticated/unauthenticated users, role mapping rules
- ✅ User Pools vs Identity Pools — authentication vs authorization distinction
- ✅ AWS Directory Service — Managed Microsoft AD, AD Connector, Simple AD, trust relationships

### 4.7 Authorization Controls
- ✅ Amazon Verified Permissions — NEW, fine-grained authorization using Cedar policy language
- ✅ ABAC (Attribute-Based Access Control) — using tags for access decisions, aws:PrincipalTag, aws:ResourceTag
- ✅ RBAC (Role-Based Access Control) — role-per-job-function pattern
- ✅ ABAC vs RBAC — when to use which, exam scenarios

### 4.8 IAM Condition Keys (must memorize)
- ✅ aws:SourceIp — restrict by IP address
- ✅ aws:SourceVpc — restrict to specific VPC
- ✅ aws:SourceVpce — restrict to specific VPC endpoint
- ✅ aws:PrincipalOrgID — restrict to organization members
- ✅ aws:SecureTransport — enforce HTTPS
- ✅ aws:RequestedRegion — restrict to specific regions
- ✅ aws:PrincipalTag / aws:ResourceTag — ABAC
- ✅ aws:MultiFactorAuthPresent — enforce MFA
- ✅ aws:MultiFactorAuthAge — enforce recent MFA
- ✅ aws:TokenIssueTime — session revocation
- ✅ aws:CalledVia — restrict to calls made through specific services
- ✅ aws:PrincipalAccount — restrict by account
- ✅ iam:PermissionsBoundary — enforce boundary on role creation
- ✅ s3:x-amz-server-side-encryption — enforce encryption
- ✅ kms:ViaService — restrict KMS key usage to specific services

### 4.9 IAM Security Tools & Troubleshooting
- ✅ IAM Access Analyzer — identifies resources shared externally, validates policies, generates least-privilege policies, unused access findings
- ✅ IAM Policy Simulator — test and troubleshoot policies before deployment
- ✅ IAM credential report — CSV report of all users and their credential status
- ✅ IAM access advisor — shows last-accessed service data for right-sizing permissions
- ✅ CloudTrail for IAM troubleshooting — reading denied API calls

### 4.10 IAM Best Practices & Exam Patterns
- ✅ Least privilege principle — practical implementation
- ✅ Separation of duties — multi-account patterns
- ✅ Root user management — MFA, monitoring via CloudTrail, limiting usage, break-glass procedures
- ✅ Centralized root access for member accounts (Organizations)
- ✅ Access key rotation — automation patterns
- ✅ S3 presigned URLs — temporary access, inherits signer's permissions
- ✅ CloudFront signed URLs vs signed cookies — IP restrictions, expiry, multiple objects
- ✅ S3 presigned URLs vs CloudFront signed URLs — when to use which
- ✅ Delegated administrator accounts — Organizations feature

---

## Domain 5: Data Protection (18%)

### 5.1 AWS KMS — Deep Dive
- ✅ Key types — AWS owned keys, AWS managed keys, customer managed keys (CMKs)
- ✅ Key material options — AWS-generated, customer-imported (wrapping key + import token), CloudHSM custom key store, External Key Store (XKS)
- ✅ Key policies — resource policy on the key, PRIMARY access control mechanism
- ✅ Key policy + IAM policy interaction — both needed unless key policy grants to account root
- ✅ KMS grants — temporary delegated permissions, GranteePrincipal, RetiringPrincipal
- ✅ Encryption context — additional authenticated data (AAD), logged in CloudTrail
- ✅ Envelope encryption — data key encrypts data, KMS key encrypts data key, GenerateDataKey API
- ✅ Key rotation — automatic (annual for AWS managed, configurable for CMK), manual rotation via alias swapping
- ✅ Multi-region keys — replicas across regions, same key material, different ARNs
- ✅ Symmetric vs asymmetric keys — when to use which
- ✅ Key states — enabled, disabled, pending deletion, pending import
- ✅ Key deletion — 7-30 day waiting period, imported keys immediate deletion, CloudWatch alarm for usage during waiting period
- ✅ KMS permissions — kms:Encrypt, kms:Decrypt, kms:GenerateDataKey, kms:ReEncrypt, kms:CreateGrant, kms:DescribeKey
- ✅ Cross-account key sharing — key policy grants + IAM policy in other account
- ✅ Region-specific nature — keys are regional (except multi-region keys)
- ✅ kms:ViaService — restrict key usage to specific AWS services
- ✅ Imported key material — differences from AWS-generated, no auto-rotation, can set expiration

### 5.2 AWS CloudHSM
- ✅ Dedicated HSM hardware — single-tenant, you own the keys
- ✅ FIPS 140-2 Level 3 validated (vs KMS = Level 2)
- ✅ Symmetric + asymmetric key support
- ✅ Custom key store integration with KMS
- ✅ Cluster architecture — HA across AZs
- ✅ Use cases — SSL/TLS offloading, Oracle TDE, code signing, custom PKI
- ✅ KMS vs CloudHSM decision criteria

### 5.3 Secrets & Certificate Management
- ✅ AWS Secrets Manager — secret storage, automatic rotation (Lambda-based), database credential rotation (RDS, Redshift, DocumentDB), multi-region replication, resource-based policies
- ✅ SSM Parameter Store — String, StringList, SecureString (KMS-encrypted), hierarchical paths, no auto-rotation, free tier
- ✅ Secrets Manager vs Parameter Store — when to use which
- ✅ AWS Certificate Manager (ACM) — public SSL/TLS provisioning, auto-renewal, DNS/email validation, integrations (CloudFront, ALB, NLB, API Gateway — NOT EC2 directly), cannot export ACM-issued certs
- ✅ AWS Private Certificate Authority (ACM PCA) — private CA hierarchy, private cert issuance, CRL, OCSP

### 5.4 Data-at-Rest Encryption
- ✅ S3 encryption — SSE-S3 (AES-256), SSE-KMS (audit trail), SSE-C (customer-provided keys), client-side encryption
- ✅ S3 default encryption — bucket-level enforcement
- ✅ S3 bucket keys — reduce KMS API calls and cost
- ✅ EBS encryption — AES-256, KMS-based, snapshot encryption, encrypted AMI copying, default encryption setting
- ✅ RDS/Aurora encryption — KMS at rest, SSL/TLS in transit, IAM database authentication, encrypted read replicas
- ✅ DynamoDB encryption — AWS owned (default), AWS managed, customer managed; DynamoDB Encryption Client
- ✅ EFS encryption — at rest (KMS) and in transit (TLS mount helper)
- ✅ Redshift encryption — KMS or CloudHSM, audit logging
- ✅ OpenSearch encryption — node-to-node encryption, at-rest encryption
- ✅ Kinesis encryption — server-side encryption with KMS

### 5.5 Data-in-Transit Encryption
- ✅ TLS/SSL everywhere — enforcing via policies
- ✅ ELB security policies — predefined vs custom, cipher suites, Perfect Forward Secrecy (ECDHE)
- ✅ PrivateLink — private API access without internet traversal
- ✅ VPC endpoints — gateway (S3, DynamoDB) vs interface (PrivateLink)
- ✅ Client VPN with TLS
- ✅ Inter-resource encryption (NEW in C03) — EMR, EKS, SageMaker inter-node encryption, Nitro encryption (hardware-level)
- ✅ MACsec on Direct Connect — Layer 2 encryption
- ✅ AWS Verified Access — TLS-based zero trust

### 5.6 Data Protection Mechanisms
- ✅ S3 Object Lock — WORM model, Governance mode vs Compliance mode, retention periods, legal hold
- ✅ S3 Glacier Vault Lock — immutable vault policies, WORM compliance
- ✅ S3 versioning — accidental deletion protection, MFA Delete
- ✅ S3 lifecycle policies — automated transitions and expirations
- ✅ S3 Block Public Access — account-level and bucket-level
- ✅ S3 access logging — server access logs
- ✅ S3 Access Points — named network endpoints with own policies
- ✅ S3 bucket policies — resource-based policies, aws:SecureTransport condition
- ✅ S3 CORS — cross-origin resource sharing configuration
- ✅ AWS Backup — centralized backup, cross-account, cross-region, vault lock (WORM)
- ✅ AWS DataSync — secure data replication
- ✅ Amazon Data Lifecycle Manager — EBS snapshot lifecycle

### 5.7 Data Masking & Classification (NEW in C03)
- ✅ CloudWatch Logs data protection policies — PII masking in logs
- ✅ SNS message data protection — PII detection/masking in messages
- ✅ Amazon Macie — ML-based sensitive data discovery in S3, PII/PHI/PCI detection
- ✅ Data classification levels — public, internal, confidential, regulatory

---

## Domain 3: Infrastructure Security (18%)

### 3.1 VPC Security — Network Layer
- ✅ VPC architecture — subnets (public/private), route tables, internet gateways, NAT gateways, CIDR blocks
- ✅ Security Groups — stateful, instance-level, allow-only, evaluate ALL rules
- ✅ Network ACLs (NACLs) — stateless, subnet-level, allow + deny, rules processed in ORDER, ephemeral ports
- ✅ Security Groups vs NACLs — when to use which, exam traps
- ✅ VPC Flow Logs — capture at VPC/subnet/ENI level, source/dest IPs, protocol, ports, accept/reject, CloudWatch or S3 destination
- ✅ Transit Gateway Flow Logs — cross-TGW traffic
- ✅ VPC endpoints — Gateway (S3, DynamoDB) vs Interface (PrivateLink), endpoint policies
- ✅ VPC endpoint policies — additional layer of access control
- ✅ VPC Peering — direct VPC-to-VPC, no transitive routing, cross-account
- ✅ VPC Traffic Mirroring — copy EC2 traffic to security appliance (IDS/IPS), target is ENI or NLB
- ✅ Network segmentation — north/south vs east/west traffic, isolated subnets
- ✅ AWS Reachability Analyzer — verify/validate network paths between resources, identify unintended access

### 3.2 AWS Network Firewall
- ✅ Stateful managed firewall — IDS/IPS for VPCs
- ✅ Suricata-compatible rules
- ✅ Domain filtering — allow/deny specific domains
- ✅ Protocol-level inspection
- ✅ Integration with Firewall Manager for centralized management
- ✅ TLS inspection — decrypt, inspect, re-encrypt HTTPS traffic for deep packet inspection

### 3.3 Hybrid & Multi-Cloud Connectivity
- ✅ AWS Site-to-Site VPN — IPsec tunnels, private IP VPN over Direct Connect
- ✅ AWS Direct Connect — dedicated private connection, encryption options
- ✅ MACsec on Direct Connect — Layer 2 encryption
- ✅ AWS Transit Gateway — regional hub for VPC/VPN/Direct Connect interconnection
- ✅ AWS Client VPN — managed client-based VPN
- ✅ AWS Verified Access — zero-trust without VPN (NEW emphasis in C03)

### 3.4 Edge & Application Security
- ✅ Amazon CloudFront — edge caching, DDoS absorption, OAI vs OAC (Origin Access Control), signed URLs/cookies, custom headers, geo-restriction, field-level encryption, TLS config
- ✅ AWS WAF — Layer 7 protection, web ACLs, rule groups; IP/geo/string match/regex/SQLi/XSS conditions; rate limiting; managed rules (AWS + Marketplace); integration with CloudFront, ALB, API Gateway, AppSync
- ✅ AWS Shield Standard — free, all accounts, Layer 3/4 DDoS protection
- ✅ AWS Shield Advanced — $3K/mo, DRT team, cost protection, advanced metrics, WAF included, health-based detection
- ✅ Shield Standard vs Advanced — when to use which
- ✅ AWS Firewall Manager — centralized WAF/Shield/SG/Network Firewall/DNS Firewall management across Organizations
- ✅ Route 53 — DNS health checks, DNSSEC, Resolver DNS Firewall (domain filtering)
- ✅ AWS Global Accelerator — anycast IP, edge DDoS protection, health-based routing
- ✅ DDoS mitigation architecture — CloudFront + Shield + WAF + auto-scaling + Route 53
- ✅ Lambda@Edge vs CloudFront Functions — edge compute for JWT validation, header manipulation, bot detection

### 3.5 Compute Security
- ✅ EC2 hardening — AMI hardening, key pairs, dedicated instances/hosts
- ✅ EC2 Instance Metadata Service — IMDSv1 vs IMDSv2, hop limit, why v2 is required
- ✅ Nitro system — hardware-based security, Nitro Enclaves for isolated compute
- ✅ Instance profiles — wrapper for EC2 role attachment
- ✅ Amazon Inspector — vulnerability scanning for EC2, ECR containers, Lambda; CVE detection; CIS benchmarks; network reachability
- ✅ SSM Patch Manager — automated patching, patch baselines, compliance dashboard
- ✅ SSM Session Manager — secure shell without SSH keys or bastion hosts, no inbound ports, TLS 1.2, audit logging
- ✅ EC2 Instance Connect — browser-based SSH
- ✅ EC2 Image Builder — automated AMI pipeline
- ✅ Container security — ECR image scanning, ECS task roles, ECS task execution roles, EKS pod security, EKS IRSA, Fargate isolation

### 3.6 API & Application Security
- ✅ API Gateway — throttling (10K req/sec, 5K burst), caching, authorization (IAM, Cognito, Lambda authorizers), mutual TLS, resource policies, WAF integration, logging
- ✅ ELB — ALB/NLB/CLB, TLS termination, security policies, PFS (ECDHE), WAF integration (ALB only)
- ✅ Lambda security — execution roles, resource-based policies, VPC-attached Lambda, environment variable encryption

### 3.7 GenAI Infrastructure Security (NEW in C03)
- ✅ Amazon Bedrock guardrails — content filters, denied topics, word filters
- ✅ PII detection/redaction in Bedrock
- ✅ OWASP Top 10 for LLM Applications — prompt injection, data leakage, insecure output handling
- ✅ Contextual grounding checks
- ✅ Automated Reasoning checks (hallucination prevention)
- ✅ Amazon Q Developer — code security scanning in pipeline
- ✅ Amazon CodeGuru Security — vulnerability detection in code
- ✅ Bedrock Model Invocation Logging — audit trail for all AI model calls (NEW in C03)
- ✅ Amazon SageMaker security — VPC isolation for training jobs, IAM execution roles, KMS encryption of model artifacts

---

## Domain 1: Detection (16%)

### 1.1 Amazon GuardDuty — Deep Dive
- ✅ Threat detection sources — CloudTrail management events, CloudTrail S3 data events, VPC Flow Logs, DNS logs
- ✅ Finding types — Backdoor, CryptoCurrency, Trojan, UnauthorizedAccess, Recon, Stealth, etc.
- ✅ Extended Threat Detection (NEW in C03) — multi-stage attack correlation, AI/ML attack sequence identification
- ✅ Runtime Monitoring — EKS, ECS, EC2 OS-level analysis
- ✅ Malware Protection for EC2 — EBS volume scanning
- ✅ Malware Protection for S3 — object scanning
- ✅ S3 Protection — object-level API monitoring
- ✅ EventBridge integration — automation triggers
- ✅ Multi-account management — delegated administrator
- ✅ Suppression rules — filtering out expected findings

### 1.2 AWS Security Hub
- ✅ Centralized findings dashboard — aggregates from GuardDuty, Macie, Inspector, Firewall Manager, IAM Access Analyzer
- ✅ Security standards — CIS AWS Benchmarks, PCI DSS, AWS Foundational Security Best Practices, NIST 800-53
- ✅ Custom insights — custom groupings and filters
- ✅ ASFF (AWS Security Finding Format) — normalized finding format
- ✅ Cross-account aggregation — delegated administrator
- ✅ Automated actions — EventBridge + Lambda
- ✅ Integration with Detective for investigation

### 1.3 Amazon Macie
- ✅ ML-based sensitive data discovery in S3
- ✅ PII, PHI, PCI data identification
- ✅ Custom data identifiers — regex-based
- ✅ Automated discovery jobs
- ✅ EventBridge + SNS integration
- ✅ Multi-account management

### 1.4 Amazon Inspector
- ✅ EC2 vulnerability scanning — CVEs, CIS benchmarks
- ✅ Container image scanning — ECR
- ✅ Lambda function scanning
- ✅ Network reachability findings
- ✅ Continuous scanning vs on-demand
- ✅ Integration with Security Hub

### 1.5 Amazon Detective
- ✅ Root cause analysis — investigation AFTER a finding
- ✅ Graph-based analysis — CloudTrail, VPC Flow Logs, GuardDuty findings
- ✅ Visualization of entity relationships
- ✅ When to use Detective vs GuardDuty vs Security Hub

### 1.6 AWS CloudTrail — Deep Dive
- ✅ Management events vs data events vs Insights events
- ✅ Organization trails — automatic logging across all member accounts
- ✅ Multi-region trails
- ✅ Log file integrity validation — SHA-256 hashing, digital signing, digest files
- ✅ S3 + CloudWatch Logs destinations
- ✅ SNS notifications on log delivery
- ✅ CloudTrail Lake — SQL-based querying of events
- ✅ CloudTrail Insights — anomalous API activity detection (unusual volume, error rates)
- ✅ Event selectors — filtering which events to log
- ✅ Protecting CloudTrail logs — SCPs, S3 Object Lock, bucket policies

### 1.7 Amazon CloudWatch
- ✅ Metrics, alarms, dashboards
- ✅ CloudWatch Logs — log groups, log streams, metric filters, retention policies
- ✅ CloudWatch Logs Insights — SQL-like queries
- ✅ CloudWatch Agent — custom metrics and logs from EC2
- ✅ CloudWatch Alarms — threshold-based, anomaly detection, composite alarms
- ✅ CloudWatch data protection policies — PII masking in logs (NEW in C03)
- ✅ Cross-account monitoring

### 1.8 Amazon Security Lake (NEW in C03)
- ✅ Centralized security data lake
- ✅ OCSF (Open Cybersecurity Schema Framework) format — normalized data
- ✅ Auto-collection from AWS services + third-party sources
- ✅ Apache Parquet format
- ✅ Cross-account and cross-region aggregation
- ✅ Subscriber integration for SIEM/analytics

### 1.9 Additional Logging
- ✅ VPC Flow Logs — format, filtering, destinations
- ✅ Transit Gateway Flow Logs
- ✅ Route 53 Resolver logs — DNS query logging
- ✅ S3 access logging
- ✅ ELB access logs
- ✅ CloudFront access logs
- ✅ API Gateway logging — execution logs, access logs
- ✅ Lambda logging — CloudWatch Logs integration
- ✅ Amazon Athena — querying logs in S3 (CloudTrail, VPC Flow Logs)
- ✅ Amazon OpenSearch — log analysis, real-time dashboards
- ✅ Amazon Managed Grafana — visualization

### 1.10 Detection Comparison: GuardDuty vs Macie vs Inspector vs Detective
- ✅ GuardDuty = active threat detection from logs
- ✅ Macie = sensitive data discovery in S3
- ✅ Inspector = vulnerability scanning of compute
- ✅ Detective = investigation/root cause analysis AFTER a finding

---

## Domain 6: Security Foundations & Governance (14%)

### 6.1 AWS Organizations — Deep Dive
- ✅ Multi-account management — OUs, consolidated billing
- ✅ Service Control Policies (SCPs) — deny vs allow, inheritance through OU tree, precedence
- ✅ Resource Control Policies (RCPs) — NEW in C03, resource-centric control
- ✅ AI service opt-out policies — NEW
- ✅ Declarative policies — NEW
- ✅ Tag policies — enforce tagging standards
- ✅ Backup policies — centralized backup rules
- ✅ SCP inheritance chain — root → OU → sub-OU → account
- ✅ SCP does NOT affect management account
- ✅ Delegated administrator accounts — Security Hub, GuardDuty, etc.
- ✅ Centralized root access management for member accounts

### 6.2 AWS Control Tower
- ✅ Landing zone setup — best-practice multi-account environment
- ✅ Guardrails/controls — preventive (SCPs), detective (Config Rules), proactive (CloudFormation hooks)
- ✅ Mandatory vs optional vs custom controls
- ✅ Account Factory — automated account vending
- ✅ Security Hub integration
- ✅ Customizations for Control Tower (CfCT)
- ✅ New vs existing environment deployment

### 6.3 AWS Config
- ✅ Resource inventory and configuration history
- ✅ Configuration change notifications
- ✅ Config Rules — 400+ managed rules, custom rules (Lambda-based)
- ✅ Conformance packs — pre-built compliance rule sets
- ✅ Auto-remediation — SSM Automation documents
- ✅ Multi-account/multi-region aggregation
- ✅ Compliance timeline — visual history of resource compliance
- ✅ AWS Config vs CloudTrail — state tracking vs API logging

### 6.4 Infrastructure as Code Security
- ✅ CloudFormation — stack sets (multi-account/multi-region), drift detection
- ✅ CloudFormation Guard — policy-as-code validation of templates
- ✅ cfn-lint — template linting
- ✅ Service Catalog — curated product portfolios, launch constraints, secure sharing

### 6.5 Compliance & Audit
- ✅ AWS Audit Manager — automated evidence collection, pre-built frameworks (CIS, PCI DSS, GDPR, HIPAA, SOC 2), custom frameworks
- ✅ AWS Artifact — compliance reports/certifications (SOC, PCI, ISO)
- ✅ AWS Well-Architected Framework — Security Pillar
- ✅ Compliance frameworks awareness — PCI DSS, ISO 27001, HIPAA, SOC 1/2, FedRAMP, NIST CSF, FIPS 140-2, GDPR

### 6.6 Resource Sharing & Management
- ✅ AWS Resource Access Manager (RAM) — share resources across accounts (subnets, Transit Gateways, etc.)
- ✅ Resource tagging strategies — mandatory tags, tag policies
- ✅ AWS Firewall Manager — centralized security policy management

### 6.7 Shared Responsibility Model
- ✅ AWS responsibility — security OF the cloud (hardware, network, facilities, hypervisor)
- ✅ Customer responsibility — security IN the cloud (data, IAM, OS patching, encryption, network config)
- ✅ Shared controls — patch management, configuration, awareness

---

## Domain 2: Incident Response (14%)

### 2.1 Incident Response Lifecycle
- ✅ Preparation — design/test response plans, runbooks, provision access, deploy security tools
- ✅ Detection — log correlation, finding validation
- ✅ Containment — network isolation (security group swap, quarantine subnet), blast radius minimization
- ✅ Eradication — removing threats, patching vulnerabilities
- ✅ Recovery — restoring operations, validating remediation
- ✅ Post-incident — lessons learned, runbook improvement

### 2.2 EC2 Compromise Response (heavily tested)
- ✅ Isolation via security group replacement (not modification)
- ✅ EBS snapshot capture for forensics
- ✅ Memory dump acquisition via SSM Run Command
- ✅ Offline analysis in forensic VPC
- ✅ Evidence preservation — snapshot BEFORE changes
- ✅ Do NOT log into compromised instances directly
- ✅ Automated Forensics Orchestrator for Amazon EC2

### 2.3 Credential Compromise Response
- ✅ IAM user key compromise — inactivate keys, delete keys, regenerate
- ✅ Role session compromise — revoke sessions via aws:TokenIssueTime
- ✅ Root user compromise — MFA reset, password reset, check for unauthorized users/policies

### 2.4 Automated Incident Response
- ✅ GuardDuty → EventBridge → Lambda pattern — auto-isolation, snapshot, notify
- ✅ Step Functions for multi-step orchestrated response
- ✅ SSM Automation documents — pre-built remediation runbooks
- ✅ Security Hub automated actions
- ✅ SNS notifications to security team
- ✅ Config Rules auto-remediation

### 2.5 Investigation Tools
- ✅ Amazon Detective — root cause analysis, graph visualization
- ✅ CloudTrail log analysis — who did what, when
- ✅ VPC Flow Logs analysis — network-level evidence
- ✅ SSM OpsCenter — operational item management
- ✅ SageMaker notebooks for forensic analysis

### 2.6 Testing & Resilience
- ✅ AWS Fault Injection Service — chaos engineering, test response plans
- ✅ AWS Resilience Hub — resilience posture validation
- ✅ Amazon Application Recovery Controller — disaster recovery coordination
- ✅ GameDay exercises — tabletop and live testing

---

## Cross-Domain: Commonly Confused Topics (EXAM TRAPS)

### Service Confusion Pairs
- ✅ GuardDuty vs Macie vs Inspector vs Detective
- ✅ KMS vs CloudHSM — when to use which
- ✅ Secrets Manager vs Parameter Store — features, rotation, cost
- ✅ SCPs vs RCPs — principal-centric vs resource-centric
- ✅ Security Groups vs NACLs — stateful/stateless, rules
- ✅ S3 Presigned URLs vs CloudFront Signed URLs
- ✅ Permission Boundaries vs SCPs — entity level vs account level
- ✅ Cognito User Pools vs Identity Pools — auth vs authz
- ✅ Shield Standard vs Shield Advanced
- ✅ AWS Config vs CloudTrail — state vs API logs
- ✅ OAI vs OAC — legacy vs current CloudFront origin access
- ✅ Gateway endpoints vs Interface endpoints
- ✅ IMDSv1 vs IMDSv2

### Tricky Concepts
- ✅ Cross-account access: resource policy vs AssumeRole — when to use which
- ✅ When resource policies alone are sufficient vs when role assumption is needed
- ✅ KMS key policy is PRIMARY — IAM policies alone cannot grant KMS access unless key policy allows it
- ✅ S3 Object Lock Governance mode vs Compliance mode
- ✅ SCP does NOT affect management account actions
- ✅ Role chaining caps session to 1 hour regardless of max duration setting
- ✅ Default deny vs explicit deny — different behavior with resource policies

---

## Essential Whitepapers & Reading
- ⬜ AWS Security Incident Response Guide
- ⬜ AWS Well-Architected Framework — Security Pillar
- ⬜ AWS KMS Best Practices
- ⬜ Best Practices for DDoS Resiliency
- ⬜ Shared Responsibility Model documentation

---

## Total Coverage Estimate
- **Services:** 81 AWS services in scope
- **Concepts:** 200+ individual topics
- **Domains:** 6, fully mapped
- **Exam weight coverage:** 100%
