---
author:
    name: Jan Valo
order: 70
---
# Forms/Fields

Canopy CMS is making use of [laravel-form-builder](https://kristijanhusak.github.io/laravel-form-builder/) library to build backend forms. 

Example:
```php
$this
    ->setUpModel(new {Plugin})
    ->setValidatorClass({Plugin}Request::class)
    ->withCustomFields()
    ->add('field_name', 'text', [
        'label'      => __('Field label'),
        'label_attr' => ['class' => 'control-label required'],
        'attr'       => [
        'placeholder'  => __('Placeholder'),
        'data-counter' => 120,
    ],
]);
```
## Form fields

### Input fields 
Includes Text, Password, Email, Number, Textarea
```php
->add('field_name', 'text', [ // "text" can be changed to "password", "email", "number" or "textarea"
    'label'      => __('Field name'),
    'label_attr' => ['class' => 'control-label required'], // Add class "required" if that is mandatory field
    'attr'       => [
        'placeholder'  => __('Placeholder'),
        'data-counter' => 120, // Maximum characters
    ],
])
```
### Toggle field
```php
->add('field_name', 'onOff', [
    'label'         => __('Field label'),
    'label_attr'    => ['class' => 'control-label'],
    'default_value' => false,
    ])
```

### Editor field
Creates a WYSIWYG editor for HTML content
```php
->add('field_name', 'editor', [
    'label'      => __('Field label'),
    'label_attr' => ['class' => 'control-label'],
    'attr'       => [
        'with-short-code' => false, // if true, it will add a button to select shortcode
        'without-buttons' => false, // if true, all buttons will be hidden
    ],
])
  ```
### Select
```php
->add('field_name', 'select', [ // Change "select" to "customSelect" for better UI
    'label'      => __('Field label'),
    'label_attr' => ['class' => 'control-label required'], // Add class "required" if that is mandatory field
    'choices'    => [
        1 => __('Option 1'),
        2 => __('Option 2'),
    ],
])
  ```
### Radio
```php
->add('field_name', 'customRadio', [
    'label'      => __('Field label'),
    'label_attr' => ['class' => 'control-label'],
    'choices'    => [
        ['option1', 'Option 1'],
        ['option2', 'Option 2'],
    ],
])
  ```
### Image field
```php
->add('field_name', 'mediaImage', [
    'label'      => __('Field label'),
    'label_attr' => ['class' => 'control-label'],
])
  ```
### List of images field
```php
->add('field_name[]', 'mediaImages', [
    'label'      => __('Field label'),
    'label_attr' => ['class' => 'control-label'],
    'values'     => $this->model ? json_decode($this->field_name, true) : [],
])
  ```

### File field
```php
->add('field_name', 'mediaFile', [
    'label'      => __('Field label'),
    'label_attr' => ['class' => 'control-label'],
])
  ```
### Color field
```php
->add('field_name', 'color', [
    'label'      => __('Field label'),
    'label_attr' => ['class' => 'control-label'],
])
  ```
### Time field
```php
->add('field_name', 'time', [
    'label'      => __('Field label'),
    'label_attr' => ['class' => 'control-label'],
])
  ```
### Number field with input mask
```php
Assets::addScripts(['input-mask']);

->add('field_name', 'text', [
    'label'      => __('Field label'),
    'label_attr' => ['class' => 'control-label'],
    'attr'       => [
        'id'    => 'field_name',
        'class' => 'form-control input-mask-number',
    ],
])
  ```
### Date picker field
```php
->add('field_name', 'text', [
    'label'         => __('Field label'),
    'label_attr'    => ['class' => 'control-label'],
    'attr'          => [
        'class'            => 'form-control datepicker',
        'data-date-format' => 'yyyy/mm/dd',
    ],
    'default_value' => now(config('app.timezone'))->format('Y/m/d'),
])
  ```
### Repeater fields
// If your model has columns options, it will populate $model->options to repeater value.
```php
$repeaterValue = $this->model->options;

// Or

$repeaterValue = json_encode([
    [
        [
            'key'   => 'text',
            'value' => 'test 1',
        ],
        [
            'key'   => 'image',
            'value' => 'news/4.jpg',
        ],
        [
            'key'   => 'textarea',
            'value' => 'test 2',
        ],
    ],
    [
        [
            'key'   => 'text',
            'value' => 'Test 3',
        ],
        [
            'key'   => 'image',
            'value' => 'news/4.jpg',
        ],
        [
            'key'   => 'textarea',
            'value' => 'Test 4',
        ],
    ],
]);

->add('options', 'repeater', [
    'label'      => __('Repeater field'),
    'label_attr' => ['class' => 'control-label'],
    'fields' => [
        [
            'type'       => 'text',
            'label'      => __('Text'),
            'label_attr' => ['class' => 'control-label required'],
            'attributes' => [
                'name'    => 'text',
                'value'   => null,
                'options' => [
                    'class'        => 'form-control',
                    'data-counter' => 255,
                ],
            ],
        ],
        [
            'type' => 'mediaImage',
            'label'      => __('Image'),
            'label_attr' => ['class' => 'control-label'],
            'attributes' => [
                'name'    => 'image',
                'value'   => null,
            ],
        ],
        [
            'type'       => 'textarea',
            'label'      => __('Textarea'),
            'label_attr' => ['class' => 'control-label'],
            'attributes' => [
                'name'    => 'textarea',
                'value'   => null,
                'options' => [
                    'class'        => 'form-control',
                    'data-counter' => 255,
                    'rows' => 3,
                ],
            ],
        ],
    ],
    'value' => $repeaterValue,
])
  ```
### Form layouts
Default layout template for form is core.base::forms.form, you can set other layout for form.

Example:
```php
->setFormOption('template', 'core.base::forms.form-modal')
```
By default, a form will have 2 columns. It's separated by a breaking point. You can set it by using:
```php
->setBreakFieldPoint('field_name');
  ```
### Row with multiple fields
```php
$this
    ->add('rowOpen1', 'html', [
        'html' => '<div class="row">',
    ])
    ->add('field1', 'text', [
        'label'      => 'Field 1',
        'label_attr' => ['class' => 'control-label'],
        'wrapper'    => [
            'class' => 'form-group col-md-6',
        ],
    ])
    ->add('field2', 'text', [
        'label'      => 'Field 2',
        'label_attr' => ['class' => 'control-label'],
        'wrapper'    => [
            'class' => 'form-group col-md-6',
        ],
    ])
    ->add('rowClose1', 'html', [
        'html' => '</div>',
    ]);
  ```
If you want to have 3 fields on a row, just need to change col-md-6 to col-md-4 and add 1 more field inside rowOpen1 and rowClose1.

### Add columns to existing form

```php
add_filter(BASE_FILTER_BEFORE_RENDER_FORM, function ($form, $data)
{
if (get_class($data) == \Canopy\Blog\Models\Post::class) {

        $test = \MetaBox::getMetaData($data, 'test', true);

        $form
            ->add('test', 'text', [
                'label'      => __('Test Field'),
                'label_attr' => ['class' => 'control-label'],
                'value'      => $test,
                'attr'       => [
                    'placeholder' => __('Test'),
                ],
            ]);

    }

    return $form;
}, 120, 3);

add_action(BASE_ACTION_AFTER_CREATE_CONTENT, 'save_addition_fields', 120, 3);
add_action(BASE_ACTION_AFTER_UPDATE_CONTENT, 'save_addition_fields', 120, 3);

/**
* @param string $screen
* @param Request $request
* @param Model $data
  */
  function save_addition_fields($screen, $request, $data)
  {
      if (get_class($data) == \Canopy\Blog\Models\Post::class) {
          MetaBox::saveMetaBoxData($data, 'test', $request->input('test'));
      }
  }
  ```
  Display the value of Test field in platform/themes/[your-theme]/views/post.blade.php.
```php
  \MetaBox::getMetaData($post, 'test', true);
  ```
  ### Add blade view file
  replace the **blade_file_goes_here** to your blade file directory

```php
    $this->add('rowClose1', 'html', [
        'html' => '. view("plugins/ecommerce::blade_file_goes_here") .'
    ]);
```

### Pass data to blade view

```php
    $this->add('rowClose1', 'html', [
	    'html' => '. view("plugins/ecommerce::blade_file_goes_here", ['data' => $this->getModel()]) .'
    ]);
```