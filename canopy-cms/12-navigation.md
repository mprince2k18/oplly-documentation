---
author:
    name: Mohammad Prince
order: 73
---

# Navigation
## Default menu locations

    platform/packages/menu/config/general.php
    
```php
'locations' => [
    'header-menu' => 'Header Navigation',
    'primary-menu'   => 'Primary Navigation',
    'footer-menu' => 'Footer Navigation',
],
```
## Render menu by location
```php
{!!
   Menu::renderMenuLocation('primary-menu', [ 
     'options' => [],
     'theme'   => true,
   ])
!!}
```
`primary-menu` is the menu location key
`'options'` are attributes of `ul` tag. Ex: `'options' => ['id' => 'menu-header-primary-menu', 'class' => 'menu']`
## Add new menu location
```php
Menu::addMenuLocation('menu-location-key', 'Description here');
```
## Remove a menu location
```php
Menu:removeMenuLocation('menu-location-key');
```
## Customize menu views
to modify the view so that menu is displayed. You could make a file in `/public/themes/your-theme/partials`
```php
<ul {!! $options !!}>
    @foreach ($menu_nodes as $key => $row)
        <li class="{{ $row->css_class }} @if ($row->url == Request::url()) current @endif">
            <a href="{{ $row->url }}" target="{{ $row->target }}">
                <i class='{{ trim($row->icon_font) }}'></i> <span>{{ $row->name }}</span>
            </a>
            @if ($row->has_child)
                {!! Menu::generateMenu([
                    'slug' => $menu->slug,
                    'parent_id' => $row->id
                ]) !!}
            @endif
        </li>
    @endforeach
</ul>
```
The default code for the menu is found in `core/menu/resources/views/partials/default.blade.php`
And to show the menu with a custom view, use the below code:
```php
{!!
    Menu::renderMenuLocation('primary-menu', [
        'options' => [],
        'theme' => true,
        'view' => 'custom-menu',
    ])
!!}
```
Menu in the location 'primary-menu' will be generated using a custom view in `/platform/themes/your-theme/partials/custom-menu.blade.php`