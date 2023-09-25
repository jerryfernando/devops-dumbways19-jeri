
# Deploy Wayshub
Tasks :
[ Appserver ]

    - Gunakan nodejs versi 14.x
    - Clone repository Wayshub frontend & backend lalu deploy aplikasinya menggunakan PM2
    - Install dan konfigurasi database MySQL (mysql_secure_installation)
    - Di wayshub-frontend, rubah isi BaseURL file src/config/api.js menggunakan domain yang sudah disediakan (api.<nama>.studentdumbways.my.id)
    - Di wayshub-backend, rubah isi konfigurasi database MySQL di config/config.json sesuai dengan user pass kalian, dengan nama database "db-wayshub"
## deploy aplikasinya menggunakan PM2


install

```bash
npm install -g pm2

```


```bash
  cd wayshub-frontend/
```
```bash
  npm install
```
```bash
  pm2 ecosystem simple
```
```bash
  nano ecosystem.config.js
```

```bash
  module.exports = {
  apps : [{
    name   : "frontend",
    script : "npm start"
  }]
}
```
### lalukan hal yang sama pada direktori wayshub-backend

```bash
  cd wayshub-backend/
```
```bash
  npm install
```
```bash
  pm2 ecosystem simple
```
```bash
  nano ecosystem.config.js
```

```bash
  module.exports = {
  apps : [{
    name   : "backend",
    script : "npm start"
  }]
}
```
```bash
  cd ..
```
```bash
  pm2 start
```
### konfigurasi database mysql
```bash
  exec bash
```
```bash
  sudo apt update
```
```bash
  sudo nano /etc/apt/sources.list
```
### search (to replace) ubah mirrors jadi archive
```bash
  mirrors.idcloudhost.com
```
```bash
  archive.idcloudhost.com
```
### setting dan create user root
```bash
  sudo apt install mysql-server
```
```bash
  sudo systemctl status mysql.service
```
```bash
  sudo mysql -u root -p
```

```bash
  CREATE USER 'jeri'@'%' IDENTIFIED WITH mysql_native_password BY 'Jeri@888';
```

```bash
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'Jeri@888';
```
### membuat hak akses
```bash
  sudo mysql_secure_installation
```
```bash
  sudo mysql -u root -p
```
```bash
  GRANT ALL PRIVILEGES ON *.* TO 'jeri'@'%';
```
### atau
```bash
  GRANT ALL PRIVILEGES ON *.* TO 'jeri'@'%' WITH GRANT OPTION;
```
### di wayshub-frontend/src/config/api.js konfigurasi api.js 
```bash
  cd wayshub-frontend/
```
```bash
  cd src/
```
```bash
 cd config/
```
```bash
  nano api.js
```
### lalu ubah api.(nama)
```bash
  baseURL:"http://api.jeri.studentdumbways.my.id/api/v1"
```

### di wayshub-backend/config/config.json konfigurasi config.json di ubah nama dan password yang sudah dibikin

```bash
  cd wayshub-backend/
```

```bash
  cd config/
```

```bash
  nano config.json
```

### mengabungkan konfigurasi
```bash
  cd wayshub-backend/
```

```bash
  npm install -g sequelize-cli
```

```bash
  sequelize db:create
```

```bash
  sequelize db:migrate
```

```bash
  cd ...
```
```bash
  cd wayshub-frontend/
```

```bash
  pm2 start
```