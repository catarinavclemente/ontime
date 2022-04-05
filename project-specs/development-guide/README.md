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

`$ sudo salt-call state.apply profiles.docker`

This [page](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9+-+Docker) explains how to use docker for running web server and all needed services for website development.

Source: [https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/AWS+Cloud9)

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

Source: [https://getcomposer.org/download/](https://getcomposer.org/download/)\
[https://getcomposer.org/doc/faqs/how-to-install-untrusted-packages-safely.md](https://getcomposer.org/doc/faqs/how-to-install-untrusted-packages-safely.md)

#### [Docker profile](https://webgate.ec.europa.eu/fpfis/wikis/display/MULTISITE/4.+Configure+C9#id-4.ConfigureC9-Dockerprofile) **installation specific php version 7.4**  <a href="#id-4.configurec9-2profilesareavailable" id="id-4.configurec9-2profilesareavailable"></a>

`$ sudo` `salt-call state.apply profiles.docker pillar='{"docker":{"php_version":"7.4"}}`

#### `Install the project`

```
dc exec web composer install
dc exec web ./vendor/bin/run toolkit:build-dev
dc exec web ./vendor/bin/run toolkit:install-clean
```

### Git usage

**Security**

You can generate a key with this command:\
`$ ssh-keygen -b 4096 -t rsa -f /home/ec2-user/.ssh/id_rsa`

On the remote system, add the contents of your public key file (for example, `~/id_rsa.pub`) to a new line in your `~/.ssh/authorized_keys` file; on the command line, enter:\
`$ cat ~/id_rsa.pub >> ~/.ssh/authorized_keys`

You may want to check the contents of \~/.ssh/authorized\_keys to make sure your public key was added properly; on the command line, enter:\
`$ more ~/.ssh/authorized_keys`[\
](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

Sources: \
[Creating/Converting/Move SSH keys to the right place\
](https://webgate.ec.europa.eu/fpfis/wikis/pages/viewpage.action?pageId=297601060#id-6.C9,SSH\&PhpStorm-Configurationfileforscripts)[Generate an hardware security key to authenticate to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)\
[Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)\
<mark style="color:yellow;">**Configuration**</mark>\ <mark style="color:yellow;"></mark>_<mark style="color:yellow;">First, a quick review: Git uses a series of configuration files to determine non-default behavior that you may want. The first place Git looks for these values is in the system-wide</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`[path]/etc/gitconfig`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">file, which contains settings that are applied to every user on the system and all of their repositories. If you pass the option</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`--system`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">to</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`git config`</mark><mark style="color:yellow;">, it reads and writes from this file specifically.</mark>_

_<mark style="color:yellow;">The next place Git looks is the</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`~/.gitconfig`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">(or</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`~/.config/git/config`</mark><mark style="color:yellow;">) file, which is specific to each user. You can make Git read and write to this file by passing the</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`--global`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">option.</mark>_ <mark style="color:yellow;"></mark><mark style="color:yellow;">Aliases are stored in \~/.gitconfig.</mark>

_<mark style="color:yellow;">Finally, Git looks for configuration values in the configuration file in the Git directory (</mark><mark style="color:yellow;">`.git/config`</mark><mark style="color:yellow;">) of whatever repository you’re currently using. These values are specific to that single repository, and represent passing the</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`--local`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">option to</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`git config`</mark><mark style="color:yellow;">. If you don’t specify which level you want to work with, this is the default.</mark>_

_<mark style="color:yellow;">Each of these “levels” (system, global, local) overwrites values in the previous level, so values in</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`.git/config`</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">trump those in</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">`[path]/etc/gitconfig`</mark><mark style="color:yellow;">, for instance.\\</mark>_

<mark style="color:yellow;">Source:</mark> [<mark style="color:yellow;">https://www.git-scm.com/book/en/v2/Customizing-Git-Git-Configuration</mark>](https://www.git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)<mark style="color:yellow;"></mark>

### Project configuration

Start by cloning GIT reference repo:\
`$ git clone git@github.com:ec-europa/<repository-name>.git`

Add the 'VIRTUAL\_HOST' variable to your '.env' file.



Run usual commands:

```
$ [root@ip-172-XX-XX-XX MYWEBSITE]# composer install
$ [root@ip-172-XX-XX-XX MYWEBSITE]# ./vendor/bin/run toolkit:build-dev
$ [root@ip-172-XX-XX-XX MYWEBSITE]# ./vendor/bin/run toolkit:install-clean
$ [root@ip-172-XX-XX-XX MYWEBSITE]# ./vendor/bin/drush
```

**Using Docker Compose**

To run the containerised environment, you can follow these steps to set it up, using Docker Compose.

Run: `docker-compose up -d`

This will set up and run the environment. After spawning, please follow the set of commands specified in the documentation of a given component, site or a project.&#x20;

**Create a docker-compose.override** file to add settings for existent services (ASDA credentials for web service) or to add entirely new services. **This file is never committed to the repository.**

**Create a docker-compose.override** file to add settings for existent services (ASDA credentials for web service) or to add entirely new services. **This file is never committed to the repository.**

If it's a fresh install:\
`docker-compose exec web ./vendor/bin/run toolkit:download-dump`

#### Set-up SSH from your EC2 instance

[https://medium.com/sonabstudios/setting-up-github-on-aws-cloud9-with-ssh-2545c4f989ea](https://medium.com/sonabstudios/setting-up-github-on-aws-cloud9-with-ssh-2545c4f989ea)

#### Aliases

Then, perform a clone installation with production data:\
`docker-compose exec web ./vendor/bin/run toolkit:install-clone`

###

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
