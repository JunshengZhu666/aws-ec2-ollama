# AWS EC2 CUDA Ollama Setup

This guide outlines the steps to set up an Ollama API service on an AWS EC2 instance with CUDA support.

## 1. Launch EC2 Instance

a. Go to EC2 dashboard and click "Launch instance"
b. Name your instance (e.g., "Ollama-GPU-Server")
c. AMI: Search for and select "Deep Learning Base OSS Nvidia Driver GPU AMI (Ubuntu 22.04)"
d. Instance type: g4dn.xlarge (4 vCPUs, 16 GiB Memory, 1 GPU)
e. Create or select a key pair for SSH access
f. Network settings: Create a security group with the following rules:
   - Allow SSH (port 22) from your IP
   - Allow Custom TCP (port 8080) from anywhere (0.0.0.0/0)
g. Configure storage: At least 30 GiB
h. Launch the instance

## 2. Connect to EC2 Instance

```
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

## 3. Update System

```
sudo apt update && sudo apt upgrade -y
```

## 4. Install Go

```
sudo apt install -y golang-go
```

## 5. Install Ollama

```
curl -fsSL https://ollama.com/install.sh | sh
```

## 6. Clone Repository

```
git clone https://github.com/JunshengZhu666/aws-ec2-ollama.git
cd aws-ec2-ollama
```

## 7. Start Ollama in Background

```
ollama serve 
```

## 8. Pull Gemma Model

```
ollama pull qwen2.5vl:7b
```

## 9. Run Go Application

```
go run main.go
```


## Troubleshooting

- Ensure EC2 instance is running
- Verify Go application is running
- Check port 8080 is open in EC2 security group
- Confirm Ollama is running and "gemma2:2b" model is available

To check service status:
```
sudo systemctl status ollama-api.service
```
