# Imagery for Laravel

**NOTE: Still under initial development, not yet functional. Initial release
 will be available in the next week or so. Stay tuned. :)**

## Goal
Provide developers a simplified solution to serving dynamic and optimized images,
 regardless if the user uploaded unoptimized images. This is particularly
 important for blogs and CMS'.

## Reasoning
There are some online third-party services out there that can handle this. But
 what do you do if you don't want the extra expense or complexity, or are
 serving sensitive images in an intranet setting that cannot be trusted to 3rd-
 party vendors? This package aims to fill that gap, and more-over, improve user
 experience in your application by loading assets faster, and at the right sizes.

## Installation
1. Pull in the package:
  ```sh
  composer require genealabs/imagery
  ```

2. Register the service provider in `\config\app.php`:
  ```php
  GeneaLabs\LaravelImagery\Providers\LaravelImageryService::class,
  ```

3. Publish the assets:
  ```sh
  php artisan imagery:publish --assets
  ```

## Configuration
Annotations to be added...
```php
<?php

return [
    'storage-folder' => 'imagery-cache/',
    'size-presets' => [
        'thumbnail' => 150,
        'extra-small' => 480,
        'small' => 768,
        'medium' => 992,
        'large' => 1200,
    ]
];
```

## Usage
### Options
#### alwaysPreserveAspectRatio
**type: bool, default: true**
Allow distortion of images if set to false.

#### doNotCreateDerivativeImages
**type: bool, default: false**
Prevent Laravel Imagery from automatically creating preset image sizes. This
 should normally be left on, unless specifically not needed.

#### overrideScreenConstraint
**type: bool, default: false**
Allows overriding of constraining image to screen dimensions.

#### screenConstraintMethod
**type: string, options: 'contain|cover', default: contain.**
Determine how screen sizing constraints work. Just like the CSS `background-size`
 properties. `cover` will try to size the image to fill the boundaries of the size
 provided (or if not provided, use the screen size), while `contain` will size
 the image to fit within those bounds.

## Planned Features
- Detects visitor's screen dimensions and optimizes the image for it.
- Your images don't have to be in a public folder to be served, imagery creates
 derivative images in its own public folder.
- Further optimizes derivative images through lossless compression (using async
 queue so as not to hold things up).
