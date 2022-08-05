# nginx-simple-error-pages
Keep your nginx error pages looking simple, but remove the nginx info

## Installation
```bash
mkdir -p /etc/nginx/error_pages
git clone https://github.com/Tapplion/nginx-simple-error-pages /etc/nginx/error_pages
mkdir /etc/nginx/snippets/
ln -s /etc/nginx/error_pages/snippets/error_pages.conf /etc/nginx/snippets/error_pages.conf
ln -s /etc/nginx/error_pages/snippets/error_pages_content.conf /etc/nginx/snippets/error_pages_content.conf
```
Then add to each of your vhosts the following:
```
include snippets/error_pages.conf;
```

Example:
```nginx
$ cat /etc/nginx/conf.d/plex.conf 

server {
    listen      80;
    listen      [::]:80;
    listen      443 ssl http2;
    listen      [::]:443 ssl http2;
    server_name plex.sv1 plex.sv1.lnet;
    include     snippets/ssl.conf;
    include     snippets/error_pages.conf; # <== This
    root        /usr/share/nginx/html;

    location / {
        include snippets/reverse-proxy.conf;
        proxy_pass https://127.0.0.1:32400;
    }
}
```

## Screenshots
### 404 Error Page
![404 Error Page](screenshots/404.png)

### 502 Error Page
![502 error page](screenshots/502.png)
