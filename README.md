# Rafael Anulao Personal Site

Static personal website for Rafael Anulao. The site has no build step and is meant to run cleanly from a Raspberry Pi, Nginx, Caddy, or any static file host.

## Local Preview

Open `index.html` directly in a browser, or use the VS Code Live Server setting in this repository.

## Raspberry Pi Deployment

Example Nginx directory:

```sh
sudo mkdir -p /var/www/rafael-site
sudo chown -R "$USER":www-data /var/www/rafael-site
rsync -av --delete index.html styles.css assets/ /var/www/rafael-site/
```

Example Nginx server block:

```nginx
server {
    listen 80;
    server_name your-domain.example;
    root /var/www/rafael-site;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

After editing the server block:

```sh
sudo nginx -t
sudo systemctl reload nginx
```

For remote deploys from your laptop:

```sh
rsync -av --delete index.html styles.css assets/ pi@raspberrypi.local:/var/www/rafael-site/
```
