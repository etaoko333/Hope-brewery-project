Embarking on the Brewery Beverage Website project involves deploying a web server on AWS EC2, configuring NGINX, setting up monitoring with CloudWatch, and managing assets with S3. Here's a comprehensive guide to assist you through each step:

1. Launch an EC2 Instance
Select an Amazon Linux 2 AMI: This is a stable and widely supported choice.

- Instance Type: Choose t2.micro for testing or development purposes.
Inbound Rules:
- HTTP (Port 80): Allows web traffic.
- SSH (Port 22): Enables secure shell access.
- Key Pair: Create or select an existing key pair for SSH access.

2. Connect to Your EC2 Instance
- Using SSH: ssh -i /path/to/your-key.pem ec2-user@your-ec2-public-ip

**- 3. Install and Configure NGINX**
**Update Packages:**
Ensure your package lists are up-to-date:
- sudo apt update
- Install NGINX
- Install NGINX using the apt package manager:
 sudo apt install nginx -y
- Start and Enable NGINX
- Start the NGINX service and enable it to run on system boot:
- sudo systemctl start nginx
- msudo systemctl enable nginx
- sudo systemctl status nginx
- You should see an active (running) status.
- Access via Browser:
- Navigate to your EC2 instance's public IP address in a web browser. You should see the default NGINX welcome page, indicating a successful installation.

4- Steps to Download and Set Up the Project file from GitHub
-** **Install Git ****
- Ensure Git is installed on your server:
- sudo apt update
- sudo apt install git -y
**Clone the Repository**
- Use the git clone command to download the repository: git clone https://github.com/etaoko333/Hope-brewery-project.git
- This will create a folder named Hope-brewery-project in your current directory.
- Navigate to the Project Directory
- cd Hope-brewery-project
- Set Up NGINX to Serve the Project
-Move Files to the Web Root Directory
- sudo mkdir -p /var/www/brewery
- sudo cp -r * /var/www/brewery
- **Update NGINX Configuration**
- Edit the default NGINX configuration or create a new file:
- sudo vim /etc/nginx/sites-available/brewery
**- Add the following configuration **
server {
    listen 80;
    server_name your_domain_or_IP;  # Replace with your domain or public IP

    root /var/www/brewery;  # Correct document root
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
Enable the site by creating a symlink:
- sudo ln -s /etc/nginx/sites-available/brewery /etc/nginx/sites-enabled/
**Test and restart NGINX:**
- sudo nginx -t
-sudo systemctl restart nginx
  5. Deploy Your Website Content
  **Check the NGINX Error Logs:**
- If you continue to see errors, check the logs again for updated messages:
- sudo tail -f /var/log/nginx/error.log

**- 6. Configure AWS S3 for Asset Storage**
To offload static assets to S3:
**Create an S3 Bucket:**
In the AWS Management Console, create a new S3 bucket (e.g., hophaven-beerlist).
- Upload Assets:
- Upload your static assets (images, videos, etc.) to the S3 bucket.
- Set Permissions:
- Ensure the bucket policy allows public read access for these assets.
- Configure NGINX to Serve Assets from S3:
- Update your website's HTML to reference the assets stored in S3. For example:

<img src="https://hophaven-beerlist.s3.amazonaws.com/image.jpg" alt="Brewery Image">

**8. Monitor with AWS CloudWatch**
- Set up monitoring to ensure your website's reliability:
- Install CloudWatch Agent:
- Follow AWS's official documentation to install and configure the CloudWatch agent on your Ubuntu instance.
- Configure Metrics Collection:
- Set up the agent to collect metrics such as CPU usage, memory, disk I/O, and NGINX access logs.
- Create Alarms:
- In the CloudWatch console, create alarms to notify you of any unusual activity or resource usage.
**Additional**
- 9. Secure Your Website with SSL/TLS
To provide a secure browsing experience:
SSL/TLS Configuration
For HTTPS support, you'll need to configure SSL/TLS certificates.
Domain Name Support
To serve your website on a custom domain (e.g., www.brewery.com), you'll need to update the server_name directive.
How to Update the NGINX Configuration
Locate the Configuration File




4. Test the Website
Open your browser and navigate to your server's IP address or domain:
http://<server-ip>
http://brewery.com (if you have configured DNS)
