---
author:
    name: Mohammad Prince
order: 50
---
# Blade Structure

The frontend and the backend has different extends layouts. When you create a new blade for frontend or backend follow this skeleton layout.

## Frontend Blade Skeleton

Creating a new blade file you have the header, footer automatically. To get the navigation or assets you have to extends the master template. Here is the example:

```php
    @extends(Theme::getThemeNamespace() . '::views.[master-file-directory]')
```

Now you need to replace the ```[master-file-directory]``` to your project master directory. Here is the live example:

```php
    @extends(Theme::getThemeNamespace() . '::views.ecommerce.customers.master')
```

Now for the content section we need to call ```@section('content')``` for the main content display.

```php
@section('content')
    // content goes here
@endsection
```

## Backend Blade Skeleton

> *Coming soon*