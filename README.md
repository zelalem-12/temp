# Today Backend: Essential Commands

This quick reference guide contains the most important commands for managing your Today backend deployment.

## Connect to Server

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248
```

## Container Management

### Check Container Status

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo docker ps"
```

### Start Container

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo docker start today-backend"
```

### Stop Container

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo docker stop today-backend"
```

### Restart Container

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo docker restart today-backend"
```

### View Logs

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo docker logs today-backend"
```

### Follow Logs in Real-time

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo docker logs -f today-backend"
```

## Deployment

### Update Application (Pull Latest Code and Restart)

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "cd ~/today-backend && git pull && sudo docker stop today-backend && sudo docker rm today-backend && sudo docker build -t today-app-backend . && sudo docker run -d -p 3070:3070 --env-file .env --restart unless-stopped --name today-backend today-app-backend"
```

## Monitoring

### Check Resource Usage

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo docker stats today-backend --no-stream"
```

### Test API Endpoint

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "curl http://localhost:3070/token/top-gainers"
```

## Troubleshooting

### Check if Port is in Use

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo netstat -tulpn | grep 3070"
```

### Check Disk Space

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "df -h"
```

### Run Container Interactively for Debugging

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "cd ~/today-backend && sudo docker run --rm -it -p 3070:3070 --env-file .env today-app-backend"
```

## Backup

### Backup Environment Variables

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "cp ~/today-backend/.env ~/today-backend-env-backup-$(date +%Y%m%d)"
```

## Cleanup

### Remove Unused Docker Resources (All)

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo docker system prune -a"
```

### Remove Only Dangling Images (Safe Cleanup)

```bash
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "sudo docker image prune -f"
```

### Delete Old Direct Deployment Directory

```bash
# First ensure you have a backup of the .env file
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "test -f ~/today-backend/.env && echo 'Confirmed: .env exists in new location'"

# Then delete the old directory
ssh -i todayapp-staging-pem.pem ubuntu@35.175.245.248 "rm -rf ~/today-backend-direct"
``` 
