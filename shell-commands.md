# RTFM
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

### File Cleanup
_Recursively remove all files of a specific type (in this case, .webp images)_
```
find . -type f -name '*.webp' -delete
```
_Delete a folder with stuff in it. CAREFUL: There is no confirmation and no undo!_
```
rm -rf foldername
```

# SSL Stuff

### Show SSL Certificate on a site:
_Change domain and IP address_
```
openssl s_client -showcerts -servername www.domain.com -connect 192.124.249.110:443
```
