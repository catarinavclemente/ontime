# Aliases

.... /home/ec2-user/.bashrc.d/\
cd ec2-user/.bashrc.d \
sudo vim 00-catarina.aliases.sh\
\


{% hint style="info" %}
After adding the aliases to the .bashrc file, run:\
`source ~/.bashrc`
{% endhint %}

## Basic commands

```
grep='grep --color=tty'
ls='/bin/ls -A --color=auto -hp --time-style="+%F %T"' alias ll='ls -al' alias rf='readlink -f' alias vi='vim' 
diff='colordiff -b -B -r --exclude=.svn --exclude=.git' 
hgrep='history | grep'
```

## cloud9 Aliases

```
cloud9GetPublicIP="curl http://169.254.169.254/latest/meta-data/public-ipv4 && echo ''" 
cloud9EC2Reboot='aws ec2 reboot-instances --instance-ids="$(curl http://169.254.169.254/latest/meta-data/instance-id)"'DOCKER d or dc
```

## Docker d or c

```
dps='docker ps'
dc='docker-compose' 
dcup='dc up -d --remove-orphans' 
dcstart='dc start' 
dcrestart='dc restart' 
dcstop='dc stop' 
dcdown='dc down --volumes --remove-orphans'
```

## fast find

`ff='find . -name $1'`

## change directories easily

```
cdenv="cd ~/environment/"
..='cd ..' 
 ...='cd ../..' 
....='cd ../../..' 
.....='cd ../../../..'
```

## GIT g

```
gs='git status -sb' 
gd='git diff'
gco='git checkout'
ga='git add' 
gap='git add -p'
grm='git rm'
gb='git branch -v'
gc='git commit'
gca='git commit --amend' 
gcm='git commit -m' 
gll='git pull' 
gsh='git push' 
glog='git log --graph --pretty=format:"%C(auto)%h -%d %s %Cgreen(%cr) %C(bold blue)<%an>%Creset" --abbrev-commit'
```
