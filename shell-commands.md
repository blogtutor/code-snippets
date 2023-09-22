# RTFM
```
man [command]
```

```
[command] --help
```

# Working with files & folders

### List all files in a folder, sorted by file size (largest first).
```
ls -lhSa
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
_Find the ten largest folders in the current directory:_
```
du -hs * | sort -rh | head -10
```

### Finding backdoors
_Search for strings in files to track down hidden backdoors_.  Some examples:
```
grep -R '<?php`
grep -R 'You are logged in'
grep -R '$_GET'
grep -R 'if(isset($_GET'
grep -R 'POST'
grep -R 'administrator'   ## Good to run in /uploads/
grep -R 'wp_create_user'  ## Good to run from /wp-content/ and also check root folder
grep -R '/perl'
```
_Note this example uses Regex and can be run from /uploads/ to searches the `20*` folders only._
```
grep -E -R -o 'base64|st_rot13|gzuncompress|eval|exec|system|assert|stripslashes|reg_replace|move_uploaded_file|<?php' 20*
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
_Find files that don't have expected extensions - useful when searching for non-image files in /uploads/20*_:
```
find 2* -type f -not -name '*.jpg' -not -name '*.jpeg' -not -name '*.webp' -not -name '*.png'
```
_Delete a folder with stuff in it, including all subfolders. CAREFUL: There is no confirmation and no undo!!_
```
rm -rf foldername
```
_Find files with a certain date, newer than a certain date, or between dates_. More info:
https://unix.stackexchange.com/questions/424319/how-to-find-files-based-on-timestamp
```
find . -type f -ls | grep 'Jan 11 04'
find . -type f -newermt '9/23/2023'
find . -type f -newermt 2018-01-10 ! -newermt 2018-01-11 
```
_Find files that are owned by a group other than desired. For example, for BigScoots replace `GROUPNAME` with 'nginx'. Use `! -path` to exclude paths._
```
find . ! -group GROUPNAME 
find . ! -group GROUPNAME ! -path './APATH/' ! -path './ANOTHERPATH'
```

# SSL Stuff

### Show SSL Certificate on a site:
_Change domain and IP address_
```
openssl s_client -showcerts -servername www.domain.com -connect 192.124.249.110:443
```
