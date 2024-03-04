# Hosting Multiples Sites on Same Server using Virtual Hosts

This if for NGINX 
for 
### Apache Instructions : [Click Here](./apache.md)



- Installing Nginx 

        sudo dnf update
        sudo dnf install nginx -y

        systemctl start nginx
        systemctl enable nginx

- Setting the Config files
    
    [make sure to modify it according to your domain name & Document path] 

    For site1

        sudo nano /etc/nginx/conf.d/site1.conf

        #paste this
        server {
            listen 80;
            server_name site1.example.com;

            root /var/www/site1;
            index index.html;

            location / {
                try_files $uri $uri/ =404;
            }
        }

    For site 2

        sudo nano /etc/nginx/conf.d/site2.conf

        #paste it
        server {
            listen 80;
            server_name site2.example.com;

            root /var/www/site2;
            index index.html;

            location / {
                try_files $uri $uri/ =404;
            }
        }

- Check if the Config file synatx is correct or not
        
        sudo nginx -t

- Reload NGINX to apply config file changes

        sudo systemctl reload nginx

⚠️ Note `/usr/share/nginx/html` is the nginx document root to change . you can have your directory anywhere for your virtual host

- Creating Directories for sites

        sudo mkdir -p /var/www/site1
        sudo mkdir -p /var/www/site2


- adding Contents to your Site Directories

        echo "<h1>Site1</h1>" | sudo tee /var/www/site1/index.html

        echo "<h1>Site2</h1>" | sudo tee /var/www/site2/index.html

## Testing

As we dont have Domains we can check it by modifying the hosts file 

### Windows

path : `C:\Windows\System32\drivers\etc\hosts`

  - launch your notepad with admin permission
  - opne and add your IP and domain name
    

        	<server-ip>	site1.example.com
	        <server-ip>	site2.example.com

- Now visit your site on the browser on the same machine

### Linux

path `/etc/hosts`

- edit the hosts file

        sudo nano /etc/hosts

- Add your IP and Domain


        <server-ip>	site1.example.com
        <server-ip>	site2.example.com

    
- Now visit your site on the browser on the same machine