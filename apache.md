# Using Virtual Hosts on Httpd (Apache)

- Installing Httpd

        sudo dnf update
        sudo dnf install httpd -y

        systemctl start httpd
        systemctl enable httpd

- Create configuration files for your virtual hosts:

For Site1

        sudo nano /etc/httpd/conf.d/site1.conf

        #Paste it
        <VirtualHost *:80>
            ServerName site1.example.com
            DocumentRoot /var/www/site1
        </VirtualHost>

For Site2

        sudo nano /etc/httpd/conf.d/site2.conf

        #Paste it
        <VirtualHost *:80>
            ServerName site2.example.com
            DocumentRoot /var/www/site2
        </VirtualHost>

- Reload Httpd to apply config file changes

        sudo systemctl reload httpd

⚠️ Note `/var/www/html` is the nginx document root to change . you can have your directory anywhere for your virtual host

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