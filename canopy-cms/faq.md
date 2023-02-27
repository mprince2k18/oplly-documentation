---
author:
    name: Mohammad Prince
order: 60
---
## how to create a config file & register?

create a php file into config folder. For example: ``` directory: platform\plugins\ecommerce\config\review.php ```

The config will look like this:

```php
    return [ 
        'enable' => true,
    ]; 
```

Now we need to register the config file to the providers. For example: ``` platform\plugins\ecommerce\src\Providers\EcommerceServiceProvider.php ```

Find the ```boot()``` function. inside ```loadAndPublishConfigurations([])``` pass the config file name here.

For example: 

```php
    loadAndPublishConfigurations(['review'])
```

## how to create a route file & register?

create a php file into routes folder. For example: ``` directory: platform\plugins\ecommerce\routes\zoom.php ```

```php
    <?php

    Route::group(['namespace' => 'Canopy\Ecommerce\Http\Controllers', 'middleware' => ['web', 'core']], function () {
        Route::group(['prefix' => BaseHelper::getAdminPrefix(), 'middleware' => 'auth'], function () {
            Route::group(['prefix' => 'zoom', 'as' => 'zoom.'], function () {
                
                Route::get('/setup', [
                    'as'   => 'index',
                    'uses' => 'ZoomController@index',
                ]);

            });
        });
    });
```

Now we need to register the route file to the providers. For example: ``` platform\plugins\ecommerce\src\Providers\EcommerceServiceProvider.php ```

Find the ```boot()``` function. inside ```loadRoutes([])``` pass the route file name here.

For example: 

```php
    loadRoutes(['zoom'])
```

## how to inject CSS or JS in a specific page?

Answer goes here.

## how to get the charge_id?

Answer goes here.

## how to get the invoice number?

Answer goes here.

## how book live works?

Answer goes here.

## how email template works?

Answer goes here.
## how to add variables to email template?

First you need to add the variable to the config. Go to 
```php 
    config\plugins\ecommerce\email.php 
```

Find 'variables' key, now add 'zoom_url'.

```php
    'variables'   => [
        'zoom_url'         => 'Zoom URL'
    ],
```

Then we need to setEmailVariables at 

```php
    platform\plugins\ecommerce\src\Supports\OrderHelper.php
```

```php
    public function setEmailVariables($order)
    {
        return EmailHandler::setModule(ECOMMERCE_MODULE_SCREEN_NAME)
            ->setVariableValues([
            'zoom_url'          => 'https://us04web.zoom.us'
        ]);
    }
```

All set. Now we can use the 'zoom_url' at the .tpl file.
