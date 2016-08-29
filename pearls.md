+ Git Credential Helper:

```
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'
```

Will store your github username and password in cache for an hour.

+ Push to same branch on github:

```
git config --global push.default matching
```

Regular expression to match `key:` in Sublime Text 3

```
([A-Za-z]*):
```

and replace with quoted key using:

```
"$1":
```