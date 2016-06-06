# Model generator
Auto-generate models for a Laravel 5 project.

Connects to your existing database and auto-generates models based on existing schema.
 - Support for multiple dababases.
 - Support for magic properties.
 - Support for custom methods.
 - Support for guarded fields.
 - Support for "extends".
 - Support for addition column-attributes after magic properties.
 - Support for building constants in model.

# Installation
Add ```"mrcorex/laravel-model-generator": "^1"``` to your composer.json file.

Add a configuration-file called corex and add following code to it. Modify it to suit your needs.
```php
return [
    'laravel-model-generator' => [
        'path' => base_path('app/Models'),
        'namespace' => 'App\Models',
        'databaseSubDirectory' => true,
        'extends' => '',
        'const' => [
            '{connection}' => [
                '{table}' => [
                    'id' => '{id}',
                    'name' => '{name}',
                    'prefix' => '{prefix}',
                    'suffix' => '{suffix}',
                    'replace' => [
                        'XXXX' => 'YYYY',
                    ]
                ]
            ]
        ]
    ]
];
```

Settings:
 - **path** - where models are saved.
 - **namespace** - namespace of models.
 - **databaseSubDirectory** - true/false if name of database-connection should be applied to namespace/directory. Name will automatically be converted to PascalCase.
 - **extends** - class to extend instead of "Illuminate\Database\Eloquent\Model".
 - **const** - (optional) This section is used to specify connections and tables which should contains constants from content of table.
 - **{connection}** - (optional) Name of connection.
 - **{table}** - (optional) Name of table.
 - **{id}** - (required) Name of field to get id from used in constant as value.
 - **{name}** - (required) Name of field to get name of constant.
 - **{prefix}** - (optional) Prefix to add to each name of constant.
 - **{suffix}** - (optional) Suffix to add to each name of constant.
 - **replace** - (optional) Values to replace in name of constant.

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

Options:
 - guarded: Comma separated list of guarded fields.

# TODO
 - Add SQL for rest of supported drivers.
