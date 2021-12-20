## Replace a link in the Yoast SEO Breadcrumb trail
```
add_filter( 'wpseo_breadcrumb_output', 'np_wpseo_breadcrumb_output' );
function np_wpseo_breadcrumb_output( $output ){
  if( is_singular() ){
    $from = '<a href="https://www.domain.com/category/food/">Recipes</a>'; // EDIT this to your needs
    $to = '<a href="https://www.domain.com/recipe-index/">Recipes</a>'; // EDIT this to your needs
    $output = str_replace( $from, $to, $output );
  }
return $output;
}
```
## Display Errors even when WordPress doesn't
Courtesy of Zack and Justin at [BigScoots](https://www.bigscoots.com/). Add at the top of `index.php`.
```
ini_set('error_reporting', E_ERROR);
register_shutdown_function("fatal_handler");
function fatal_handler() {
$error = error_get_last();
echo("<pre>");
print_r($error);
}
```
