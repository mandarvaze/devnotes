# Working with Amazon (AWS)

## Lightsail - virtual private server instances - $5 for 512gb instance/month
### Setting up SSH - trying to use my own ssh keys.
1. Logging in
    * Change key permissions. `chmod 600 KEYFILE`
    * `ssh -i KEYFILE ubuntu@ip-address`
### PHP Wordpress config
1. Packages
    * `php7.0 php7.0-cli php7.0-fpm php7.0-mysql php7.0-xml php7.0-mbstring php7.0-zip php7.0-gd php7.0-curl php-imagick mysql-server git nginx`
    * Install [composer](https://getcomposer.org).
        * Follow instructions from composer
    * Configure nginx and php7.0-fpm
        * nginx - configure default virtual environment
        * Enable php7.0-fpm in configuration.
    * Create rsa key to share with bitbucket or github
        * `ssh-keygen -t rsa` - no password
    * Add a deployment key to github to pull code to server.
## Server Admin
* Restart service
    * `sudo systemctl restart nginx`
    * `sudo systemctl retart php7.0-fpm`