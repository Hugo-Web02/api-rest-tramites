# API REST Tramites en Laravel🚀

##### La API permitirá realizar operaciones CRUD (Crear, Leer, Actualizar y Eliminar) utilizando los métodos HTTP (POST, GET, PUT y DELETE) para administrar la información de los tramites en una base de datos.

##### Requisitos previos:

Antes de comenzar, asegúrate de tener instalado PHP, Composer y cualquier servidor de apache
php --version
composer --version
xammp/wamp/laravel herd

##### Crear un proyecto de Laravel

composer create-project laravel/laravel api-rest-tramites

##### Acceder al proyecto creado

cd api-rest-tramites

##### Generación de clave de aplicación

php artisan key:generate

##### Crear Base de Datos en MySQL

hugo20271015_tramites

##### Configuración de la base de datos

Abre el archivo .env y configura los detalles de tu base de datos, como el nombre de la base de datos, el nombre de usuario y la contraseña.

DB_CONNECTION=mysql
DB_HOST=mysql-hugo20271015.alwaysdata.net
DB_PORT=3306
DB_DATABASE=hugo20271015_tramites
DB_USERNAME=hugo20271015
DB_PASSWORD=Hugova2002

##### Ejecución del servidor de desarrollo

php artisan serve
php artisan serve --port=8500

##### Para Crear mi Modelo, Controlador y Migraciones

php artisan make:model Empleado -mcr

##### Correr las migraciones

php artisan migrate

##### Definir los campos para mi tabla en la Migracion correspondiente a mi tabla

    Schema::create('tramites', function (Blueprint $table) {
$table->id();
$table->string('nombre');
$table->text('descripcion')->nullable();
$table->enum('estado', ['pendiente', 'en proceso', 'completado'])->default('pendiente');
$table->date('fecha_creacion');
$table->timestamps();
});

##### Definir los campos en mi modelo para trabahar con mi tabla

protected $table = 'tramites'; // Nombre de la tabla en la base de datos

protected $fillable = [
    'nombre',
    'descripcion',
    'estado',
    'fecha_creacion'
];

##### Define las rutas de nuestra API en el archivo routes/api.php

use App\Http\Controllers\TramiteController;

Route::get('/tramites', [TramiteController::class, 'index']);
Route::post('/tramites', [TramiteController::class, 'store']);
Route::get('/tramites/{id}', [TramiteController::class, 'show']);
Route::put('/tramites/{id}', [TramiteController::class, 'update']);
Route::delete('/tramites/{id}', [TramiteController::class, 'destroy']);



## Lista de Endpoint API

#### Método GET ✅
👉 http://127.0.0.1:8500/api/tramites

<img width="883" height="743" alt="24" src="https://github.com/user-attachments/assets/177cdeed-81e3-4e70-8501-d10176667dbf" />



#### Método POST ✅
👉 http://127.0.0.1:8500/api/tramites

<img width="886" height="696" alt="23" src="https://github.com/user-attachments/assets/8894bc69-f607-4db7-9a01-ea2ecf74ba93" />


#### Método GET ✅
👉 http://127.0.0.1:8500/api/tramites/2


<img width="888" height="575" alt="25" src="https://github.com/user-attachments/assets/21f93c9c-2396-44c4-897e-8383701b1263" />


#### Método PUT ✅
👉 http://127.0.0.1:8500/api/tramites/2

<img width="892" height="745" alt="26" src="https://github.com/user-attachments/assets/7850348d-2928-43cb-b3de-a579d3352447" />


#### Método DELETE ✅
👉 http://127.0.0.1:8500/api/tramites/2

<img width="887" height="437" alt="31" src="https://github.com/user-attachments/assets/311b7d2b-626c-4bd0-aa7d-074a69e8c7f4" />


####Definir los métodos o funciones para cada una de tus rutas en un controlador

    public function index()
{
$tramites = Tramite::all();
return response()->json($tramites, 200);
}

public function store(Request $request)
{
$tramite = Tramite::create($request->all());
return response()->json($tramite, 201);
}

public function show($IdTramite)
{
$tramite = Tramite::findOrFail($IdTramite);
return response()->json($tramite, 200);
}

public function update(Request $request, $IdTramite)
{
$tramite = Tramite::findOrFail($IdTramite);
$tramite->update($request->all());
return response()->json($tramite, 200);
}

public function destroy($IdTramite)
{
$tramite = Tramite::findOrFail($IdTramite);
$tramite->delete();
return response()->json(['message' => 'Trámite eliminado correctamente'], 200);
}

#### Notas con las Migraciones

- Subir la migracion.
    php artisan migrate
- Deshacer la última migración ejecutada
    php artisan migrate:rollback

- Deshacer todas las migraciones
    php artisan migrate:reset

- Muestrar todas las migraciones indicando cuales han sido ejecutadas
    php artisan migrate:status
- Deshace todas las migraciones y las ejecuta otra vez.
    php artisan migrate:refresh
