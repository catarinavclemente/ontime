# GIT

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

Sources:\
[Creating/Converting/Move SSH keys to the right place\
](https://webgate.ec.europa.eu/fpfis/wikis/pages/viewpage.action?pageId=297601060#id-6.C9,SSH\&PhpStorm-Configurationfileforscripts)[Generate an hardware security key to authenticate to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)\
[Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)\
[Setting up GitHub on AWS Cloud9 with ssh](https://medium.com/sonabstudios/setting-up-github-on-aws-cloud9-with-ssh-2545c4f989ea)

This command below will, afterwards, remove all of the items from the Git index (not from the working directory or local repository), and then will update the Git index, while respecting Git ignores. _PS. Index = Cache_

<mark style="background-color:orange;">git rm -r --cached . && git add . && git commit -am "EJPREV-00: Remove ignored files."</mark>
