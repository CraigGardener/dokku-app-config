# dokku-app-config

A [Dokku] [1] plugin to copy config files from the app's git repository.

Rewritten version of [dokku-app-configfiles] [2] is a plugin that allows dokku
app config files (such as `VHOST`, `ENV`, `DOCKER_OPTIONS`, `nginx.tpl` or
`nginx.ssl.tpl`, etc. to be taken from the app's git repository.
This eliminates the need to manually create these files on the dokku server.

In short, per-app dokku config files are checked into the app's git repository
under the directory `.dokku/`. Upon a git push to the dokku server, any files in
`.dokku/` are copied to `/home/dokku/[app]/`.

[1]: https://github.com/progrium/dokku
[2]: https://github.com/mikexstudios/dokku-app-configfiles

## Why would I use this?
Although it is prudent to always keep server configuration files separate from
app files, many cloud hosts (such as dotcloud) offer the option to supply custom
nginx and other configuration files by checking them into your app's root
directory.

This approach is simple, and an advantage is that these configuration files are
always backed up with the app.

This plugin enables similar functionality for dokku.

## Installation
On dokku 0.4+:

    sudo dokku plugin:install https://github.com/CraigGardener/dokku-app-config.git

On dokku 0.3.x, clone into the dokku plugins directory:

    git clone https://github.com/CraigGardener/dokku-app-config.git /var/lib/dokku/plugins/dokku-app-config

## Usage
Within your app's git repository, create a `.dokku` directory:

    mkdir .dokku

Add any dokku app config files to the `.dokku` directory,
e.g. environment variables and docker options:

    echo "export MYVARIABLE='myvalue'" > ENV
    echo "--name myapp" > DOCKER_OPTIONS_DEPLOY

Add the `.dokku` directory to your app's git repository:

    git add .dokku/
    git commit -m "Add dokku config files"

## Contributing
Feel free to fork and create a Pull Request.

## License
The MIT License (MIT)
