# CI/CD Demo - React + Docker + Docker Compose + AWS EC2

## Local setup

```bash
npm install
npm run dev
```

## Test Docker

```bash
docker build -t cicd-demo .
docker run -d -p 8080:80 --name cicd-demo-container cicd-demo
```

Open http://localhost:8080

## Test Docker Compose

```bash
docker compose up -d --build
docker compose ps
```

Open http://localhost

Stop:

```bash
docker compose down
```

## EC2 setup

Ubuntu EC2:
- Allow SSH (22) from your IP
- Allow HTTP (80) from the internet

Install Docker:

```bash
sudo apt update
sudo apt install -y docker.io docker-compose-v2
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
```

Log out and reconnect.

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/cicd-demo.git
cd cicd-demo
docker compose up -d --build
```

## GitHub Actions secrets

Create these repository secrets under Settings → Secrets and variables → Actions:

- EC2_HOST = EC2 public IP
- EC2_USER = ubuntu
- EC2_SSH_KEY = complete contents of your EC2 private key

Then push to `main`:

```bash
git add .
git commit -m "Deploy application"
git push origin main
```

GitHub Actions will build the application and deploy it to EC2.
