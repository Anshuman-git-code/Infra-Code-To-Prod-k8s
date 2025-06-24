# 🚀 Complete CI/CD Pipeline with AWS EKS

This project demonstrates a comprehensive CI/CD pipeline using Terraform, Jenkins, SonarQube, JFrog Artifactory, Docker, and AWS EKS. The pipeline automates the entire software delivery process from code commit to production deployment.

## 📋 Project Overview

This project implements a modern DevOps pipeline that includes:

- **Infrastructure as Code (IaC)** using Terraform
- **Continuous Integration** with Jenkins
- **Code Quality Analysis** with SonarQube
- **Artifact Management** with JFrog Artifactory
- **Container Orchestration** with AWS EKS
- **Automated Deployment** with Jenkins Pipeline
- **Email Notifications** for pipeline status

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Git Repository│    │   Jenkins       │    │   SonarQube     │
│                 │───▶│   (CI/CD)       │───▶│   (Code Quality)│
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                │
                                ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   JFrog         │◀───│   Docker        │───▶│   AWS EKS       │
│   Artifactory   │    │   (Container)   │    │   (Kubernetes)  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🛠️ Technologies Used

- **Infrastructure**: Terraform, AWS EC2, AWS EKS
- **CI/CD**: Jenkins
- **Code Quality**: SonarQube
- **Artifact Management**: JFrog Artifactory
- **Containerization**: Docker
- **Orchestration**: Kubernetes (AWS EKS)
- **Security**: Trivy (Vulnerability Scanner)

## 📁 Project Structure

```
24_June_2025/
├── README.md
├── Project-Structure.png
└── Registretion-App-Files/
    ├── install.sh          # Infrastructure setup script
    ├── main.tf             # Terraform main configuration
    ├── provider.tf         # AWS provider configuration
    └── terraform.tfstate   # Terraform state file
```

## 🚀 Getting Started

### Prerequisites

- AWS CLI configured with appropriate permissions
- Terraform installed
- Docker installed (for local testing)
- kubectl installed

### 1. Infrastructure Setup with Terraform

The project uses Terraform to provision the required AWS infrastructure:

```bash
cd Registretion-App-Files
terraform init
terraform plan
terraform apply
```

#### Infrastructure Components:

- **EC2 Instance**: t2.large instance for Jenkins and SonarQube
- **Security Group**: Configured for ports 22, 80, 443, 8080, 9000, 3000
- **EBS Volume**: 40GB root volume

### 2. Automated Installation Script

The `install.sh` script automatically configures:

- **Java 17**: Required for Jenkins and SonarQube
- **Jenkins**: Latest stable version
- **Docker**: For containerization
- **SonarQube**: Code quality analysis
- **Trivy**: Vulnerability scanning

## 🔧 Configuration Steps

### 1. Jenkins Configuration

After the EC2 instance is provisioned:

1. Access Jenkins at `http://<EC2-PUBLIC-IP>:8080`
2. Get the initial admin password from `/var/lib/jenkins/secrets/initialAdminPassword`
3. Install recommended plugins
4. Create admin user

### 2. SonarQube Integration

1. Access SonarQube at `http://<EC2-PUBLIC-IP>:9000`
2. Default credentials: `admin/admin`
3. Install SonarQube Scanner plugin in Jenkins
4. Configure SonarQube server in Jenkins

### 3. JFrog Artifactory Integration

1. Set up JFrog Artifactory (cloud or self-hosted)
2. Configure Artifactory credentials in Jenkins
3. Set up repository for Docker images

### 4. AWS EKS Cluster Setup

1. Create EKS cluster using AWS CLI or console
2. Download kubeconfig file
3. Configure kubectl for EKS cluster
4. Set up necessary RBAC and service accounts

## 📜 Jenkins Pipeline (Jenkinsfile)

The pipeline includes the following stages:

```groovy
pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                // Code quality analysis
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build application and create Docker image
            }
        }
        
        stage('Security Scan') {
            steps {
                // Trivy vulnerability scan
            }
        }
        
        stage('Push to Artifactory') {
            steps {
                // Push Docker image to JFrog Artifactory
            }
        }
        
        stage('Deploy to EKS') {
            steps {
                // Deploy application to AWS EKS
            }
        }
    }
    
    post {
        always {
            // Email notification
        }
    }
}
```

## 🔔 Email Notifications

Configure email notifications in Jenkins:

1. Install Email Extension Plugin
2. Configure SMTP settings
3. Set up email templates
4. Configure pipeline to send notifications on success/failure

## 🔄 Pipeline Triggers

The pipeline can be triggered by:

- **Webhook**: Automatic trigger on code push
- **Polling**: Regular checks for code changes
- **Manual**: Manual trigger from Jenkins UI
- **Scheduled**: Time-based triggers

## 🧪 Testing and Verification

### 1. Pipeline Verification

1. Make a code change and push to repository
2. Monitor Jenkins pipeline execution
3. Verify each stage completes successfully
4. Check SonarQube for code quality metrics
5. Verify Docker image in Artifactory
6. Confirm deployment to EKS cluster

### 2. Application Verification

1. Access the deployed application
2. Verify functionality
3. Check logs and metrics
4. Monitor resource usage

## 🔒 Security Considerations

- **Network Security**: Security groups restrict access
- **Vulnerability Scanning**: Trivy scans for security issues
- **Code Quality**: SonarQube identifies potential security vulnerabilities
- **Secrets Management**: Use Jenkins credentials for sensitive data
- **RBAC**: Proper Kubernetes role-based access control

## 📊 Monitoring and Logging

- **Jenkins**: Built-in monitoring and logging
- **SonarQube**: Code quality metrics and reports
- **EKS**: Kubernetes dashboard and monitoring
- **Application**: Application-specific logging

## 🚨 Troubleshooting

### Common Issues:

1. **Jenkins not accessible**: Check security group and service status
2. **SonarQube connection issues**: Verify network connectivity
3. **Docker permission errors**: Ensure proper group membership
4. **EKS deployment failures**: Check kubeconfig and RBAC

### Useful Commands:

```bash
# Check Jenkins status
sudo systemctl status jenkins

# Check Docker status
sudo systemctl status docker

# Check SonarQube logs
docker logs sonar

# Check EKS cluster
kubectl get nodes
kubectl get pods --all-namespaces
```

## 📈 Best Practices

1. **Infrastructure as Code**: All infrastructure defined in Terraform
2. **Automation**: Complete automation of CI/CD pipeline
3. **Security**: Multiple layers of security scanning
4. **Monitoring**: Comprehensive monitoring and alerting
5. **Documentation**: Clear documentation and runbooks

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💻 Author

Created with ❤️ for demonstrating modern DevOps practices and CI/CD pipeline implementation.

---

**Note**: This project is for educational and demonstration purposes. Please ensure proper security measures and compliance requirements are met for production use. 