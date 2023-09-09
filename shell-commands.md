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

### Check on files & disk usage
_Get a total count of files in a folder and its subfolders_
```
find . -type f | wc -l
```
_Check total disk usage of a folder:_
```
du -h
```

### Finding backdoors
_Search for these strings in files to track down hidden backdoors_.  
```
grep -r 'You are logged in'
grep -r '<?php`
grep -r 'if(isset($_GET'
```
_Note this example uses Regex and can be run from /uploads/ to searches the `20*` folders only._
```
grep -E -r -o 'base64|st_rot13|gzuncompress|eval|exec|system|assert|stripslashes|reg_replace|move_uploaded_file|<?php' 20*
```

### File Searching & Cleanup
_Recursively find all files of a specific type_.
```
find . -type f -name '*.webp'
find . -type f -name '*.pl'
find . -type f -name '*.php'
```
_Add the -delete flag to delete the found files_:
```
find . -type f -name '*.webp' -delete
```
_Find files that don't have expected extensions - useful when searching in /uploads/ folder especially_
```
find 2* -type f -not -name '*.jpg' -not -name '*.jpeg' -not -name '*.webp' -not -name '*.png'
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
