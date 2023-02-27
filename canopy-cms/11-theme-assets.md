---
author:
    name: Mohammad Prince
order: 72
---

# Theme Assets

## Basic
Add assets to your route.

```php
// path: public/css/style.css
$theme->asset()->add('core-style', 'css/style.css');
```
```php
// path: public/js/script.css
$theme->asset()->container('footer')->add('core-script', 'js/script.js');
```
```php
// path: public/themes/[present-theme]/assets/css/custom.css
// This case has dependency with "core-style".
$theme->asset()->usePath()->add('custom', 'css/custom.css', array('core-style'));
```
```php
// path: public/themes/[present-theme]/assets/js/custom.js
// This case has dependency with "core-script".
$theme->asset()->container('footer')->usePath()->add('custom', 'js/custom.js', array('core-script'));
```

> By giving an argument to the method, you can compel the use theme to hunt
> up an existing theme.

Render styles and scripts in your layout.
```php
// Without container
echo Theme::asset()->styles();

// With "footer" container
echo Theme::asset()->container('footer')->scripts();
```
Direct path to theme asset.
```php
echo Theme::asset()->url('img/image.png');
```
Remove added CSS/Js.
```php
// Add to platform/themes/[your-theme]/functions/functions.php
app()->booted(function () {
    Theme::asset()->remove('style-css');
    Theme::asset()->container('footer')->remove('style-js');
});
```