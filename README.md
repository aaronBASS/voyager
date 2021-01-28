### Prerequists

[x] Laraval 8 requirements Laravel:Docs
[x] Composer
[x] Git


# Installation

### Instructions based on [voyager-docs:Installation](https://voyager-docs.devdojo.com/getting-started/installation)


Create project directory
```
sudo mkdir ~/html/voyager/
sudo chmod -R a+rw ~/html/voyager/
cd ~/html/voyager/
```

Setup git
```
sudo git init
sudo nano ~/html/voyager/.git/config
```

Or use vscode with git/github plugin
- add folder to workspace
- create README.md [add title and project description]
- publish to github


Open git config file
```
cd .git
sudo nano config
```

Add github user detail (add remote repository details if manually setting up git)
```
[user]
	name = username
	email = your@email.com
```
Exit `ctrl + c`, `Y`, `Enter`

Move back to project directory
```
cd -
```
You should be in ~/html/voyager/


Update & Upgrade
```
sudo apt-get update
sudo apt-get upgrade
```

Install laravel via Composer
```
sudo composer create-project laravel/laravel voyager
```

Change permissions
```
sudo chown -R www-data:www-data ~/html/voyager/
sudo usermod -a -G www-data username
sudo find ~/html/voyager/ -type f -exec chmod 644 {} \;
sudo find ~/html/voyager/ -type d -exec chmod 755 {} \;
```

Install voyager with composer
```
cd voyager
sudo composer require tcg/voyager
```

Change permissions
```
sudo chown -R www-data:www-data ~/html/voyager/voyager/
sudo find ~/html/voyager/voyager/ -type f -exec chmod 644 {} \;
sudo find ~/html/voyager/voyager/ -type d -exec chmod 755 {} \;
sudo chgrp -R www-data storage bootstrap/cache
sudo chmod -R ug+rwx storage bootstrap/cache
```

Configure database
```
sudo apt install mariadb-server
sudo mysql_secure_installation
sudo apt-get update
```

Enter current password for root (enter for none): ENTER Set root password? [Y/n] `y` Remove anonymous users? [Y/n] `y` Disallow root login remotely? [Y/n] `y` Remove test database and access to it? [Y/n] y Reload privilege tables now? [Y/n] `y`

```
sudo mysql -u root -p
```

```
CREATE DATABASE voyager;
CREATE USER 'voyageruser'@'localhost' IDENTIFIED BY 'voyagerpass';
GRANT ALL PRIVILEGES ON voyager.* TO 'voyageruser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

Configure the .env file
```
sudo nano .env
```
Change the following database details
```
DB_DATABASE=voyager
DB_USERNAME=voyageruser
DB_PASSWORD=voyagerpass
```

To install Voyager without dummy data simply run
```
php artisan voyager:install
```
If you prefer installing it with the dummy data run the following command:
```
sudo php artisan voyager:install --with-dummy
```

Start up a local development server with 
```
sudo php artisan serve
```
and visit:
http://127.0.0.1:8000/admin/login

login (if you selected dummy data):

email: `admin@admin.com`
password: `password`