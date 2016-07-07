# vhost-manager
A bash script to managet Vhost on Apache 2 linux

#Usage

First install script

```sh
$ git clone https://github.com/rubensfernandes/vhost-manager.git
$ cd vhost-manager
$ ./vhost.bash -install
```

To add a virtual host call 'mysite.dev' with webroot '~/projects/mysite/web'

```sh
$ vhost -d ~/projects/mysite/web -url 'mysite.dev' 'mysite'
```
>'mysite' is a name of config ex: /etc/apache2/sites-available/mysite.conf

To use a specific template
```sh
$ vhost -d ~/projects/mysite/web -url 'mysite.dev' -t ~/template.conf 'mysite'
```
- **-d** is a directory
- **-url** is the url to set in /etc/hosts
- **-t** is the template
- **-logpath** path to save log files
- **mysite** is name of config to set in /etc/apache2/sites-available/mysite.conf

>Templates should be use parameters
* template.url
* template.webroot
* template.email
* template.logpath

Example:
```
<VirtualHost *:80>

    ServerName template.url
    ServerAlias template.url

    ServerAdmin template.email
    DocumentRoot template.webroot


    ErrorLog template.logpath/error.log
    CustomLog template.logpath/access.log combined

    #REWRITE URL
    <Directory template.webroot >

        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted

    </Directory>

</VirtualHost>

```

To remove a virtual host use
```sh
$ vhost -rm mysite
```

To see help
```sh
$ vhost -h
```
