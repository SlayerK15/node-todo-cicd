# Jenkins CI/CD Pipeline for Node.js Todo Application

## Overview
This project demonstrates a complete CI/CD pipeline implementation for a Node.js Todo application using Jenkins, Docker, and GitHub webhooks. The pipeline automatically builds, tests, and deploys the application whenever changes are pushed to the repository.

### Components:
- **Source Control**: GitHub
- **CI/CD Tool**: Jenkins
- **Containerization**: Docker & Docker Compose
- **Application**: Node.js Todo App
- **Server**: EC2 Instance
- **Port Configuration**: 8000:8000

## Prerequisites
- Jenkins 
- Docker & Docker Compose
- Git
- GitHub Account
- EC2 Instance or equivalent server
- Node.js

## Setup Instructions

### 1. EC2 Instance Setup
```bash
# Update package manager
sudo apt update

# Install Docker
sudo apt install docker.io

# Install Docker Compose
sudo apt install docker-compose

# Add user to docker group
sudo usermod -aG docker $USER

# Start Docker service
sudo systemctl start docker
sudo systemctl enable docker
```

### 2. Jenkins Installation & Configuration
```bash
# Install Jenkins
sudo apt install jenkins

# Start Jenkins service
sudo systemctl start jenkins

# Get initial admin password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Required Jenkins Plugins:
- Docker Pipeline
- GitHub Integration
- NodeJS Plugin

### 3. GitHub Repository Setup
1. Fork the repository: https://github.com/LondheShubham153/node-todo-cicd
2. Clone your forked repository:
```bash
git clone https://github.com/[your-username]/node-todo-cicd.git
```

### 4. Webhook Configuration
1. Go to your GitHub repository settings
2. Add webhook:
   - URL: `http://[jenkins-server]:8080/github-webhook/`
   - Content type: `application/json`
   - Events: Push events
   - Active: ✓

### 5. Jenkins Pipeline Configuration
In Build Steps add an Executive Shell and add the following command to the textbox:
```bash
docker-compose up -d
```

### 6. Application Structure
```
node-todo-cicd/
├── app.js
├── Dockerfile
├── docker-compose.yml
├── Jenkinsfile
├── package.json
├── README.md
└── views/
    └── todo.ejs
```

## Troubleshooting

### Common Issues & Solutions

1. Docker Permission Denied
```bash
sudo chmod 666 /var/run/docker.sock
```

2. Jenkins Cannot Access Docker
```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

3. Port Already in Use
```bash
# Check for processes using port 8000
sudo lsof -i :8000

# Kill process if needed
sudo kill -9 [PID]
```

## Security Best Practices

1. Jenkins Security:
   - Use HTTPS
   - Implement authentication
   - Regular security updates
   - Restrict access to authorized users

2. Docker Security:
   - Use specific image versions
   - Regular security scans
   - Proper permission management
   - Container resource limits

## Monitoring & Maintenance

1. Regular Tasks:
   - Jenkins workspace cleanup
   - Docker image cleanup
   - Log rotation
   - Security updates

2. Monitoring:
   - Application logs
   - Jenkins build logs
   - Container health
   - Server resources

## Project Demo
The application can be accessed at: `http://[server-ip]:8000`

## Contributing
1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License
This project is licensed under the MIT License - see the LICENSE file for details

## Acknowledgments
- TrainWithShubham for the DevOps training
- Jenkins community for documentation
- Docker community for container orchestration support


