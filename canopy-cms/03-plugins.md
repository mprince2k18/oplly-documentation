---
author:
    name: Jan Valo
order: 80
---
# Plugins

Plugins are packages that are loaded using custom configuration that is merged and autoloaded with the 
main composer in the project root. Each plugin is a laravel package

The plugin configuration is defined in the plugin root folder as a JSON file called ```plugin.json```.

```json lines
{
    "name": "Demo",
    "namespace": "Canopy\\Demo\\",
    "provider": "Canopy\\Demo\\Providers\\DemoServiceProvider",
    "author": "Plugin Author",
    "version": "1.0",
    "description": "The description for plugin"
}
```

Plugin needs to include a handler class in the ```/src``` folder that dictates 3 main events
for the plugin where we can specify custom actions

```php
namespace Canopy\Demo;

use Schema;
use Canopy\Base\Interfaces\PluginInterface;

class Plugin implements PluginInterface
{
    /**
    * @return void
    */
    public static function activate()
    {
    }

    /**
    * @return void
    */
    public static function deactivate()
    {
    }
    
    /**
    * @return void
    */
    public static function remove()
    {
    }
}
```
### Permissions
Every plugin needs to have sets of permissions defined that are stored as config in ```/config/permissions.php```
```php
return [
    [
        'name' => 'Demo',
        'flag' => 'demo.list',
    ],
    [
        'name' => 'Create',
        'flag' => 'demo.create',
        'parent_flag' => 'demo.list',
    ],
    [
        'name' => 'Edit',
        'flag' => 'demo.edit',
        'parent_flag' => 'demo.list',
    ],
    [
        'name' => 'Delete',
        'flag' => 'demo.delete',
        'parent_flag' => 'demo.list',
    ],
];
```

### Translations
To support i18n we can place lang variables in ```resources/lang/en/plugin.php```

The rest of the ```/src``` can include standard folders for Laravel package.
The folder should include plugin specific Models, Views and Controllers.

### Forms
Additionally, the folder can include custom forms used in the backend that will
be located in the ```/src/Forms``` folder. This declares a form class that is used for add/edit operations
in the backend. Example below shows a simple form. See ```Canopy\Base\Forms\FormAbstract``` for details and
all available methods. See Fields page for the full list of available fields

```php
<?php

namespace Canopy\Ecommerce\Forms;

use Canopy\Base\Forms\FormAbstract;
use Canopy\Ecommerce\Models\Product;
use EcommerceHelper;

class ProductForm extends FormAbstract
{
    /**
     * {@inheritDoc}
     */
    public function buildForm()
    {
        $this
            ->setupModel(new Product)
            ->add('title', 'text', [
                'label'      => trans('plugins/ecommerce::products.form.title'),
                'label_attr' => ['class' => 'text-title-field required'],
                'attr'       => [
                    'placeholder'  => trans('core/base::forms.title_placeholder'),
                    'data-counter' => 120,
                ],
            ])
            ->add('description', 'editor', [
                'label'      => trans('core/base::forms.description'),
                'label_attr' => ['class' => 'control-label'],
                'attr'       => [
                    'rows'         => 2,
                    'placeholder'  => trans('core/base::forms.description_placeholder'),
                    'data-counter' => 1000,
                ],
            ])
            ->add('content', 'editor', [
                'label'      => trans('plugins/ecommerce::products.form.content'),
                'label_attr' => ['class' => 'text-title-field'],
                'attr'       => [
                    'rows'            => 4,
                    'with-short-code' => true,
                ],
            ]);
    }
}
```
