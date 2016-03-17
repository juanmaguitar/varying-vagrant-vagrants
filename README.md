# Varying Vagrant Vagrants

## Notes of this custom version 

### box `precise64`

As the default box give some problems w/ my current environment (including network) i've changed the box to `precise64` that i don't know why it solve all the problems

### upgrade ubuntu

When `ssh` after the ubuntu system can be updated with 

    do-release-upgrade

after 10min or so of installation & reboot, you must do `vagrant halt` and `vagrant up` to use new system properly

### xdebug

XDebug is supossed to be installed but is not (maybe is because the change of the box)

Anyway it can be simply installed by doing 

1- `vagrant ssh`  
2- `sudo pecl install xdebug`   
```bash
Build process completed successfully
Installing '/usr/lib/php5/20121212/xdebug.so'
install ok: channel://pecl.php.net/xdebug-2.4.0
configuration option "php_ini" is not set to php.ini location
You should add "zend_extension=xdebug.so" to php.ini
```
3- Add `zend_extension=xdebug.so` to `/etc/php5/fpm/php.ini`  
4- `vagrant halt` and `vagrant up`  
5- After this if we go to `http://vvv.dev/phpinfo/` (and look for _xdebug_) we should see _xdebug_ is properly loaded   

### auto-setup `vvv-init.sh` files

These files inside project folder under `www` will be executed automatically in every _provision_ (`vagrant up --provision`)
But they should be executed as `vagrant` user and not under `root` user (deault user when provisioning)

To solve this a workaround could be doing this inside of every [auto-site](https://github.com/varying-vagrant-vagrants/vvv/wiki/Auto-site-Setup) folder...

    mv vvv-init.sh init.sh
    echo "su -c './init.sh' vagrant" > vvv-init.sh

This applies for:

- [Demo using WP CLI | vvv-demo-1](https://github.com/simonwheatley/vvv-demo-1)
- [Demo using Composer | vvv-demo-2](https://github.com/simonwheatley/vvv-demo-2)
- [Demo using WP CLI and SVN | vvv-demo-3](https://github.com/simonwheatley/vvv-demo-3)

... and similars




---
For more info read `README.source.md`