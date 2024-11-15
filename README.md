# Static-Site-Server-
Static Site Server for DevOps Roadmap 
https://roadmap.sh/projects/static-site-server

1. Configure EC2 instance
2. Install and configure nging
```
sudo apt update
sudo apt install nginx

```
3. Rsync local site from local to the EC2 instance
```
rsync -avz index.html style.css <ec2_username>@<ec2_ip>:/var/www/html/
```
4. Configura DNS
5. Configure nginx
- create nging config for domain
```
sudo vim /etc/nginx/sites-available/<domain-name>
```
- add configuration 
```
server {
    listen 80;
    server_name <domain_name> www.<domain_name>;

    root /var/www/html;  
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

```
- create symbolic link from sites-available to sites-enabled:
```
sudo ln -s /etc/nginx/sites-available/<domain_name> /etc/nginx/sites-enabled/
```
- restart nginx
```
sudo nginx -t
sudo systemctl restart nginx
```