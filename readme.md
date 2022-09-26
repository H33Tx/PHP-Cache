# PHP Cache

Simple but powerful caching system, written in PHP.

## Usage

Paste the code below at the start when you want to cache your file:

```php
$cachefile = "change-this.html";
$cachetime = 2628288; // Default is one month, in seconds

// Serve from the cache if it is younger than $cachetime
if (file_exists($cachefile) && time() - $cachetime < filemtime($cachefile)) {
    echo "<p style='display:none'>Cached copy, generated " . date('d/m/Y H:i', filemtime($cachefile)) . " SERVER TIME</p>";
    $handle = fopen($cachefile, 'rb');
    $buffer = '';
    while (!feof($handle)) {
        $buffer = fread($handle, 4096);
        echo $buffer;
        ob_flush();
        flush();
    }
    fclose($handle);
    // Place additional code/html to be executed/displayed before exiting
    exit;
}

ob_start(); // Start the output buffer
```

Make sure to set `$cachefile` to the proper file and if it's inside a directory, make sure it exists.

After that, `include("cache");` at the point, where you want to stop caching the file.

## FAQ

**Does it work with larger Cached files?** Yes, it does.

**Can I put the `cache.php` file inside a subdirectory?** Yes, you can.

**Will it work, if I store that cache file inside a directory?** Yes, it works. You just need to properly specify the path.

## Donate

If you liked this small piece of code, make sure to become a supporter:
- [Ko-Fi.com/saintly](https://ko-fi.com/saintly)
- [PayPal: yuki.akihabara@yandex.com](https://paypal.me/WOLFRAMEdev)

## License

Licensed unter the MIT License. See LICENSE.