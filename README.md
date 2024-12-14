Lauch Two Server WebServer and AppServer
create RDS and S3 bucket(ACL Enabled)
create one CloudFront Distribution For S3Bucket
WebServer Configuration :

Install LEMP on WebServer
In Configuration File of Nginx add request block of PHP
 $ location ~ \.php$ {
    proxy_pass http://IP;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    }

AppServer Configuration :
Install Mysql and Create database in RDS (add SG of AppServer In RDS)
create uploads folder and give 777 permission
Install aws sdk and composer in AppServer
