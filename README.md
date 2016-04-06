# Model generator
Auto-generate models for a Laravel 5 project.

Connects to your existing database and auto-generates models based on existing schema.
 - Support for multiple dababases.
 - Support for magic properties.
 - Support for custom methods.

# Installation
Add ```"mrcorex/laravel-model-generator": "^1"``` to your composer.json file.

Add a configuration-file called corex and add following code to it. Modify it to suit your needs.
```php
return [
    'laravel-model-generator' => [
        'path' => base_path('app/Models'),
        'namespace' => 'App\Models',
        'databaseSubDirectory' => true,
        'tablePublic' => false
    ]
];
```

To register it and make sure you have this option available for development only, add following code to AppServiceProviders@register.
```php
public function register()
{
    if ($this->app->environment() == 'local') {
        $this->app->register('CoRex\Generator\ModelGeneratorProvider');
    }
}
```

# Help
```php artisan help make:models```

Arguments:
 - database: Name of database to generate models from. It will be added to namespace/path for separation of models. It is possible to disable this.
 - tables: Comma separated table names to generate. Specify "." to generate all.

# TODO
 - Add SQL for rest of supported drivers.
