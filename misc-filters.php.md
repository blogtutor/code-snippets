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
