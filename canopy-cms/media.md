---
author:
    name: Mohammad Prince
order: 73
---

## File Upload

You can create your custom upload with `RvMedia` facade
```
rv_media_handle_upload(request()->file('file'), 0, 'your-folder');
```
## Upload file from a path
You can use a path with to simulate a file upload `UploadedFile` and upload it using `RvMedia::handleUpload()`

Example:
```php
$fileUpload = new \Illuminate\Http\UploadedFile(database_path('files/example.png'), 'example.png', 'image/png', null, true);
$image = \RvMedia::handleUpload($fileUpload, [destination-folder]);
```
Note: You can use `base_path()` as well to get the file path.
