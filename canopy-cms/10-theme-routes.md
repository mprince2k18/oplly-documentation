---
author:
    name: Mohammad Prince
order: 71
---

# Theme routes
Routes for the theme are located in 
**frontend**: `/platform/themes/shopwise/routes/[route-file].php`
**backend**: `/platform/plugins/[your-package]/routes/[route-file].php`

To ensure that default routes do not override your own routes, please place them at the top of the file.
```php
<?php

// Custom routes
// If you don't need to add your custom routes, you can delete this route group.
Route::group(['namespace' => 'Theme\[your-theme]\Http\Controllers', 'middleware' => 'web'], function () {
    Route::group(apply_filters(BASE_FILTER_GROUP_PUBLIC_ROUTE, []), function () {
        // Add your custom route here
        // Ex: Route::get('/oplly', '[your-theme]Controller@getHello');
    });
});

Theme::routes();

Route::group(['namespace' => 'Theme\[your-theme]\Http\Controllers', 'middleware' => 'web'], function () {
    Route::group(apply_filters(BASE_FILTER_GROUP_PUBLIC_ROUTE, []), function () {
        Route::get('oplly', [
            'as'   => 'public.index',
            'uses' => '[your-theme]Controller@index',
        ]);
    });
});
```