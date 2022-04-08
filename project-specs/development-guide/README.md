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

#### Install and setup composer <a href="#id-4.configurec9-dockerprofile" id="id-4.configurec9-dockerprofile"></a>

```
$ php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
$ php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
$ php composer-setup.php
$ sudo mv composer.phar /usr/local/bin/composer
```

**`Composer (version 2.3.3) successfully installed to: /home/ec2-user/environment/composer.phar`**

Source: [https://getcomposer.org/download/](https://getcomposer.org/download/)\
[https://getcomposer.org/doc/faqs/how-to-install-untrusted-packages-safely.md](https://getcomposer.org/doc/faqs/how-to-install-untrusted-packages-safely.md)

#### \`\` <a href="#id-4.configurec9-2profilesareavailable" id="id-4.configurec9-2profilesareavailable"></a>

`Source:` [`https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/4.+Configure+C9`](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/4.+Configure+C9)\`\`

### Project installation

Start by making sure you have the correct access rights to the remote GitHub repository.

Then, clone the GIT reference repo:\
`$ git clone git@github.com:ec-europa/<repository-name>.git`

**Add the 'VIRTUAL\_HOST' variable to your '.env.dist' file.**



**Set-up and run the environment with Docker Compose**

To run the containerised environment, you can follow these steps to set it up, using Docker Compose.

Run: `docker-compose up -d`

This will set up and run the environment. After spawning, please follow the set of commands specified in the documentation of a given component, site or a project.

**Create a docker-compose.override** file to add settings for existent services (ASDA credentials for web service) or to add entirely new services. **This file is never committed to the repository.**

### Vim

:w ! sudo tee %\
para forçar a escrita num arquivo sem permissão de escrita.
