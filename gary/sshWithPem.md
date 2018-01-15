## ssh key generate
  - ssh-keygen -t rsa
  
## modify permission
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub  
chmod 644 ~/.ssh/authorized_keys
chmod 644 ~/.ssh/known_hosts
```

## send pub key to server
 - scp $HOME/.ssh/id_rsa.pub user@myhost.com:id_rsa.pub
 
## add authorized key (in server)
 - cat $HOME/id_rsa.pub >> $HOME/.ssh/authorized_keys
 
