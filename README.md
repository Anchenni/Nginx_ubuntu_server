# Nginx_ubuntu_server

Certainly! Here are the complete instructions for setting up Nginx  web server on Ubuntu Server, including the creation of a simple HTML page for Nginx:

**Step 1: Install Nginx**

1. Connect to your Ubuntu Server VM.
2. Open a terminal window.

Update the package list:

```bash
sudo apt update
```

Install Nginx:

```bash
sudo apt install nginx
```

**Step 2: Create a Directory for Nginx Web Content**

Create a directory to store the web content for your Nginx site. In this example, we'll use `/var/www/my_nginx_site`:

```bash
sudo mkdir /var/www/my_nginx_site
```

Set appropriate permissions for the directory to ensure Nginx can read files from it:

```bash
sudo chown -R www-data:www-data /var/www/my_nginx_site
```

**Step 3: Create an HTML File for Nginx**

Create an HTML file in the new directory to serve as the content for your Nginx site. Use a text editor to create and edit the HTML file:

```bash
sudo nano /var/www/my_nginx_site/index.html
```

Add the following simple HTML code to the file:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Nginx Site</title>
</head>
<body>
    <h1>Welcome to My Nginx Site</h1>
    <p>This is a basic HTML page served by Nginx on Ubuntu Server.</p>
</body>
</html>
```

Save the file by pressing `Ctrl + O`, then press `Enter`, and exit by pressing `Ctrl + X`.

**Step 4: Create an Nginx Configuration File**

Create a new Nginx configuration file for your website:

```bash
sudo nano /etc/nginx/sites-available/my_nginx_site
```

In the text editor, add the following Nginx configuration, adjusting the `server_name` and `root` directives as needed:

```nginx
server {
    listen 8080;  # Use port 8080 instead of the default 80
    server_name localhost;  # Replace with your desired hostname

    root /var/www/my_nginx_site;  # Path to your Nginx site's content
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

**Step 5: Enable the Nginx Configuration**

Create a symbolic link to enable the Nginx configuration:

```bash
sudo ln -s /etc/nginx/sites-available/my_nginx_site /etc/nginx/sites-enabled/
```

**Step 6: Test Nginx Configuration**

Before restarting Nginx, test the configuration to ensure there are no syntax errors:

```bash
sudo nginx -t
```

**Step 7: Restart Nginx**

If the test is successful, restart Nginx to apply the new configuration:

```bash
sudo systemctl restart nginx
```

**Step 8: Access Your Nginx Web Page**

You can access your Nginx web page by visiting "http://localhost:8080" in your web browser. You should see the simple HTML page served by Nginx.

With this setup, Nginx serves content from the `/var/www/my_nginx_site` directory, while Apache continues to serve content from its default directory (`/var/www/html`). This configuration keeps the web content directories separate for Nginx and Apache, ensuring they do not interfere with each other.
