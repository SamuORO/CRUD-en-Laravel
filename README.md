# Laboratorio: Implementación de un CRUD de productos en Laravel

<p align="center">
  <img src="https://img.shields.io/badge/PHP-8.3.28-777BB4?logo=php&logoColor=white" alt="PHP">
  <img src="https://img.shields.io/badge/Laravel-13.37.0-FF2D20?logo=laravel&logoColor=white" alt="Laravel">
  <img src="https://img.shields.io/badge-MySQL-Database-4479A1?logo=mysql&logoColor=white" alt="MySQL">
  <img src="https://img.shields.io/badge-Bootstrap-Frontend-7952B3?logo=bootstrap&logoColor=white" alt="Bootstrap">
</p>

## 1. Introducción

Laravel es un framework de PHP que permite desarrollar aplicaciones web mediante una estructura organizada, facilitando la separación de responsabilidades y el mantenimiento del código. En este laboratorio se trabajó con el patrón Modelo-Vista-Controlador (MVC) para construir un CRUD de productos.

CRUD corresponde a las operaciones *Create, Read, Update y Delete* (crear, leer, actualizar y eliminar). La aplicación permite registrar productos, consultar su información, editar sus datos y eliminarlos mediante una interfaz desarrollada con Blade y Bootstrap.

El proyecto también permitió configurar una base de datos MySQL en WampServer, ejecutar migraciones, definir rutas y controladores, validar formularios y solucionar inconvenientes de compatibilidad y configuración encontrados durante la práctica.

## 2. Objetivos

- Comprender la estructura de un proyecto Laravel y su relación con el patrón MVC.
- Configurar Laravel en un entorno de desarrollo local con Windows 11 y WampServer.
- Conectar la aplicación con una base de datos MySQL.
- Ejecutar migraciones para crear las tablas necesarias.
- Crear un modelo para representar los productos.
- Implementar las operaciones de creación, consulta, edición y eliminación de productos.
- Utilizar rutas de recursos y un controlador para organizar las operaciones CRUD.
- Diseñar vistas con Blade y Bootstrap.
- Validar los datos recibidos en los formularios antes de guardarlos.
- Identificar y resolver errores de configuración, migraciones y compatibilidad.
- Documentar los resultados obtenidos durante la práctica.

## 3. Requisitos previos y tecnologías utilizadas

Para realizar el laboratorio se utilizaron las siguientes herramientas y tecnologías:

| Tecnología | Detalle |
|:---:|---|
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/13ed7e81-cfcf-45ec-9b0b-5c5b522a955c" />| **Sistema operativo:** Windows 11 |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/2c3a1372-de3d-4bd1-b653-15680e96b570" />| **PHP:** 8.3.28 |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/ffe48f2e-845d-47a2-a4d2-e8f0ab65b080" />| **Composer:** 2.10.3 |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/1601ea0b-57bd-4c9f-a879-c7cdb5816eb8" />| **Laravel Installer:** 5.32.0 · **Laravel Framework:** 13.37.0 (`laravel new`) |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/403b59f3-6fd5-4a29-8510-d93cd0dda1ee" />| **Servidor web:** Apache 2.4.65, incluido en WampServer |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/6df06f68-e255-431d-9c8a-477d491f2c65" />| **Base de datos:** MySQL 8.4.7, administrada con phpMyAdmin 5.2.3 (usuario `root`) |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/d436645b-022d-4d0b-9a77-6f8bcf6039db" />| **Entorno de desarrollo local:** WampServer (`C:\wamp64\www`) |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/e6f29db3-cb0b-4a5e-8738-aefb279b463d" />| **Editor de código:** Visual Studio Code |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/dd9618a2-2e74-4cc0-bfbb-323fd41248dc" />| **Herramientas frontend:** npm (`npm install` y `npm run dev`) con Vite 8.3.4 |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/1601ea0b-57bd-4c9f-a879-c7cdb5816eb8" /> | **Autenticación:** Laravel UI 4.6.3, con scaffolding de Bootstrap |
| <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/e4b25607-0eb9-487a-b70c-142abf23db7d" />| **Navegador web:** Google Chrome |

### 3.1. Verificación de las herramientas

Antes de trabajar en el proyecto se comprobaron las versiones de las herramientas mediante los siguientes comandos:

```powershell
php -v
composer -v
laravel -v
node -v
npm -v
```

Estas herramientas permiten ejecutar el código PHP, administrar las dependencias, crear aplicaciones Laravel y compilar los recursos del frontend.

## 4. Instalación y creación del proyecto

### 4.1. Instalación de Laravel Installer

Se utilizó Composer para instalar el instalador de Laravel de forma global:

```powershell
composer global require laravel/installer
```

Este comando permite utilizar la herramienta `laravel` desde la terminal para crear nuevos proyectos.

### 4.2. Creación del proyecto

Se accedió al directorio de trabajo de WAMP:

```powershell
cd C:\wamp64\www
```

Se creó el proyecto con el nombre `crud`:

```powershell
laravel new crud
```

Después se ingresó a la carpeta del proyecto:

```powershell
cd C:\wamp64\www\crud
```

Se verificó la instalación con:

```powershell
php artisan --version
```

El resultado confirmó que el proyecto utilizaba Laravel Framework 13.37.0.

### 4.3. Primera ejecución de la aplicación

Para comprobar que Laravel funcionaba correctamente, se inició el servidor local:

```powershell
php artisan serve
```

<img width="1291" height="591" alt="image" src="https://github.com/user-attachments/assets/53fca240-91b2-4297-be39-7cd937b21b07" />

Posteriormente, se abrió la dirección local en el navegador:

`http://localhost:8000`

El servidor permite probar la aplicación localmente. Mientras se trabaja con `php artisan serve`, la terminal debe permanecer abierta.

## 5. Arquitectura Modelo-Vista-Controlador (MVC)

Laravel organiza los componentes de la aplicación mediante una estructura que facilita la separación de responsabilidades.

### 5.1. Modelo

Los modelos representan los datos y permiten interactuar con la base de datos mediante Eloquent ORM.

En este proyecto se creó:

- `app/Models/Product.php`: representa los productos almacenados en la tabla `products`.

El modelo utiliza la propiedad `$fillable` para indicar los campos que se pueden asignar de forma masiva:

```php
protected $fillable = [
    'name',
    'description',
    'price',
    'stock',
];
```

<img width="517" height="386" alt="image" src="https://github.com/user-attachments/assets/004a5a81-16d7-4caa-a4a4-021156470ab3" />

Los campos corresponden al nombre, la descripción, el precio y la cantidad disponible de cada producto.

### 5.2. Vista

Las vistas contienen la interfaz que se presenta al usuario. Laravel utiliza Blade para generar páginas HTML y mostrar los datos enviados por los controladores.

Las vistas principales del CRUD se encuentran en `resources/views/products/`:

- `index.blade.php`: muestra la lista de productos.
- `create.blade.php`: contiene el formulario para crear un producto.
- `show.blade.php`: presenta los detalles de un producto.
- `edit.blade.php`: permite modificar los datos de un producto.

Las vistas utilizan `layouts.app` como plantilla base y clases de Bootstrap para mantener una apariencia consistente.

<img width="270" height="137" alt="image" src="https://github.com/user-attachments/assets/c1e2dd43-3174-4c5d-b8df-8511aa492188" />


### 5.3. Controlador

Los controladores reciben las solicitudes y coordinan las acciones que debe realizar la aplicación.

En el laboratorio se trabajó con:

- `app/Http/Controllers/ProductController.php`: contiene las acciones para listar, crear, guardar, mostrar, editar, actualizar y eliminar productos.
- `app/Http/Controllers/HomeController.php`: se adaptó para cargar y mostrar la lista de productos en la ruta `/home`.

El controlador `ProductController` utiliza el modelo `Product` para consultar, guardar, actualizar y eliminar registros.

### 5.4. Rutas

El archivo `routes/web.php` contiene las rutas que permiten acceder a las páginas de la aplicación.

La ruta principal del CRUD se definió mediante:

```php
use App\Http\Controllers\ProductController;

Route::get('/', [ProductController::class, 'index']);

Route::resource('products', ProductController::class);
```

La ruta de recurso genera las rutas habituales de las operaciones CRUD:

| Ruta | Método HTTP | Función |
|---|---|---|
| `/products` | GET | Mostrar la lista de productos |
| `/products/create` | GET | Mostrar el formulario de creación |
| `/products` | POST | Guardar un producto nuevo |
| `/products/{product}` | GET | Mostrar los detalles de un producto |
| `/products/{product}/edit` | GET | Mostrar el formulario de edición |
| `/products/{product}` | PUT/PATCH | Actualizar un producto |
| `/products/{product}` | DELETE | Eliminar un producto |

Durante el proyecto también se conservaron las rutas generadas para la autenticación con Laravel UI:

```php
Auth::routes();

Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])
    ->name('home');
```

La ruta `/home` se modificó para mostrar la lista de productos. La ruta `/products` es la dirección principal de la gestión de productos.

<img width="965" height="321" alt="image" src="https://github.com/user-attachments/assets/0510dd1f-7494-4266-9bde-cf5c131e5e34" />


## 6. Configuración de la base de datos MySQL

### 6.1. Creación de la base de datos

Se utilizó WAMP para ejecutar el servidor de base de datos y phpMyAdmin para administrar las bases de datos desde el navegador.

Se creó la base de datos con el siguiente nombre:

`crud`

Se utilizó MySQL como sistema de gestión de base de datos.

### 6.2. Configuración del archivo `.env`

El archivo `.env` contiene las variables de entorno utilizadas por Laravel para configurar la conexión con la base de datos y otros servicios.

Los valores utilizados para la conexión local fueron:

```dotenv
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=crud
DB_USERNAME=root
DB_PASSWORD=
```

La contraseña se dejó vacía porque el usuario `root` del entorno local no tenía contraseña configurada. Estos valores dependen de la configuración específica de WAMP.

Después de modificar el archivo, se limpió la configuración almacenada en caché:

```powershell
php artisan config:clear
```

Este paso permite que Laravel vuelva a leer las variables actualizadas del archivo `.env`.

Se verificó la conexión mediante:

```powershell
php artisan db:show
```

El comando permitió comprobar que Laravel estaba conectado a MySQL.

### 6.3. Ejecución de las migraciones

Las migraciones permiten definir y crear la estructura de las tablas de la base de datos mediante archivos PHP.

Para ejecutar las migraciones se utilizó:

```powershell
php artisan migrate
```

<img width="1101" height="280" alt="image" src="https://github.com/user-attachments/assets/ba14a5b7-237a-480c-939c-c72a82a32b82" />


Durante la práctica se crearon las tablas iniciales de Laravel y la tabla de productos. Entre las tablas del proyecto se encuentran:

- `users`: almacena la información de los usuarios.
- `cache`: permite gestionar datos almacenados en caché.
- `jobs`: contiene información relacionada con los trabajos en cola.
- `failed_jobs`: registra trabajos en cola que no se completaron correctamente.
- `migrations`: registra las migraciones ejecutadas.
- `products`: almacena los productos del CRUD.

Para verificar el estado de las migraciones se utilizó:

<img width="1415" height="395" alt="image" src="https://github.com/user-attachments/assets/ea404711-f054-4c67-838c-91bc593a330b" />


```powershell
php artisan migrate:status
```

Las migraciones completadas aparecieron con el estado `Ran`.

La tabla `products` contiene los siguientes campos:

| Campo | Función |
|---|---|
| `id` | Identificador único del producto |
| `name` | Nombre del producto |
| `description` | Descripción del producto |
| `price` | Precio del producto |
| `stock` | Cantidad disponible |
| `created_at` | Fecha de creación del registro |
| `updated_at` | Fecha de la última actualización |

<img width="1021" height="120" alt="image" src="https://github.com/user-attachments/assets/3913a8c0-77e5-4409-bc82-e2f7463b4859" />


### 6.4. Respaldo de la base de datos

Como parte de la documentación del laboratorio, se recomienda generar un respaldo de la base de datos.

El respaldo puede obtenerse desde phpMyAdmin siguiendo estos pasos:

1. Seleccionar la base de datos `crud`.
2. Abrir la opción **Exportar**.
3. Seleccionar el formato SQL.
4. Descargar el archivo generado.
5. Guardar una copia en el repositorio, por ejemplo, en `database/backup/crud.sql`.

<img width="888" height="426" alt="image" src="https://github.com/user-attachments/assets/b9c324f0-e18a-4bdb-8f87-449b3eda8b33" />


## 7. Implementación del CRUD de productos

### 7.1. Creación del modelo y del controlador

Se utilizó Artisan para generar el modelo `Product` y el controlador de recursos. El comando de generación de un modelo con migración y controlador de recursos es:

```powershell
php artisan make:model Product -mcr
```

Este comando crea el modelo, una migración y un controlador de recursos. Si los archivos ya existen en el proyecto, no es necesario volver a generarlos; se pueden editar directamente.

El modelo se configuró para permitir la asignación masiva de los campos `name`, `description`, `price` y `stock`.

### 7.2. Estructura de la tabla `products`

La migración de productos define los campos que se guardan en la base de datos. La estructura utilizada contiene un identificador, nombre, descripción, precio, stock y marcas de tiempo.

Después de definir la migración, se ejecutó:

```powershell
php artisan migrate
```

Con esto Laravel creó la tabla `products` en la base de datos `crud`.

### 7.3. Operaciones del controlador

El controlador `ProductController` organiza las acciones del CRUD:

- **Index:** consulta los productos y los envía a la vista `products.index`.
- **Create:** muestra el formulario `products.create`.
- **Store:** valida los datos y crea el registro.
- **Show:** muestra los detalles del producto seleccionado.
- **Edit:** carga el producto y presenta el formulario de edición.
- **Update:** valida los datos y actualiza el registro existente.
- **Destroy:** elimina el producto seleccionado.

Para guardar un producto se validan los campos antes de crear el registro. Las reglas utilizadas son equivalentes a las siguientes:

```php
$validated = $request->validate([
    'name' => 'required|string|max:255',
    'description' => 'nullable|string',
    'price' => 'required|numeric|min:0',
    'stock' => 'required|integer|min:0',
]);

Product::create($validated);
```

Estas reglas requieren un nombre, aceptan una descripción opcional, exigen un precio numérico igual o mayor que cero y un stock entero igual o mayor que cero.

Para actualizar se aplican las mismas reglas y se utiliza el método `update()` sobre el producto seleccionado. Para eliminar, se utiliza `delete()` sobre el registro correspondiente.

### 7.4. Vistas del CRUD con Bootstrap

Las vistas se organizaron dentro de `resources/views/products/` y utilizan `layouts.app` como plantilla base.

- **Lista (`index.blade.php`):** muestra los productos en una tabla con columnas para número, nombre, descripción, precio, stock y acciones.
- **Creación (`create.blade.php`):** presenta los campos para registrar un producto nuevo.
- **Detalles (`show.blade.php`):** muestra la información completa del producto seleccionado.
- **Edición (`edit.blade.php`):** permite modificar el nombre, la descripción, el precio y el stock.

Los formularios utilizan directivas de Blade como `@csrf` para incluir el token de seguridad y, al actualizar o eliminar, `@method('PUT')` o `@method('DELETE')` para indicar el método HTTP correspondiente.

La interfaz utiliza componentes y clases de Bootstrap, como tarjetas, tablas, botones, alertas y formularios, para mantener una presentación uniforme.

<img width="1716" height="456" alt="Captura de pantalla 2026-10-27 154931" src="https://github.com/user-attachments/assets/7ad1ed1a-ba56-423f-a158-9ae1ff74e192" />


### 7.5. Numeración de los productos

En la lista se agregó una numeración consecutiva independiente del identificador real de la base de datos. Para ello, la vista recorre los productos con un índice:

```blade
@forelse ($products as $index => $product)
    <td>{{ $index + 1 }}</td>
@endforelse
```

Así, la columna muestra `1, 2, 3...` según la posición del producto en la lista. Si se elimina un registro, los números visibles se reorganizan automáticamente.

**Importante:** esta numeración es únicamente visual. El campo `id` de MySQL no se reinicia ni se modifica al eliminar productos, porque funciona como identificador único de cada registro.

## 8. Pruebas y resultados obtenidos

### 8.1. Página principal y lista de productos

Se comprobó el acceso a la aplicación mediante:

`http://localhost:8000/`

La ruta principal se configuró para mostrar la lista de productos. También se puede acceder directamente mediante:

`http://localhost:8000/products`

La lista presenta el nombre, la descripción, el precio, el stock y los botones para ver, editar o eliminar cada producto.

<img width="1716" height="456" alt="image" src="https://github.com/user-attachments/assets/e1ad25e4-ce2f-4760-934b-9b1f9d5b4b35" />

### 8.2. Creación de productos

Se accedió al formulario de creación mediante:

`http://localhost:8000/products/create`

Se preparó un formulario con los campos nombre, descripción, precio y stock. Al enviarlo, el controlador valida los datos y guarda el producto si cumple las reglas establecidas.

Después de guardar correctamente, la aplicación redirige a la lista de productos y muestra un mensaje de confirmación.

<img width="1701" height="756" alt="image" src="https://github.com/user-attachments/assets/cc7d2516-3a54-4d30-8b87-934c66877bc0" />


### 8.3. Consulta de productos

Se puede consultar la lista desde `/products` y ver los detalles individuales desde la ruta de cada producto, por ejemplo:

`http://localhost:8000/products/1`

La vista de detalles presenta los datos del producto seleccionado y permite regresar a la lista o abrir su formulario de edición.

<img width="1691" height="530" alt="image" src="https://github.com/user-attachments/assets/0f3d3f9a-a1cf-43f3-8f0c-cb17c37e396d" />

### 8.4. Edición de productos

Se accede al formulario de edición desde el botón **Editar** de la lista. La dirección sigue el formato:

`http://localhost:8000/products/1/edit`

El formulario carga los datos existentes del producto. Al enviar los cambios, el controlador valida la información y actualiza el registro en MySQL.

<img width="1682" height="767" alt="image" src="https://github.com/user-attachments/assets/8f79e968-f67e-45c0-bcc0-d34edb89d65a" />

### 8.5. Eliminación de productos

La lista contiene un botón **Eliminar** para cada registro. La solicitud se envía mediante un formulario `POST` que incluye `@method('DELETE')` y `@csrf`.

Antes de enviar la solicitud, la interfaz solicita confirmación. Si se confirma la acción, Laravel elimina el registro y redirige a la lista.

Después de eliminar un producto, la numeración visual se vuelve a calcular desde uno. Esto no cambia los identificadores reales almacenados en la base de datos.

<img width="1700" height="440" alt="image" src="https://github.com/user-attachments/assets/9132d2b4-0600-4da5-9477-6599f577cc1f" />

### 8.6. Autenticación y página de inicio

Durante el proyecto también se instaló Laravel UI para generar la estructura de autenticación:

```powershell
composer require laravel/ui
php artisan ui bootstrap --auth
```

Se comprobó que la ruta `/register` mostrara el formulario de registro. También se conservó la ruta `/home`, cuyo controlador se adaptó para cargar la lista de productos.

La lista principal del CRUD se encuentra en `/products`, mientras que `/home` muestra la lista según la modificación realizada en `HomeController`.

## 9. Dificultades encontradas y soluciones aplicadas

### 9.1. Configuración incorrecta de la base de datos

**Dificultad:** Laravel intentaba conectarse a una base de datos con un nombre distinto al de la base de datos creada en phpMyAdmin.

**Solución:** se revisó el archivo `.env` y se configuraron los valores de conexión para utilizar la base de datos `crud`. Después se ejecutó `php artisan config:clear` y se comprobó la conexión mediante `php artisan db:show`.

### 9.2. Longitud máxima de los índices en MySQL

**Dificultad:** durante las migraciones aparecía el error `1071`, relacionado con la longitud máxima permitida para los índices.

**Solución:** se configuró una longitud predeterminada de 191 caracteres para las cadenas mediante `Schema::defaultStringLength(191)` en `AppServiceProvider`. También se redujo la longitud de las columnas `connection` y `queue` a 100 caracteres en la migración `0001_01_01_000002_create_jobs_table.php` para resolver el problema del índice compuesto de `failed_jobs`.

### 9.3. Tabla existente durante las migraciones

**Dificultad:** después de una migración fallida, Laravel intentaba crear nuevamente una tabla que ya existía.

**Solución:** se revisó el estado de las migraciones y las tablas de la base de datos. En el entorno de práctica se reiniciaron las tablas cuando fue necesario y se volvieron a ejecutar las migraciones. Este procedimiento debe hacerse con precaución, porque eliminar tablas puede borrar los datos guardados.

### 9.4. Bloqueo de npm en PowerShell

**Dificultad:** al ejecutar `npm install`, PowerShell mostraba un error de seguridad porque la ejecución de scripts estaba deshabilitada.

**Solución:** se utilizó `npm.cmd install` y, para compilar los recursos del frontend, `npm.cmd run dev`, evitando tener que cambiar la política de ejecución de PowerShell.

### 9.5. Error de middleware en los controladores

**Dificultad:** durante las pruebas de autenticación se encontró un error relacionado con la llamada al método `middleware()` en los controladores generados por Laravel UI.

**Solución:** se adaptaron los controladores de autenticación y de inicio a la interfaz `HasMiddleware` y al método estático `middleware()` utilizado en Laravel 13. Los cambios permitieron continuar con las pruebas de las rutas de autenticación y de la página de inicio.

### 9.6. Vistas CRUD inexistentes o incompletas

**Dificultad:** algunas rutas, como la de mostrar o editar un producto, generaban errores porque las vistas correspondientes todavía no estaban creadas.

**Solución:** se crearon las vistas `show.blade.php` y `edit.blade.php` dentro de `resources/views/products/`. También se prepararon las vistas de creación y listado con una estructura basada en `layouts.app` y Bootstrap.

### 9.7. Apariencia y estilos del frontend

**Dificultad:** durante las primeras pruebas, algunos cambios visuales no se apreciaban como se esperaba.

**Solución:** se revisó que se estuviera visitando la ruta correcta, que las vistas extendieran `layouts.app` y que los recursos del frontend estuvieran instalados y compilados. Para volver a cargar los estilos y el contenido se puede utilizar `Ctrl + F5` en el navegador.

### 9.8. Numeración después de eliminar productos

**Dificultad:** utilizar directamente el identificador de la base de datos como número de fila puede dejar saltos en la numeración después de eliminar un registro.

**Solución:** la tabla utiliza el índice del recorrido de Blade (`$index + 1`) para mostrar números consecutivos. El identificador real de la base de datos se conserva para que las rutas y operaciones del CRUD sigan apuntando al producto correcto.

## 10. Conclusiones

El laboratorio permitió comprender la estructura de una aplicación desarrollada con Laravel y la importancia de organizar el código mediante el patrón Modelo-Vista-Controlador. Se trabajó con modelos, vistas, controladores y rutas para implementar las cuatro operaciones de un CRUD.

La configuración de MySQL y el uso de migraciones permitieron definir la estructura de la tabla `products`. A través de Eloquent se implementaron consultas, creación, actualización y eliminación de registros, mientras que las reglas de validación ayudaron a controlar los datos recibidos por los formularios.

La creación de vistas con Blade y Bootstrap permitió presentar los productos en una tabla y disponer de formularios para crear y editar registros, además de una página para consultar sus detalles. También se ajustó la numeración de la tabla para que fuera consecutiva sin alterar los identificadores reales de MySQL.

Finalmente, la solución de los errores de migraciones, configuración, compatibilidad y presentación reforzó la importancia de comprobar los mensajes de error y verificar cada parte de la aplicación durante el desarrollo.

## 11. Referencias

1. Laravel. (s. f.). *Documentación oficial de Laravel 13: Instalación y configuración*.  
   https://laravel.com/docs/13.x/installation

2. Laravel. (s. f.). *Documentación oficial de Laravel 13: Bases de datos y migraciones*.  
   https://laravel.com/docs/13.x/migrations

3. Laravel. (s. f.). *Documentación oficial de Laravel 13: Enrutamiento*.  
   https://laravel.com/docs/13.x/routing

4. Laravel. (s. f.). *Documentación oficial de Laravel 13: Eloquent ORM*.  
   https://laravel.com/docs/13.x/eloquent

5. Laravel. (s. f.). *Documentación oficial de Laravel 13: Validación*.  
   https://laravel.com/docs/13.x/validation

6. Laravel UI. (s. f.). *Repositorio y documentación oficial de Laravel UI*.  
   https://github.com/laravel/ui

7. Bootstrap. (s. f.). *Documentación oficial de Bootstrap*.  
   https://getbootstrap.com/docs/

8. Node.js. (s. f.). *Documentación oficial de npm*.  
   https://docs.npmjs.com/

## 12. Fecha de ejecución del laboratorio

**Fecha de ejecución:** octubre de 2026

## 13. Datos del estudiante

Este laboratorio ha sido desarrollado por el estudiante de la Universidad Tecnológica de Panamá.

- **Nombre:** Samuel Orocú
- **Correo:** samuel.orocu@utp.ac.pa
- **Curso:** Desarrollo Web
- **Facultad:** Facultad de Ingeniería de Sistemas Computacionales
- **Campus:** Víctor Levi Sasso
- **Instructor del laboratorio:** Ing. Irina Fong
- **Laboratorio:** Implementación de un CRUD de productos en Laravel

---

<p align="center">
  Universidad Tecnológica de Panamá  
  Facultad de Ingeniería de Sistemas Computacionales  
  Desarrollo Web — II Semestre 2026
</p>
