---
title: Grav
publish_date: '26-10-2018 12:08'
taxonomy:
    category:
        - CMS
    author:
        - 'Daniel Bieli'
external_links:
    process: true
    no_follow: true
    target: _blank
twittercardoptions: summary
articleenabled: false
musiceventenabled: false
orgaenabled: false
orga:
    ratingValue: 2.5
orgaratingenabled: false
eventenabled: false
personenabled: false
restaurantenabled: false
restaurant:
    acceptsReservations: 'yes'
    priceRange: $
---

[Grav](https://getgrav.org/) is a **Fast**, **Simple**, and **Flexible**, file-based Web-platform.  There is **Zero** installation required.  Just extract the ZIP archive, and you are already up and running.  It follows similar principles to other flat-file CMS platforms, but has a different design philosophy than most. Grav comes with a powerful **Package Management System** to allow for simple installation and upgrading of plugins and themes, as well as simple updating of Grav itself.

The underlying architecture of Grav is designed to use well-established and _best-in-class_ technologies to ensure that Grav is simple to use and easy to extend. Some of these key technologies include:

- [Twig Templating](http://twig.sensiolabs.org/): for powerful control of the user interface
- [Markdown](http://en.wikipedia.org/wiki/Markdown): for easy content creation
- [YAML](http://yaml.org): for simple configuration
- [Parsedown](http://parsedown.org/): for fast Markdown and Markdown Extra support
- [Doctrine Cache](http://doctrine-orm.readthedocs.io/projects/doctrine-orm/en/latest/reference/caching.html): layer for performance
- [Pimple Dependency Injection Container](http://pimple.sensiolabs.org/): for extensibility and maintainability
- [Symfony Event Dispatcher](http://symfony.com/doc/current/components/event_dispatcher/introduction.html): for plugin event handling
* [Symfony Console](http://symfony.com/doc/current/components/console/introduction.html): for CLI interface
- [Gregwar Image Library](https://github.com/Gregwar/Image): for dynamic image manipulation

## Requirements

- PHP 5.6.4 or higher. Check the [required modules list](https://learn.getgrav.org/basics/requirements#php-requirements)
- Check the [Apache](https://learn.getgrav.org/basics/requirements#apache-requirements) or [IIS](https://learn.getgrav.org/basics/requirements#iis-requirements) requirements

## Webserver Konfig

- [Quelle](https://github.com/getgrav/grav/tree/master/webserver-configs)

### Nginx

	```nginx
    ## Begin - Index
    # for subfolders, simply adjust:
    # `location /subfolder {`
    # and the rewrite to use `/subfolder/index.php`
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
    ## End - Index

    ## Begin - Security
    # deny all direct access for these folders
    location ~* /(\.git|cache|bin|logs|backup|tests)/.*$ { return 403; }
    # deny running scripts inside core system folders
    location ~* /(system|vendor)/.*\.(txt|xml|md|html|yaml|yml|php|pl|py|cgi|twig|sh|bat)$ { return 403; }
    # deny running scripts inside user folder
    location ~* /user/.*\.(txt|md|yaml|yml|php|pl|py|cgi|twig|sh|bat)$ { return 403; }
    # deny access to specific files in the root folder
    location ~ /(LICENSE\.txt|composer\.lock|composer\.json|nginx\.conf|web\.config|htaccess\.txt|\.htaccess) { return 403; }
    ## End - Security
	```

## QuickStart

These are the options to get Grav
	
### Downloading a Grav Package

You can download a **ready-built** package from the [Downloads page on https://getgrav.org](https://getgrav.org/downloads)

### With Composer

su www-data -c composer create-project getgrav/grav /var/www/php.pagespeed.plus/htdocs

You can create a new project with the latest **stable** Grav release with the following command:

```
sudo -i -i -u 
```

### From GitHub

1. Clone the Grav repository from [https://github.com/getgrav/grav]() to a folder in the webroot of your server, e.g. `~/webroot/grav`. Launch a **terminal** or **console** and navigate to the webroot folder:
   
```bash
cd var/www/domain
git clone https://github.com/getgrav/grav.git
```

2. Install the **plugin** and **theme dependencies** by using the [Grav CLI application](https://learn.getgrav.org/advanced/grav-cli) `bin/grav`:

   ```bash
   cd var/www/domain/grav
   bin/grav install
   ```

Check out the [install procedures](https://learn.getgrav.org/basics/installation) for more information.

## Adding Functionality

### Admin Plugin installieren

    bin/gpm install admin

#### Benutzer erstellen

    bin/plugin login new-user
 
You can download [plugins](https://getgrav.org/downloads/plugins) or [themes](https://getgrav.org/downloads/themes) manually from the appropriate tab on the [Downloads page on https://getgrav.org](https://getgrav.org/downloads), but the preferred solution is to use the [Grav Package Manager](https://learn.getgrav.org/advanced/grav-gpm) or `GPM`:

```
bin/gpm index
```

This will display all the available plugins and then you can install one or more with:

```
bin/gpm install toc sitemap github shortcode-chartjs advanced-pagecache prism-highlight breadcrumbs page-toc lazy-image admin-power-tools webpacker tinymce-editor git-sync


## Updating

To update Grav you should use the [Grav Package Manager](https://learn.getgrav.org/advanced/grav-gpm) or `GPM`:

```bash
bin/gpm selfupgrade
```

To update plugins and themes:

```bash
bin/gpm update
```

## Admin

### Features

* User login with automatic password encryption
* Forgot password functionality
* Logged-in-user management
* One click Grav core updates
* Dashboard with maintenance status, site activity and latest page updates
* Notifications system for latest news, blogs, and announcements
* Ajax-powered backup capability
* Ajax-powered clear-cache capability
* System configuration management
* Site configuration management
* Normal and Expert modes which allow editing via forms or YAML
* Page listing with filtering and search
* Page creation, editing, moving, copying, and deleting
* Powerful syntax highlighting code editor with instant Grav-powered preview
* Editor features, hot keys, toolbar, and distraction-free fullscreen mode
* Drag-n-drop upload of page media files including drag-n-drop placement in the editor
* One click theme and plugin updates
* Plugin manager that allows listing and configuration of installed plugins
* Theme manager that allows listing and configuration of installed themes
* GPM-powered installation of new plugins and themes


### Installation

First ensure you are running the latest **Grav 0.9.34 or later**.  This is required for the admin plugin to run properly (`-f` forces a refresh of the GPM index).

```bash
bin/gpm selfupgrade -f
```

The admin plugin actually requires the help of 3 other plugins, so to get the admin plugin to work you first need to install **admin**, **login**, **forms**, and **email** plugins.  These are available via GPM, and because the plugin has dependencies you just need to proceed and install the admin plugin, and agree when prompted to install the others:

```bash
bin/gpm install admin
```

### Create User with CLI

After this you need to create a user account with admin privileges:

```bash
bin/plugin login new-user
```

### Create User Manually

Alternatively, you can create a user account manually, in a file called `user/accounts/admin.yaml`. This **filename** is actually the **username** that you will use to login. The contents will contain the other information for the user.

```yaml
password: 'password'
email: 'youremail@mail.com'
fullname: 'Johnny Appleseed'
title: 'Site Administrator'
access:
  admin:
    login: true
    super: true
```

Of course you should edit your `email`, `password`, `fullname`, and `title` to suit your needs.

> You can use any password when you manually put it in this `.yaml` file.  However, when you change your password in the admin, it must contain at least one number and one uppercase and lowercase letter, and at least 8 or more characters.

## Themes

- [Gantry](http://gantry.org/)
- [Knowledge Base](https://github.com/Perlkonig/grav-skeleton-knowledge-base)

## Plugins

- [bin/gpm install breadcrumbs](https://github.com/getgrav/grav-plugin-breadcrumbs/blob/master/README.md)
- [bin/gpm install dropcaps](https://github.com/sommerregen/grav-plugin-dropcaps/blob/master/README.md)
- [bin/gpm install external_links](https://github.com/sommerregen/grav-plugin-external-links/blob/master/README.md)

```bash
bin/gpm install feed-us
bin/gpm install file-content
bin/gpm install custom-css
bin/gpm install cookiespolicy
bin/gpm install git-sync
bin/gpm install github
bin/gpm install lazy-image
bin/gpm install markdown-fontawesome
bin/gpm install markdown-tasklists
bin/gpm install minify-html
bin/gpm install optimus
bin/gpm install podcast
bin/gpm install highlight
bin/gpm install seo
bin/gpm install shortcode-assets
bin/gpm install sitemap
bin/gpm install simple-responsive-tables
bin/gpm install star-ratings
bin/gpm install themer
bin/gpm install tinyseo
bin/gpm install tinymce-editor
bin/gpm install tntsearch
bin/gpm install toc
bin/gpm install youtube
```

## Getting Started

* [What is Grav?](https://learn.getgrav.org/basics/what-is-grav)
* [Install](https://learn.getgrav.org/basics/installation) Grav in few seconds
* Understand the [Configuration](https://learn.getgrav.org/basics/grav-configuration)
* Take a peek at our available free [Skeletons](https://getgrav.org/downloads/skeletons)
* If you have questions, jump on our [Slack Room](https://getgrav.org/slack)!
* Have fun!

## Exploring More

* Have a look at our [Basic Tutorial](https://learn.getgrav.org/basics/basic-tutorial)
* Dive into more [advanced](https://learn.getgrav.org/advanced) functions
* Learn about the [Grav CLI](https://learn.getgrav.org/cli-console/grav-cli)
* Review examples in the [Grav Cookbook](https://learn.getgrav.org/cookbook)

## License

See [LICENSE](https://github.com/getgrav/LICENSE.txt)


- [gitflow-model](http://nvie.com/posts/a-successful-git-branching-model/)
- [gitflow-extensions](https://github.com/nvie/gitflow)

## Running Tests

First install the dev dependencies by running `composer update` from the Grav root.  
Then `composer test` will run the Unit Tests, which should be always executed successfully on any site.  
Windows users should use the `composer test-windows` command.  
You can also run a single unit test file, e.g. `composer test tests/unit/Grav/Common/AssetsTest.php`
