# WebSecurityScanner
WebSecurityScanner Version 1.7
# WebSecurity Scanner

A powerful tool for analyzing websites for security vulnerabilities, privacy concerns, and unsafe practices. Get a comprehensive security score from 0-100 with detailed recommendations.

## Features

- Comprehensive security analysis
- SSL/TLS verification
- Security headers analysis
- Resource permission detection (camera, microphone, geolocation)
- Cookies and trackers analysis
- Vulnerability detection
- Actionable security recommendations

## Installation

### Automatic Installation (Recommended)

The easiest way to install WebSecurity Scanner is to use the automatic installation script:

```bash
# 1. Make the script executable
chmod +x install.sh

# 2. Run the installation script
./install.sh
```

The script will:
- Install all required dependencies
- Set up the application
- Configure PM2 for process management
- Set up autostart on system boot (optional)

### Manual Installation

If you prefer to install manually:

```bash
# 1. Navigate to the project directory
cd websecurity-scanner

# 2. Install dependencies
npm install

# 3. Build the project
npm run build

# 4. Start the application
npm start
```

## Setting up Nginx as a Reverse Proxy

To make your WebSecurity Scanner available on port 80/443, you can use Nginx as a reverse proxy:

```bash
# Install Nginx
sudo apt update
sudo apt install nginx

# Create a new Nginx configuration
sudo nano /etc/nginx/sites-available/websecurity-scanner

# Add the following configuration
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

# Create a symbolic link to enable the site
sudo ln -s /etc/nginx/sites-available/websecurity-scanner /etc/nginx/sites-enabled/

# Test Nginx configuration
sudo nginx -t

# If the test is successful, restart Nginx
sudo systemctl restart nginx
```

## Usage

1. Access the WebSecurity Scanner at http://localhost:5000 (or your domain if you set up Nginx)
2. Enter a website URL to scan
3. View the comprehensive security report
4. Check security recommendations for the scanned website

## PM2 Management Commands

After installation, you can use these PM2 commands to manage the application:

```bash
# View application status
pm2 status

# View application logs
pm2 logs websecurity-scanner

# Restart application
pm2 restart websecurity-scanner

# Stop application
pm2 stop websecurity-scanner
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
