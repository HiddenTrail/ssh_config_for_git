# ssh_config_for_git
SSH configuration to use with Git when you have multiple Git accounts. Examples here are shown with GitHub and Bitbucket.

Basic understanding of creating SSH keys and using public keys on Git services are required. Here are the basic instuctions for:

- [GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

- [Bitbucket](https://support.atlassian.com/bitbucket-cloud/docs/set-up-personal-ssh-keys-on-windows/)

- [GitLab](https://docs.gitlab.com/ee/user/ssh.html)

## configuration file in .ssh

Several different Git accounts are configured in `~/.ssh/config`:
```
Host <hostname 1>
	HostName bitbucket.org
	User git
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/<private file for git 1>

...

Host <hostname n>
	HostName github.com
	User git
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/<private file for git n>            
```

For example:
```
Host bb
	HostName bitbucket.org
	User git
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/id_rsa_bitbucket

Host ghht
	HostName github.com
	User git
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/id_rsa_github_ht             
```

## cloning repositories

Cloning is made easier with above structured configuration by replacing `git@bitbucket.org` or `git@github.com` by `host` name from above configuration.

Instead of command given by Bitbucket or GitHub:

`git clone git@bitbucket.org:MKorkia/ssh_config_for_git.git`

or

`git clone git@github.com:HiddenTrail/ssh_config_for_git.git`

you can use shorter version:

`git clone bb:MKorkia/ssh_config_for_git.git`

or

`git clone ghht:HiddenTrail/ssh_config_for_git.git`

This is also visible in `.git/config` file inside cloned repository:

```
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
	ignorecase = true
	precomposeunicode = true
[remote "origin"]
	url = bb:MKorkia/ssh_config_for_git.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
	remote = origin
	merge = refs/heads/main
```

and with `git remote -v` command:

```
origin	bb:MKorkia/ssh_config_for_git.git (fetch)
origin	bb:MKorkia/ssh_config_for_git.git (push)
```

## additional tutorial link
[alejandro-martin/multiple-ssh-keys-git.adoc](https://gist.github.com/alejandro-martin/aabe88cf15871121e076f66b65306610)
