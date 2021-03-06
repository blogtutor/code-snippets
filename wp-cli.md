# WP-CLI Commands

## Export Database

```
wp db export
```

## Search & Replace
_Append `--dry-run` first, then if all looks good, run the command without it._

**_Basic search and replace in all tables. Useful for http->https conversion._**
```
wp search-replace 'http://domain.com' 'https://domain.com' --skip-columns=guid --dry-run
```
**_Remove `/year/month/day/` from hardcoded links. Make sure all links are https: first._**
```
wp search-replace 'https://domain.com/([0-9]{4})/([0-9]{2})/([0-9]{2})/' 'https://domain.com/' --regex --skip-columns=guid --dry-run
```
**_Remove `/year/month/` from hardcodedlinks. Make sure all links are https: first._**
```
wp search-replace 'https://domain.com/([0-9]{4})/([0-9]{2})/' 'https://domain.com/' --regex --skip-columns=guid --dry-run
```
**_Change `/year/month/postname.html` to `/postname/` in permalinks. Make sure all links are https: first._**
```
wp search-replace 'https://domain.com/([0-9]{4})/([0-9]{2})/(.*).html' 'https://domain.com/\3/' --regex --skip-columns=guid --dry-run
```
**_Change `/category/postanme/` to `/postanme/` in permalinks. Make sure all links are https: first._**

This needs to be done separately for each hardcoded category URL, replacing the most specific categories (child categories) first. 

`(.*?)(\/|'|"|\s|>)` [should avoid a greedy regex](https://github.com/wp-cli/search-replace-command/issues/157#issuecomment-876750207) so that all instances in an individual cell will get replaced.

It should also work if the link is missing the trailing slash -- it looks for a delimiter of a trailing slash, single quote, double quote, space, or greater-than sign.
```
wp search-replace 'https:\/\/domain\.com\/category-name\/(.*?)(\/|'|"|\s|>)` `https://domain.com/\1` --regex --skip-columns=guid --dry-run
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
