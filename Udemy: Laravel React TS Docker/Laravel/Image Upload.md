Simple method for uploading

```php
class ImageController extends Controller
{
    public function upload(Request $request) {

        $file = $request->file(key: "img");

        $name = \Str::random(length: 10);

        $url = Storage::putFileAs(
            "images",
            $file,
            $name . "." . $file->extension()
        );

        return [
            "url" => $url
        ];
    }
}
```

If the images are public, replace the value of `root` from `storage_path('app')` -> `public_path()`

```php
// config/filesystems.php
    'disks' => [
        'local' => [
            'driver' => 'local',
            'root' => public_path(),
            // 'root' => storage_path('app'),
            'throw' => false,
        ],
	
	/**
	 **
	 */
	
	]
```


- In this case, the image will be uploaded to `public/images`. 
- It can be accessed from http://hostname/images/file_name_here.extension