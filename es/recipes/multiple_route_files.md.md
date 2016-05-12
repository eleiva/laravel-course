# Multiples archivos de enrutamiento

Ventajas: Mejor organizacion de las rutas de nuestra aplicacion. A medida que crece es recomendable separar un archivo gigante de rutas, por varios.

Un buen ejemplo es si tenemos una api publica. 
De esta forma tendremos que modificar el file RouteServiceProvider.php e incluir las rutas correspondientes como sigue:

```
<?php

namespace App\Providers;

use Illuminate\Foundation\Support\Providers\RouteServiceProvider as ServiceProvider;
use Illuminate\Routing\Router;

class RouteServiceProvider extends ServiceProvider
{

    /**
     * This namespace is applied to the controller routes in your routes file.
     *
     * In addition, it is set as the URL generator's root namespace.
     *
     * @var string
     */
    protected $webNamespace = 'App\Http\Controllers\Web';

    protected $apiNamespace = 'App\Http\Controllers\Api';

    /**
     * Define your route model bindings, pattern filters, etc.
     *
     * @param  \Illuminate\Routing\Router $router
     *
     * @return void
     */
    public function boot(Router $router)
    {
        //

        parent::boot($router);
    }

    /**
     * Define the routes for the application.
     *
     * @param  \Illuminate\Routing\Router $router
     *
     * @return void
     */
    public function map(Router $router)
    {

        /*
        |--------------------------------------------------------------------------
        | Web Router 
        |--------------------------------------------------------------------------
        */

        $router->group(['namespace' => $this->webNamespace], function ($router) {
            require app_path('Http/routes.web.php');
        });

        /*
        |--------------------------------------------------------------------------
        | Api Router 
        |--------------------------------------------------------------------------
        */

        $router->group(['namespace' => $this->apiNamespace], function ($router) {
            require app_path('Http/routes.api.php');
        });

    }
}
```

[101-Para Principiantes](101/boot.md)
