# Vendor Stream Wrapper module #

## Overview ##
Drupal and Composer working together is great for management of external
libraries that can be integrated into Drupal sites. It is a good practice to
have the /vendor directory outside the webroot, and this is what the[Drupal
Composer template](https://github.com/drupal-composer/drupal-project) does. The
problem with moving the vendor out of the webroot however comes when trying to
provide public URLs to files in the /vendor directory, such as CSS or JS files
that are part of an external library.

This module provides a new stream wrapper, `vendor://`, that allows for
referencing of files in the vendor directory. It works much the same as the
`private://` file wrapper provided by Drupal core. Along with this
stream wrapper, this module sets up `*.libraries.yml` files to be parsed for
`vendor://` references, as can be seen in the example below:

example.libraries.yml:
```
some_library:
  js:
    vendor://vendor-name/package-name/js/some_file.js: {}
  css:
    theme:
      vendor://vendor-name/package-name/css/some_file.css: {}
```

The module also provides a helper function, `vendor_stream_wrapper_create_url()`
for resolving vendor files to public facing URLs:

```
$public_url = vendor_stream_wrapper_create_url('vendor://vendor/package/file.css');
```
