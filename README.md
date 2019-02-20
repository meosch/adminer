# adminer_install
Adminer setup with additional files they way we like it for a quick setup.

## Adminer in a sub-folder of the Drupal 8 Webroot

For Drupal8 development environments running Adminer in a sub-folder of the webroot may be your only option. To do so you need to make some changes to the `.htaccess` file.

After the following section in `.htaccess`, ~line 143:

```
  # Pass all requests not referring directly to files in the filesystem to
  # index.php.
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteCond %{REQUEST_URI} !=/favicon.ico
  RewriteRule ^ index.php [L]
```

Add the following to allow access to the adminer folder in the webroot.

```
  # Allow access to PHP files in /adminer folder so we can analyze the database using Adminer:
  RewriteCond %{REQUEST_URI} !/adminer/[^/]*\.php$
```

This is base of the code a few lines below this to allow `core` (~ line 149 in the original).
