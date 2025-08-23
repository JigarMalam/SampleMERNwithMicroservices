# MERN with Microservices

## Detailed Folder Structure (with explanations)

```
SampleMERNwithMicroservices/
│
├── backend/
│   ├── helloService/        # Microservice 1 (Hello API)
│   ├── profileService/      # Microservice 2 (Profile API)
|   |── README.md/           # Backend documentation
│
├── frontend/                # React-based frontend
│
├── iac_alb.py               # IaC script to create ALB + Target Groups
├── iac_asg.py               # IaC script to create ASG + Launch Templates
├── iac_infra.py             # IaC script to create VPC, Subnets, SG
|── README.md                # Backend documentation
│
├── Jenkinsfile              # CI/CD pipeline definition
├── README.md                # Main documentation
└── screenshots/             # Folder for architecture/setup screenshots

```

### Deployment Workflow Diagram
```
         Developer Commit
                │
                ▼
          Jenkins Pipeline
                │
       ┌────────┴────────┐
       ▼                 ▼
 Docker Build        Docker Push
(local/EC2)           to Amazon ECR
                │
                ▼
     Infrastructure as Code (Boto3)
                │
       ┌────────┴────────┐
       ▼                 ▼
   Auto Scaling      Application
     Groups          Load Balancer
   (EC2 + Docker)     (ALB + TGs)
       │
       ▼
   Frontend + Backend Services
   (Accessible via ALB DNS)

```


For `helloService`, create `.env` file with the content:
```bash
PORT=3001
```

For `profileService`, create `.env` file with the content:
```bash
PORT=3002
MONGO_URL="specifyYourMongoURLHereWithDatabaseNameInTheEnd"
```

Finally install packages in both the services by running the command `npm install`.

<br/>
For frontend, you have to install and start the frontend server:

```bash
cd frontend
npm install
npm start
```

Note: This will run the frontend in the development server. To run in production, build the application by running the command `npm run build`