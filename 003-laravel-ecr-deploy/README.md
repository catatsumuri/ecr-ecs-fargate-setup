# Docker Build & Push to AWS ECR

## 🚀 How to Build and Run Locally

### **Build Images**
Run the following commands to build the Docker images:

```sh
docker build -t my-ecs-php-fpm -f ./srv/Dockerfile --target=php-fpm .
docker build -t my-ecs-nginx -f ./srv/Dockerfile --target=nginx .
```

### **Run with Docker Compose**
```sh
docker compose down
docker compose up -d
```

---

## 📤 **Push Images to AWS ECR**

### **Login to ECR**
```sh
aws ecr get-login-password --region ap-northeast-1 | docker login --username AWS --password-stdin ECR_REPOSITORY_URI
```

### **Tag Images**
```sh
docker tag my-ecs-php-fpm ECR_REPOSITORY_URI/practice/my-ecs-php-fpm:latest
docker tag my-ecs-nginx ECR_REPOSITORY_URI/practice/my-ecs-nginx:latest
```

### **Push Images**
```sh
docker push ECR_REPOSITORY_URI/practice/my-ecs-php-fpm:latest
docker push ECR_REPOSITORY_URI/practice/my-ecs-nginx:latest
```

---

## ✅ **Confirm Images are Pushed Successfully**
```sh
aws ecr describe-images --repository-name practice/my-ecs-php-fpm --region ap-northeast-1
aws ecr describe-images --repository-name practice/my-ecs-nginx --region ap-northeast-1
```

---

### **Notes**
- Replace `ECR_REPOSITORY_URI` with your actual ECR repository URI (e.g., `123456789.....dkr.ecr.ap-northeast-1.amazonaws.com`).
- Ensure AWS CLI is configured before running these commands.
- Use `docker compose logs -f` to monitor the logs.


