# Development guide

## Environment

{% hint style="info" %}
**Good to know:** Before following the instructions provided on toolkit, be sure to have composer installed in your environment
{% endhint %}

### AWS Cloud 9

Request a new Cloud 9 instance (at this moment you should email Giancarlo Di NATALE)\
Create your Cloud 9 instance:

* Name your environment with your IAM username.
* Instance type is limited : "t3.medium"
* Your environment must be created in "eu-west-1" region (Ireland)
* Platform must be "Amazon Linux 2"
* Be careful, "m4.medium" is listed, but not available, for "medium" instance type you have to select "Other instance type"

#### Initialize

After creating the environment, it is compulsory to initialise it with the script provided by DevOps:\
`aws s3 cp s3://c9-install-scripts/install-salt.sh - | bash`

{% hint style="info" %}
You need to have the following software installed on your local development environment: [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), [Docker](https://docs.docker.com/install/) and [Docker Compose](https://docs.docker.com/compose/install/)
{% endhint %}

### Git, Docker and Docker Compose <a href="#id-4.configurec9-dockerprofile" id="id-4.configurec9-dockerprofile"></a>

#### Configure Docker profile <a href="#id-4.configurec9-dockerprofile" id="id-4.configurec9-dockerprofile"></a>

sudo salt-call state.apply profiles.docker

This [page](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9+-+Docker) explains how to use docker for running web server and all needed services for website development.

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php --version=1.9.0
sudo mv composer.phar /usr/local/bin/composer
```

#### Docker Compose

Run this command to download the current stable release of Docker Compose: \
&#x20;`$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/`

Apply executable permissions to the binary:\
`$ sudo chmod +x /usr/local/bin/docker-compose`

If the command docker-compose fails after installation, check your path. You can also create a symbolic link to /usr/bin or any other directory in your path.

```
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

**Using Docker Compose**

To run the containerised environment, you can follow these steps to set it up, using Docker Compose.

Run: `docker-compose up -d`

This will set up and run the environment. After spawning, please follow the set of commands specified in the documentation of a given component, site or a project. Usually the next step is to execute Composer script to download and set up dependencies.\
`docker-compose exec web ./vendor/bin/run drupal:site-install`

Wait a few minutes and, finally, run:\
`docker-compose exec web composer install`\
\
In order to tweak settings or adjust configuration of a specific container, please edit the `docker-compose.yml` file accordingly to your current needs.

### Setting up a project

To install locally a project running Toolkit 4 you should run the following commands:

Start by cloning GIT reference repo:\
`git clone git@github.com:ec-europa/<repository-name>.git`

#### Setting up the environment

By default, docker-compose reads two files, a `docker-compose.yml` and an optional `docker-compose.override.yml` file. **By convention, the `docker-compose.yml` contains your base configuration and it is committed to the repository.** This file contains a webserver, a mysql server and a selenium server. It very closely matches the environment the website is deployed on.

**Create a docker-compose.override** file to add settings for existent services (ASDA credentials for web service) or to add entirely new services. **This file is never committed to the repository.**

Check if composer.json has the correct requirements.\
And then:

```
docker-compose exec web composer install
docker-compose exec web ./vendor/bin/run toolkit:build-dev
```

If it's a fresh install:

```
docker-compose exec web ./vendor/bin/run toolkit:download-dump
```

Then:

```
docker-compose exec web ./vendor/bin/run toolkit:install-clone
```

### Git configuration

#### Aliases

Aliases are stored in \~/.gitconfig.\
\
Now you’ll learn a few of the more interesting options that you can set in this manner to customize your Git usage.

First, a quick review: Git uses a series of configuration files to determine non-default behavior that you may want. The first place Git looks for these values is in the system-wide `[path]/etc/gitconfig` file, which contains settings that are applied to every user on the system and all of their repositories. If you pass the option `--system` to `git config`, it reads and writes from this file specifically.

The next place Git looks is the `~/.gitconfig` (or `~/.config/git/config`) file, which is specific to each user. You can make Git read and write to this file by passing the `--global` option.

Finally, Git looks for configuration values in the configuration file in the Git directory (`.git/config`) of whatever repository you’re currently using. These values are specific to that single repository, and represent passing the `--local` option to `git config`. If you don’t specify which level you want to work with, this is the default.

Each of these “levels” (system, global, local) overwrites values in the previous level, so values in `.git/config` trump those in `[path]/etc/gitconfig`, for instance.\\

## Collaborating

On GitHub, create a fork from the EC repo.\
ec-europa: _https://github.com/ec-europa/\<project-name_>-reference

Add this repo as your origin branch.

In addition to origin, it’s often convenient to have a connection to your teammates’ repositories. For example, if your co-worker maintain the same repository as you, from his own fork, you can add a connection as follows:

```
git remote add other_user dev.example.com/other_user_repo.git
```

you git@github.com:you/common\_repo.git (fetch)\
you git@github.com:you/common\_repo.git (push)

co\_worker git@github.com:co\_worker/common\_repo.git (fetch\
coworker git@github.com:coworker/common\_repo.git (push)\_\
\_\_\
\_origin git@github.com:\_organization/common\_repo.git (fetch)\
origin git@github.com:organization/common\_repo.git (push)

It is good practice to keep the feature branch always up to date with [trunk](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development).\
If your branch is recent, the first option is to use rebase.

```
git checkout feature/my-feature
git rebase -i master
```

Sources: [https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development)

### Deployment into ACC

#### There are two options:

* **Traditional approach**
* **Using the auto-merge functionality**

#### Traditional approach

If we don't want to use the auto-merge we can proceed as the usual way, so **from our fork 's \<branch\_name> against reference's master branch.**

![](../.gitbook/assets/image2020-8-13\_15-57-34.png)

**PS:** Once the pipeline have green lines, we need to **contact QA Team and request a code review** before lead ACC. If we pass this code review QA directly merge our PR into master and a new drone execution will be triggered to deploy in ACC.

#### Auto-merge approach

We can use this functionality naming our fork's branch **"deploy",** so in order to trigger a new drone we need to open a **new PR from our fork's deploy branch against reference's master branch** as following:

![](../.gitbook/assets/image2020-8-13\_15-37-0.png)

Keep in mind that you can go straight to ACC but a QA review will be needed before lead PROD (unless you are hosted in a dedicated server, then deploy into PROD is under your own risk).

\
Source: [https://webgate.ec.europa.eu/fpfis/wikis/x/4YZMQ](https://webgate.ec.europa.eu/fpfis/wikis/x/4YZMQ)

### Routine

`docker-compose up -d`\
Starts the containers in the background and leaves them running.\
\
Check the state of the working directory and the staging area\
Check configurations status:\
`./vendor/bin/drush config:status`\\

### Bash

\~/.bashrc.d



### Vim

:w ! sudo tee %\
para forçar a escrita num arquivo sem permissão de escrita.
