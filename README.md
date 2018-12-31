# Docker Sandbox Documentation
Documenting docker based developer sandboxes

## Table of Contents

## Managing Ports

Sometimes containers don't start on a `docker-compose up -d` and it wasn't clear why. Check that the ports the project is requesting (likely in docker-compose.yml and likely port 80) are not already in use by something else such as apache.

## Using Xdebug

If xdebug isn’t working for a site built with bowline check the value of
`xdebug.remote_host`

It should be `host.docker.internal` not `localhost`

Check at /admin/reports/status/php or use phpinfo();
If this needs updating you should be able to add an xdebug.ini file such as:
```
xdebug.remote_enable=1
xdebug.remote_host=host.docker.internal
zend_extension=xdebug.so
xdebug.remote_log=/var/www/logs/xdebug.log
```

This can go in .docker/etc/xdebug.ini

Then docker-compose.yml needs to set where this file(s) should exist in the container(s).
Both the php and web services should get:
```
volumes:
  - ./.docker/etc/xdebug.ini:/opt/rh/php55/root/etc/php.d/xdebug.ini
```
This location assumes /opt/rh/php55/root/etc/php.d is a directory that contains a number of php .ini files.

You can confirm this location in the phpinfo output (check section `Additional .ini files parsed`, near the beginning)
Then `destroy` your containers and `build` again.
Don’t forget to `import` your database

## Contributing

We value concise documentation over completeness.
Please feel free to submit pull requests.
