---
title: "Setup DB users"
date: 2023-10-03T10:40:17Z
draft: False
---

Normally you are not able to connect to the MariaDB with root, outside the linux system. Therefor we create a new superuser with as access right from `localhost` and `127.0.0.1`.

{{< toc >}}

## Install prerequsites
### pwgen
Let’s start with the pwgen utility. It helps you create secure passwords. Unless you already have a tool for that…

```plain
sudo apt install pwgen
```

For creating random password with 24 characters, just type the following:

```pwgen -s 24 1```

This will give you like `uWMBijw6vBF9ncNF5vvO6nGZ`.

### Create superuser and give all permissions
Open the mariadb cli by accessing it with root permissions.
```sudo mariadb```

Create the new superuser for access from `localhost` and `127.0.0.1`.
```
CREATE USER `superuser`@`localhost` IDENTIFIED BY PASSWORD 'secretpw';
CREATE USER `superuser`@`127.0.0.1` IDENTIFIED BY PASSWORD 'secretpw';
```

Now grant all permissions to both new users.
```
GRANT ALL PRIVILEGES ON *.* TO `superuser`@`localhost` WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON *.* TO `superuser`@`127.0.0.1` WITH GRANT OPTION;
FLUSH PRIVILEGES;
```