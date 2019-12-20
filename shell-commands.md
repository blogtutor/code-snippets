# Learn More

## RTFM
```
man [command]
```

```
[command] --help
```

# Working with files & folders

### List all files in a folder, sorted by file size (largest first)
```
ls -lhS
```

### List specific filetypes in a folder
_Use specific extension or extensions; sorts by file size (largest first)_
```
ls -lhS *.zip
ls -lhS *.zip *.gz
```

# SSL Stuff

### Show SSL Certificate on a site:
_Change domain and IP address_
```
openssl s_client -showcerts -servername www.domain.com -connect 192.124.249.110:443
```
