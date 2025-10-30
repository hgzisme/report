---
title: "Proposal"
date: 2025-09-09
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# A PLATFORM FOR ONLINE COURSES

### 1. Executive Summary
The FocusLearn Platform is an advanced e-learning system designed to provide a structured and highly engaging learning experience for customers. The platform features a comprehensive administrative backend for course creation (CRUD), user management, and assignment review, complemented by a user-centric front end for student registration, course purchasing, and progress tracking. Its key differentiator is an integrated "Focus Mode," which helps users concentrate by incorporating a Pomodoro timer, Google Calendar integration for study scheduling, and a distraction-free environment. Furthermore, an innovative to-do list system allows users to create actionable tasks linked directly to specific timestamps within course videos, with optional AI integration to enhance task management and learning reinforcement.  

### 2. Problem Statement
### What’s the Problem?
-   Passive Learning and Low Engagement: Traditional e-learning platforms often promote passive consumption of video content. Students watch lectures without active engagement, leading to poor information retention and a high rate of course incompletion.
-   Disconnect Between Content and Action: There is a significant disconnect between learning material and actionable tasks. Students struggle to create organized notes or to-do lists that link directly back to specific concepts within a video, making review inefficient and practical application difficult.
-   Distraction and Poor Time Management: The digital learning environment is rife with distractions. Learners lack integrated tools to manage their study time effectively, block out interruptions, and structure their sessions for optimal focus and productivity, resulting in fragmented and inefficient learning.

### The Solution
-   FocusLearn is built on a serverless AWS architecture to enable flexibility, scalability, and cost efficiency.
-   The system leverages AWS Amplify, Lambda, API Gateway, DynamoDB, S3, and Cognito to create a secure, low-cost, and high-performance online learning environment.
-   Users can register, enroll in courses, manage learning tasks, and access interactive study tools—all within a cloud-native, globally available infrastructure.


### Benefits and Return on Investment
-   Serverless approach minimizes operational costs and manual maintenance.
-   Scales automatically based on user activity.
-   Uses AWS Free Tier and pay-per-use pricing, keeping average cost below $100/month.
-   Enhances engagement and retention through integrated productivity features.


### 3. Solution Architecture

![A PLATFORM FOR ONLINE COURSES](/images/2-Proposal/architecture.png)

### AWS Services Used
|        Category       |                  AWS Service                 |                          Function                          |
|:---------------------:|:--------------------------------------------:|:----------------------------------------------------------:|
| Frontend Hosting      | AWS Amplify or S3 + CloudFront               | Host and deliver static website (Next.js frontend)         |
| Backend Compute       | AWS Lambda                                   | Run API logic and course management functions serverlessly |
| API Management        | Amazon API Gateway                           | Handle HTTP requests between frontend and backend          |
| Database              | Amazon DynamoDB (NoSQL) or Aurora Serverless | Store user profiles, course data, and transactions         |
| Authentication        | Amazon Cognito                               | Manage user registration, sign-in, and tokens              |
| Email/Notifications   | Amazon SES / SNS                             | Send verification, password reset, and course alerts       |
| Storage               | Amazon S3                                    | Store course videos, images, documents                     |
| Content Delivery      | Amazon CloudFront                            | Speed up content delivery globally                         |
| Monitoring & Security | CloudWatch, IAM, AWS Shield (Standard)       | Logs, metrics, permissions, and DDoS protection            |
| Domain & Routing      | Route 53                                     | Manage custom domain and SSL certificates                  |

### Component Design
#### 1. Frontend:
-   Built using Next.js and hosted on AWS Amplify for continuous deployment.
-   Uses CloudFront CDN for fast global access.
#### 2. Backend:
-   REST APIs via API Gateway → trigger Lambda functions.
-   Each Lambda handles CRUD operations for users, courses, progress, and payments.
#### 3. Database:
-   DynamoDB stores user data and learning progress.
-   Aurora Serverless optional for relational data like transactions.
#### 4. Authentication:
-   Cognito manages login (email/password, Google OAuth).
-   Integrated with frontend via Amplify Auth module.
#### 5. Storage:
-   Course materials (videos, documents) stored on S3 with lifecycle rules (Glacier for old data).
-   Access controlled via pre-signed URLs.
#### 6. Monitoring & Logging:
-   CloudWatch monitors usage, cost, and errors.
-   AWS Budgets set for alerts under $100/month.


### 4. Technical Implementation
**Implementation Phases**

| Phase                      |                    Implementation Detail                   |
|----------------------------|:----------------------------------------------------------:|
| Infrastructure Setup       | Configure Amplify, S3, and CloudFront for deployment.      |
| Backend Deployment         | Deploy Lambda + API Gateway for course APIs.               |
| Database Configuration     | Create DynamoDB tables for users, courses, and purchases.  |
| Authentication Integration | Set up Cognito for user pool and identity federation.      |
| Notification Setup         | Integrate SES for email verification and course updates.   |
| Monitoring                 | Configure CloudWatch dashboards and alarms.                |
| Testing                    | Conduct functional and load tests for 10,000 requests/day. |

### 5. Timeline & Milestones
**Project Timeline**
-   Project Timeline
-   Pre-Internship (Month 0): 1 month for planning and old station review.
-   Internship (Months 1-3): 3 months.
    -   Month 1: Study AWS and upgrade hardware.
    -   Month 2: Design and adjust architecture.
    -   Month 3: Implement, test, and launch.
-   Post-Launch: Up to 1 year for research.


### 6. Budget Estimation
You can find the budget estimation on the [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01).  
Or you can download the [Budget Estimation File](../attachments/budget_estimation.pdf).

### Infrastructure Costs

| Amplify / S3 + CloudFront    |         5        | Hosting + CDN          |
|------------------------------|:----------------:|------------------------|
| API Gateway + Lambda         |        10        | API requests & compute |
| DynamoDB / Aurora Serverless |        15        | Course & user database |
| Cognito + SES                |         2        | Authentication + email |
| Monitoring / IAM / Route 53  |         5        | Metrics, DNS, roles    |
| Averange                     | ≈ $37 / Month    | Low Traffic            |
|                              | ≈ $80–90 / Month | Medium/high Traffic    |


### 7. Risk Assessment
#### Risk Matrix
-   Cost Overruns: Medium impact, Medium Probability.
-   Performance Degradation: Medium impact, Low Probability.
-   Security Breach: High Impact, Low Probability
-   Downtime: Medium Impact, Low Probability.
-   Data Loss: Medium Impact, Low Probability


#### Mitigation Strategies
-   Cost: Use AWS Budgets and Alerts
-   Performance: Auto-Scaling Lambda and DynamoDB
-   Security: Enable Cognito MFA and IAM least privilege
-   Downtime: Multi-AZ, CDN caching
-   Data: S3 Versioning and backup


#### Contingency Plans
-   Revert to manual methods if AWS fails.
-   Use CloudFormation for cost-related rollbacks.


### 8. Expected Outcomes
#### Technical Improvements: 
-   Fully serverless, scalable platform with minimal ops overhead.
-   Secure authentication and real-time scalability.
-   Improved engagement via interactive learning tools.

#### Long-term Value
-   Operates sustainably under $100/month at small scale.
-   Supports 10,000+ active requests/day.
-   Ready for AI-based course recommendation in future versions.
-   Ready for AI-Integrated for summarising course information
-   Improving todo-list in order taking note at specific video time line
