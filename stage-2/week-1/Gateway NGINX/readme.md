
# GATEWAY NGINX
[ Gateway ]

- Installasi nginx di server gateway
- Buat konfigurasi reverse proxy di dalam directory : /etc/nginx/dumbways
- Gunakan domain :
   - <nama>.studentdumbways.my.id (front-end)
   - api.<nama>.studentdumbways.my.id (back-end)
    note : <nama> diganti sesuai dengan nama kalian.
- SSL menggunakan certbot (http:// menjadi https://)


## instalasi nginx di sever getway


install

```bash
sudo apt update

```


```bash
  sudo apt install nginx
```

### cek status
```bash
  sudo systemctl status nginx
```
### buat file config
```bash
  cd /etc/nginx/
```
```bash
  sudo mkdir dumbways
```
```bash
  sudo nano rproxy.conf
```

```bash
  server {
    server_name jeri.studentdumbways.my.id;

    location / {
             proxy_pass http://192.168.234.128:3000;
    }
}

server {
    server_name api.jeri.studentdumbways.my.id;

    location / {
             proxy_pass http://192.168.234.128:3000;
    }
}
```

### konfirmasi file config yang telah dibuat
```bash
  sudo nginx -t
```
```bash
  sudo systemctl reload nginx
```
```bash
  http://jeri.studentdumbways.my.id/login
```

```bash
  http://api.jeri.studentdumbways.my.id/login
```
### ssl mengunakan cartbot (https// menjadi https//)
```bash
  sudo apt install snapd
```
```bash
  sudo snap install --classic certbot
```
### buat direktori baru untuk certbot
```bash
  sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
### setifikasi domain yang telah dibuat
```bash
  sudo certbot --nginx
```

### jalankan certbot
```bash
  sudo certbot renew --dry-run
```
### jalankan domain
```bash
  https://jeri.studentdumbways.my.id/login
  https://api.jeri.studentdumbways.my.id/login
```