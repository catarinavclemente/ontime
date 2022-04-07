# Environment

### C9

Request a new Cloud 9 instance (at this moment you should email Giancarlo Di NATALE)\
\
Create your Cloud 9 instance:

* Name your environment with your IAM username.
* Instance type is limited : "t3.medium"
* Your environment must be created in "eu-west-1" region (Ireland)
* Platform must be "Amazon Linux 2"
* Be careful, "m4.medium" is listed, but not available, for "medium" instance type you have to select "Other instance type"

Source: [https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/2.+Create+my+C9+environment](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/2.+Create+my+C9+environment)

#### Initialize

After creating the environment, it is compulsory to initialise it with the script provided by DevOps:\
`$ aws s3 cp s3://c9-install-scripts/install-salt.sh - | bash`

#### Configure Docker profile <a href="#id-4.configurec9-dockerprofile" id="id-4.configurec9-dockerprofile"></a>

This [page](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9+-+Docker) explains how to use docker for running web server and all needed services for website development.

Source: [https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9)

#### [Docker profile](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/4.+Configure+C9#id-4.ConfigureC9-Dockerprofile) **installation specific php version** <a href="#id-4.configurec9-2profilesareavailable" id="id-4.configurec9-2profilesareavailable"></a>

`$ sudo` `salt-call state.apply profiles.docker pillar='{"docker":{"php_version":"7.4"}}'`

**Checking your version of npm and Node.js**

To see if you already have Node.js and npm installed and check the installed version, run the following commands:

```
$ node -v
$ npm -v
```

#### &#x20;Install and setup composer <a href="#id-4.configurec9-dockerprofile" id="id-4.configurec9-dockerprofile"></a>

```
$ php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
$ php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
$ php composer-setup.php
$ sudo mv composer.phar /usr/local/bin/composer
```

**`Composer (version 2.3.3) successfully installed to: /home/ec2-user/environment/composer.phar`**

Source: [https://getcomposer.org/download/](https://getcomposer.org/download/)\
[https://getcomposer.org/doc/faqs/how-to-install-untrusted-packages-safely.md](https://getcomposer.org/doc/faqs/how-to-install-untrusted-packages-safely.md)

#### `` <a href="#id-4.configurec9-2profilesareavailable" id="id-4.configurec9-2profilesareavailable"></a>

`Source:` [`https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/4.+Configure+C9`](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/4.+Configure+C9)``

### docker info

```
docker info
Client:
 Context:    default
 Debug Mode: false

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 20.10.7
 Storage Driver: overlay2
  Backing Filesystem: xfs
  Supports d_type: true
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runtime.v1.linux runc io.containerd.runc.v2
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: d71fcd7d8303cbf684402823e425e9dd2e99285d
 runc version: 84113eef6fc27af1b01b3181f31bbaf708715301
 init version: de40ad0
 Security Options:
  seccomp
   Profile: default
 Kernel Version: 4.14.268-205.500.amzn2.x86_64
 Operating System: Amazon Linux 2
 OSType: linux
 Architecture: x86_64
 CPUs: 2
 Total Memory: 7.689GiB
 Name: ip-172-31-28-58.eu-west-1.compute.internal
 ID: CTJ3:3KST:TT3Y:Z5YB:DPUI:7VPQ:AAI2:5W7E:Q76I:N6GI:XZT7:YKEH
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
```

### Project installation

Start by making sure you have the correct access rights to the remote GitHub repository.

### Git usage

**Security**

You can generate a key with this command:\
`$ ssh-keygen -b 4096 -t rsa -f /home/ec2-user/.ssh/id_rsa`

On the remote system, add the contents of your public key file (for example, `~/id_rsa.pub`) to a new line in your `~/.ssh/authorized_keys` file; on the command line, enter:\
`$ cat` /home/ec2-user/.ssh/id\_rsa.pub. `>> ~/.ssh/authorized_keys`

You may want to check the contents of \~/.ssh/authorized\_keys to make sure your public key was added properly; on the command line, enter:\
`$ more ~/.ssh/authorized_keys`[\
](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)\
Then, set-up SSH from your EC2 instance, following the guide on the last link of the sources list, bellow.

Sources: \
[Creating/Converting/Move SSH keys to the right place\
](https://webgate.ec.europa.eu/fpfis/wikis/pages/viewpage.action?pageId=297601060#id-6.C9,SSH\&PhpStorm-Configurationfileforscripts)[Generate an hardware security key to authenticate to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)\
[Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)\
[Setting up GitHub on AWS Cloud9 with ssh](https://medium.com/sonabstudios/setting-up-github-on-aws-cloud9-with-ssh-2545c4f989ea)

Then, clone the GIT reference repo:\
`$ git clone git@github.com:ec-europa/<repository-name>.git`

Add the 'VIRTUAL\_HOST' variable to your '.env.dist' file.

#### Install the project

```
dc exec web composer install
dc exec web ./vendor/bin/run toolkit:build-dev
dc exec web ./vendor/bin/run toolkit:install-clean
```

**Using Docker Compose**

To run the containerised environment, you can follow these steps to set it up, using Docker Compose.

Run: `docker-compose up -d`

This will set up and run the environment. After spawning, please follow the set of commands specified in the documentation of a given component, site or a project.&#x20;

**Create a docker-compose.override** file to add settings for existent services (ASDA credentials for web service) or to add entirely new services. **This file is never committed to the repository.**

**If it's a fresh install:**

```
dc exec web ./vendor/bin/run toolkit:download-dump
dc exec web ./vendor/bin/run toolkit:install-clone
```

### Configure your development environment

The code at the bottom of your _sites/default/settings.php_ file should look like this:\


```
// Load environment development override configuration, if available.
// Keep this code block at the end of this file to take full effect.
if (file_exists($app_root . '/' . $site_path . '/settings.override.php')) {
  include $app_root . '/' . $site_path . '/settings.override.php';
}
```

#### Copy example.settings.local.php

Copy _sites/example.settings.local.php_ to _sites/default/_settings.override.php, and [clear the cache](https://drupalize.me/tutorial/clear-drupals-cache).

#### Enable Twig debugging options

Enabling Twig debugging involves locating the `twig.config[debug]` settings in your _services.yml_ file and changing their values.

These variables can be edited either directly in _sites/default/services.yml_ or added to the _sites/development.services.yml_ file if you followed the steps above to use a _settings.local.php_ file.

#### Edit the following variables under the `twig.config:` section

```php
debug: true
auto_reload: true
cache: false
```

If you're placing this into your _sites/development.services.yml_ file, add the `twig.config` configuration indented under the `parameters:` line. Ensure that your code additions are appropriately indented with 2 spaces, not the tab character (or an error will result).

```php
parameters:
  twig.config:
    debug: true
    auto_reload: true
    cache: false
```

From a fresh install of Drupal and with the `twig.config` additions, the _sites/development.services.yml_ file now looks like this:

```php
# Local development services.
#
# To activate this feature, follow the instructions at the top of the
# 'example.settings.local.php' file, which sits next to this file.
parameters:
  http.response.debug_cacheability_headers: true
  twig.config:
    debug: true
    auto_reload: true
    cache: false
services:
  cache.backend.null:
    class: Drupal\Core\Cache\NullBackendFactory
```

### Synchronize configuration

The process of configuration sync involves 3 steps:

1. Export: export the full configuration as YAML files from one instance of a site. \
   install-clone
2. Import: stage the configuration on a second instance of the site and compare the differences.\
   `dc exec web ./vendor/bin/drush cim`
3. Synchronize: move the staged configuration from the first site into the active configuration of the second site.\
   \
   Check the state of the working directory and the staging area\
   Check configurations status:\
   `./vendor/bin/drush config:status`\\





Site specs 07-04-2022\
\
After install-clone

Administrative theme with a responsive, mobile-first layout and a strong focus on improving the Editorial ExperienceRequires:&#x20;

* Theme Negotiation by Rules (disabled)\
  dc exec web ./vendor/bin/drush en theme\_rule

Then, enable eJustice Admin Theme.\
dc exec web ./vendor/bin/drush then ejp\_adm\_theme\
\
Then \
dc exec web ./vendor/bin/drush config-set system.theme admin ejp\_adm\_theme



Then \
dc exec web ./vendor/bin/drush cex --no\
\
Analyse... keep calm and carry on

### Vim

:w ! sudo tee %\
para forçar a escrita num arquivo sem permissão de escrita.
