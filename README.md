

## Prerequisites

- Node Version 22


### 1. For Run This Applications
```bash
# install packages
npm install 

# Testing The Applications
npm run check

# For Run the application
npm start
```


### Deployment Process
1. **Cleanup**: Removes existing process if running
   ```bash
   pm2 delete node-app || true
   ```

2. **Start Application**: Launches with absolute path
   ```bash
   pm2 start "./src/server.js" --name node-app
   ```

3. **Save Process List**: Persists PM2 configuration
   ```bash
   pm2 save
   ```

### About The Applications
1. **Route**: This Application has 2 route
   ```bash
   / # this will show a hello world page
   ```
      ```bash
   /api # this will response a json
   ```

2. **Default Port**: By Default this application will run on port 3000


## 🚀AWS Setup Flow

### Update system
```bash
   sudo apt update && sudo apt upgrade -y
```
### Install nginx
```bash
   sudo apt-get install nginx -y
```
### Setup GitHub Actions runner
```bash
   Follow GitHub runner Commands
```
### Install and start runner as service
```bash
   sudo ./svc.sh install
   sudo ./svc.sh start
```
### Install Node.js LTS
```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
```
### Install PM2 Globally
```bash
sudo npm install -g pm2
```

### Configure Nginx (Port 80 → 3000)

```bash 
   sudo nano /etc/nginx/sites-available/default
```

### Replace contents with :

```bash
   server {
    listen 80 default_server;
    listen [::]:80 default_server;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

```
### Reload Nginx
```bash
   sudo nginx -t
   sudo systemctl reload nginx
```