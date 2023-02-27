---
author:
    name: Jan Valo
order: 80
---
# Shortcodes
Shortcodes are used to insert more complex logic to content pages without having to code any logic. They are predefined with set attributes to allow customisations

## Creating a shortcode

Using function ```add_shortcode```:

```php
add_shortcode(
    string $key, 
    string $name, 
    string $description, 
    callable $callback_function
)

$callback_function: (callable) (Required) Callback function which will run when rendering shortcode.
```
Example:
```php
add_shortcode('my-block', 'My block', 'Custom block for me', 'add_custom_block_shortcode');
```
Add callback function for shortcode. Example:
```php
function add_custom_block_shortcode() {
    return 'This is my custom block';
    // or
    return view('view-for-my-block')->render();
}
// or you can do an anonymous function like this:

add_shortcode('my-block', 'My block', 'Custom block for me', function() {
    return 'This is my custom block';
    // or
    return view('view-for-my-block')->render();
});
```

You can add this function to ```theme/functions/functions.php``` or in function boot of your plugin service provider.

## Display shortcode in a theme
By default, shortcode just can be shown on ```/views/index.blade.php```, ```page.blade.php``` and ```post.blade.php```

You can find this in ```theme/config.php```
```php
$theme->composer(['index', 'page', 'post'], function(View $view) {
    $view->withShortcodes();
});
```

So you can add short code to page or post content then shortcode should be displayed on page or post.

If you want to show shortcode in other pages, please add them to theme view composer.

Or you can render shortcode by manually. Using function ```do_shortcode()```.
```php
do_shortcode(string $content)
$content: (string) (Required) Content to search for shortcodes. The name of the shortcode hook.
```
Example:
```php 
{!! do_shortcode('[my-block][/my-block]') !!}
```

If there are no shortcode tags defined, then the content will be returned without any filtering. This might cause issues when plugins are disabled but the shortcode will still show up in the post or content.

## Generate shortcode
To generate shortcode tag for a shortcode.
```php
echo generate_shortcode('my-block');
```

You can add param 2 to function generate_shortcode, it's attributes of shortcode.

Example:
```php
echo generate_shortcode('my-block', ['foo' => 'bar', 'abc' => 'xyz']);
```