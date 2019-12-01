# Laravel package for Fpdf

This repository implements a simple [ServiceProvider](https://laravel.com/docs/master/providers)
that creates a singleton instance of the Fpdf PDF library - easily accessible via a [Facade](https://laravel.com/docs/master/facades) in [Laravel](https://laravel.com/).  

See [FPDF homepage](http://www.fpdf.org/) for more information about the usage.

## Installation using [Composer](https://getcomposer.org/)
```sh
$ composer require mycools/laravel-fpdf
```

## Usage

### Laravel >= 5.5
Enjoy the auto discovery feature. 

### Laravel <5.5
To use the static interfaces (facades) you need to add the following lines to your `config/app.php`. The `[1]` is for
registering the service provider, the `[2]` are for specifying the facades:

```php
// config/app.php

return [

    //...
    
    'providers' => [
        // ...
        
        /*
         * Application Service Providers...
         */
        // ...
        Mycools\Fpdf\FpdfServiceProvider::class, // [1]
    ],
    
    // ...
    
    'aliases' => [
        // ...
        'Fpdf' => Mycools\Fpdf\Facades\Fpdf::class, // [2]
]
```

Now you can use the facades in your application. 

## Configuration (optional)
Run   
`php artisan vendor:publish --provider="Mycools\Fpdf\FpdfServiceProvider" --tag=config`  
to publish the configuration file to `config/fpdf.php`.  
  
Open this file and enter the correct page settings, if you do not want the defaults.

## Basic example

If you want to use the facade you can see a basic example here:

```php
// app/Http/routes.php | app/routes/web.php

Route::get('/', function () {

    Fpdf::AddPage();
    Fpdf::SetFont('Courier', 'B', 18);
    Fpdf::Cell(50, 25, 'Hello World!');
    Fpdf::Output();

});
```

Of course you can also inject the singleton instance via dependency injection. See an example here:

```php
// app/Http/routes.php | app/routes/web.php

Route::get('/', function (Mycools\Fpdf\Fpdf\Fpdf $fpdf) {

    $fpdf->AddPage();
    $fpdf->SetFont('Courier', 'B', 18);
    $fpdf->Cell(50, 25, 'Hello World!');
    $fpdf->Output();

});
```

```dotenv
FPDF_VAPOR_HEADERS=true
```
