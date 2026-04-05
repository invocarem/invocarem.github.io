# setup ssh with no password prompt


## Start ssh-agent 
```
eval "$(ssh-agent -s)"
```

## Add your key
```
ssh-add ~/.ssh/id_ed25519_shared
ssh-add ~/.ssh/id_ed25519
```

### Github test
```
ssh -T git@github.com
```