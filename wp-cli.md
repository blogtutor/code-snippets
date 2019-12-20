# WP-CLI Commands

## Export Database

```
wp db export
```

## Search & Replace
_Basic search and replace in all tables. Useful for http->https conversion._
```
wp search-replace 'http://domain.com' 'https://domain.com' --skip-columns=guid
```
_Remove /year/month/day/ from hardcoded links. Recommend using `--dry-run` first then running without it if all looks good._
```
wp search-replace 'https://domain.com/([0-9]{4})/([0-9]{2})/([0-9]{2})/' 'https://domain.com/' --regex --skip-columns=guid --dry-run
```
_Remove /year/month/ from hardcodedlinks._
```
wp search-replace 'simple-nourished-living.com/([0-9]{4})/([0-9]{2})/' 'simple-nourished-living.com/' --regex --skip-columns=guid --dry-run
```
_Remove /year/month/postname.html in permalinks_
```
wp search-replace 'https://melaniemakes.com/([0-9]{4})/([0-9]{2})/(.*).html' 'https://melaniemakes.com/\3/' --regex --skip-columns=guid --dry-run
```
