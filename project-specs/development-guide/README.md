# Development guide

## Environment

{% hint style="info" %}
**Good to know:** Before following the instructions provided on toolkit, be sure to have composer installed in your environment
{% endhint %}

### C9 environment

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
`aws s3 cp s3://c9-install-scripts/install-salt.sh - | bash`

{% hint style="info" %}
You need to have the following software installed on your local development environment: [Docker](https://docs.docker.com/install/) and [Docker Compose](https://docs.docker.com/compose/install/)\

{% endhint %}

#### Configure Docker profile <a href="#id-4.configurec9-dockerprofile" id="id-4.configurec9-dockerprofile"></a>

`sudo salt-call state.apply profiles.docker`

This [page](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9+-+Docker) explains how to use docker for running web server and all needed services for website development.

Source: [https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9)

**Checking your version of npm and Node.js**

To see if you already have Node.js and npm installed and check the installed version, run the following commands:

```
node -v
npm -v
```

#### &#x20;Install and setup composer <a href="#id-4.configurec9-dockerprofile" id="id-4.configurec9-dockerprofile"></a>

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
sudo mv composer.phar /usr/local/bin/composer
```

Source: [https://getcomposer.org/download/](https://getcomposer.org/download/)\
[https://getcomposer.org/doc/faqs/how-to-install-untrusted-packages-safely.md](https://getcomposer.org/doc/faqs/how-to-install-untrusted-packages-safely.md)

#### [Docker profile](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/4.+Configure+C9#id-4.ConfigureC9-Dockerprofile) **installation specific php version 7.4**  <a href="#id-4.configurec9-2profilesareavailable" id="id-4.configurec9-2profilesareavailable"></a>

`sudo` `salt-call state.apply profiles.docker pillar='{"docker":{"php_version":"7.4"}}`

**Using Docker Compose**

To run the containerised environment, you can follow these steps to set it up, using Docker Compose.

Run: `docker-compose up -d`

This will set up and run the environment. After spawning, please follow the set of commands specified in the documentation of a given component, site or a project.&#x20;

### Project installation and set-up

To install the project you should run the commands, bellow.\
[https://github.com/ec-europa/toolkit/blob/ce6278216dc58e7324f51c83c0a423ab52edb6f3/docs/installing-project.md](https://github.com/ec-europa/toolkit/blob/ce6278216dc58e7324f51c83c0a423ab52edb6f3/docs/installing-project.md)\
New project from scratch`????`

Start by cloning GIT reference repo:\
`git clone git@github.com:ec-europa/<repository-name>.git`

By default, docker-compose reads two files, a `docker-compose.yml` and an optional `docker-compose.override.yml` file. By convention, the `docker-compose.yml` contains your base configuration and it is committed to the repository. This file contains a webserver, a mysql server and a selenium server. It very closely matches the environment the website is deployed on.

**Create a docker-compose.override** file to add settings for existent services (ASDA credentials for web service) or to add entirely new services. **This file is never committed to the repository.**

**Create a docker-compose.override** file to add settings for existent services (ASDA credentials for web service) or to add entirely new services. **This file is never committed to the repository.**

If it's a fresh install:\
`docker-compose exec web ./vendor/bin/run toolkit:download-dump`

Then, perform a clone installation with production data:\
`docker-compose exec web ./vendor/bin/run toolkit:install-clone`

### Git configuration

#### Set-up SSH from your EC2 instance

[https://medium.com/sonabstudios/setting-up-github-on-aws-cloud9-with-ssh-2545c4f989ea](https://medium.com/sonabstudios/setting-up-github-on-aws-cloud9-with-ssh-2545c4f989ea)

#### Aliases

Aliases are stored in \~/.gitconfig.\
\
Now you’ll learn a few of the more interesting options that you can set in this manner to customize your Git usage.

First, a quick review: Git uses a series of configuration files to determine non-default behavior that you may want. The first place Git looks for these values is in the system-wide `[path]/etc/gitconfig` file, which contains settings that are applied to every user on the system and all of their repositories. If you pass the option `--system` to `git config`, it reads and writes from this file specifically.

The next place Git looks is the `~/.gitconfig` (or `~/.config/git/config`) file, which is specific to each user. You can make Git read and write to this file by passing the `--global` option.

Finally, Git looks for configuration values in the configuration file in the Git directory (`.git/config`) of whatever repository you’re currently using. These values are specific to that single repository, and represent passing the `--local` option to `git config`. If you don’t specify which level you want to work with, this is the default.

Each of these “levels” (system, global, local) overwrites values in the previous level, so values in `.git/config` trump those in `[path]/etc/gitconfig`, for instance.\\



[https://www.git-scm.com/book/en/v2/Customizing-Git-Git-Configuration](https://www.git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

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

![](../../.gitbook/assets/image2020-8-13\_15-57-34.png)

**PS:** Once the pipeline have green lines, we need to **contact QA Team and request a code review** before lead ACC. If we pass this code review QA directly merge our PR into master and a new drone execution will be triggered to deploy in ACC.

#### Auto-merge approach

We can use this functionality naming our fork's branch **"deploy",** so in order to trigger a new drone we need to open a **new PR from our fork's deploy branch against reference's master branch** as following:

![](../../.gitbook/assets/image2020-8-13\_15-37-0.png)

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

### Vim

:w ! sudo tee %\
para forçar a escrita num arquivo sem permissão de escrita.
