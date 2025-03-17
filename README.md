# Update package list
sudo apt update

# Install Node.js and npm
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs

# Verify installation
node -v
npm -v

# Install nginx
sudo apt install -y nginx

# Start nginx and enable it to run at boot
sudo systemctl start nginx
sudo systemctl enable nginx

# Check nginx status
sudo systemctl status nginx

const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World! Your Node.js server is running.\n');
});

const PORT = 12000;
server.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});

# Install PM2 globally
sudo npm install -g pm2

# Start your application with PM2
cd /path/to/your/app
pm2 start app.js --name "my-nodejs-app"

# Set PM2 to start on boot
pm2 startup
# Run the command that PM2 outputs

# Save the current PM2 process list
pm2 save


# Create the file in the nginx sites-available directory
sudo nano /etc/nginx/sites-available/my-nodejs-app

# Create a symbolic link to sites-enabled
sudo ln -s /etc/nginx/sites-available/my-nodejs-app /etc/nginx/sites-enabled/

# Test nginx configuration
sudo nginx -t

# If the test is successful, reload nginx
sudo systemctl reload nginx




# Create the file in the nginx sites-available directory
sudo nano /etc/nginx/sites-available/api-skoegle-config

# Create a symbolic link to sites-enabled
sudo ln -s /etc/nginx/sites-available/api-skoegle-config /etc/nginx/sites-enabled/

# Remove default configuration if needed
sudo rm /etc/nginx/sites-enabled/default

# Test nginx configuration
sudo nginx -t

# If the test is successful, reload nginx
sudo systemctl reload nginx      



server {
    listen 80;          # Listen for HTTP connections on port 80
    listen [::]:80;     # Also listen on IPv6
    
    server_name api.skoegle.com;   # Only respond to requests for this domain
    
    location / {        # For all URL paths
        # Forward requests to your Node.js app running on port 12000
        proxy_pass http://localhost:12000;
        
        # Support WebSocket connections if your app uses them
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        
        # Pass the original host header to your application
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        
        # Additional headers that help with logging and security
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}



sudo nano /etc/nginx/sites-available/api-skoegle-config


sudo ln -s /etc/nginx/sites-available/api-skoegle-config /etc/nginx/sites-enabled/

sudo rm /etc/nginx/sites-enabled/default

sudo nginx -t


nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

sudo systemctl reload nginx


curl -H "Host: api.skoegle.com" http://localhost




