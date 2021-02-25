# My [Nginx Server Configs](https://github.com/h5bp/server-configs-nginx) Fork

[![Test](https://github.com/ratjuggler/server-configs-nginx/workflows/server/badge.svg)](https://github.com/ratjuggler/server-configs-nginx/actions?query=workflow%3Aserver)

This fork includes the following additions/changes to the base configs:
- Added optional configuration for header *[X-Clacks-Overhead](https://xclacksoverhead.org)*.
- Added optional configuration for header *X-Powered-By* just so that I can put "Raspberry Pi" in it.
- Changes to nginx.conf:
  - Change user from *www-data* to *nginx*.
  - Reduced worker connections from *8000* to *1024*.
  - Increase keep-alive timeout from *20s* to *65s*.
  - Added Google fonts to the CSP:, `font-src 'self' fonts.gstatic.com; style-src 'self' fonts.googleapis.com;`
  - Removed `upgrade-insecure-requests` from the CSP to allow for localing test without SSL. **Must** be added back when using SSL.

And now back to the regular README.md...


**Nginx Server Configs** is a collection of configuration snippets that can help
your server improve the website's performance and security, while also
ensuring that resources are served with the correct content-type and are
accessible, if needed, even cross-domain.


## Getting Started

Using the Nginx server configs repo directly has a few required steps to be able to work.

* [Nginx Beginners Guide](https://nginx.org/en/docs/beginners_guide.html)
* [Nginx Request Processing](https://nginx.org/en/docs/http/request_processing.html)


### Check `nginx.conf` settings

The first thing to check is that the `nginx.conf` file contains appropriate values for
your specific install.

Most specific variables are:

* `user`
* `error_log`
* `pid`
* `access_log`

### Nginx test and restart

* To verify Nginx config

  ```shell
  nginx -t
  ```

* To verify Nginx config with a custom file

  ```shell
  nginx -t -c nginx.conf
  ```

* To reload Nginx and apply the new config

  ```shell
  nginx -s reload
  ```

### Basic structure

This repository has the following structure:

```text
./
├── conf.d/
│   ├── default.conf
│   └── templates/
├── h5bp/
│   ├── basic.conf
│   ├── location/
│   └── .../
├── mime.types
└── nginx.conf
```

* **`conf.d/`**

  This directory should contain all the `server` definitions.

  Except if they are dot prefixed or non `.conf` extension, all files in this
  folder **are** loaded automatically.

  * **`templates` folder**

    Files in this folder contain a `server` template for secure and non-secure hosts.
    They are intended to be copied in the `conf.d` folder with all `example.com` 
    occurrences changed to the target host.

* **`h5bp/`**

  This directory contains config snippets (mixins) to be included as desired.

  There are two types of config files provided, individual config snippets and
  combined config files which provide convenient defaults.

  * **`basic.conf`**

    This file loads a small subset of the rules provided by this repository to add
    expires headers, allow cross-domain fonts and protect system files from web
    access.
    The `basic.conf` file includes the rules which are recommended to always be
    defined.

  * **`location/`**
  
    Files in this folder contain one or more `location` directives. They are intended
    to be loaded in the `server` context (or, in a nested `location` block).

* **`mime.types`**

  The mime.types file is responsible for mapping file extensions to mime types.

* **`nginx.conf`**

  The main Nginx config file.


## Usage

### As a reference

To use as reference requires no special installation steps, download/checkout the
repository to a convenient location and adapt your existing Nginx configuration
incorporating the desired functionality from this repository.

Download the [latest release archive](https://github.com/h5bp/server-configs-nginx/releases/latest).

### Directly

To use directly, replace the Nginx config directory with this repository.
For example:

```shell
nginx -s stop
cd /etc
mv nginx nginx-previous
git clone https://github.com/h5bp/server-configs-nginx.git nginx
# install-specific edits
nginx
```

### Manage sites

```bash
cd /etc/nginx/conf.d
```

* Creating a new site

  ```bash
  cp templates/example.com.conf .actual-hostname.conf
  sed -i 's/example.com/actual-hostname/g' .actual-hostname.conf
  ```

* Enabling a site

  ```bash
  mv .actual-hostname.conf actual-hostname.conf
  ```

* Disabling a site

  ```bash
  mv actual-hostname.conf .actual-hostname.conf
  ```

```bash
nginx -s reload
```


## Support

 * Nginx v**1.8.0**+


## Contributing

Anyone is welcome to [contribute](.github/CONTRIBUTING.md),
however, if you decide to get involved, please take a moment to review
the [guidelines](.github/CONTRIBUTING.md):

* [Bug reports](.github/CONTRIBUTING.md#bugs)
* [Feature requests](.github/CONTRIBUTING.md#features)
* [Pull requests](.github/CONTRIBUTING.md#pull-requests)


## Acknowledgements

[Nginx Server Configs](https://github.com/h5bp/server-configs-nginx) is
only possible thanks to all the awesome
[contributors](https://github.com/h5bp/server-configs-nginx/graphs/contributors)!


## License

The code is available under the [MIT license](LICENSE.txt).
