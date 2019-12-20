# WP-CLI Commands

## Export Database

```
wp db export
```

## Search & Replace
_Append `--dry-run` first, then if all looks good, run the command without it._

_Basic search and replace in all tables. Useful for http->https conversion._
```
wp search-replace 'http://domain.com' 'https://domain.com' --skip-columns=guid --dry-run
```
_Remove `/year/month/day/` from hardcoded links. Make sure all links are https: first._
```
wp search-replace 'https://domain.com/([0-9]{4})/([0-9]{2})/([0-9]{2})/' 'https://domain.com/' --regex --skip-columns=guid --dry-run
```
_Remove `/year/month/` from hardcodedlinks. Make sure all links are https: first._
```
wp search-replace 'https://domain.com/([0-9]{4})/([0-9]{2})/' 'https://domain.com/' --regex --skip-columns=guid --dry-run
```
_Change `/year/month/postname.html` to `/postname/` in permalinks. Make sure all links are https: first._
```
wp search-replace 'https://domain.com/([0-9]{4})/([0-9]{2})/(.*).html' 'https://domain.com/\3/' --regex --skip-columns=guid --dry-run
```

## Full list of built-in commands
https://developer.wordpress.org/cli/commands/

## WP-Cli not installed? Download it and run it directly from the Phar file.

First, download wp-cli.phar using wget or curl. For example:

```
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
```

Then, check if it works:
```
php wp-cli.phar --info
```

If so, you can run any command using `php wp-cli.phar` instead of the `wp` shortcut.
https://make.wordpress.org/cli/handbook/installing/
