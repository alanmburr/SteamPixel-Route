# Simple PHP Router

Hey! This is a simple and small PHP router that can handle the whole URL routing for your project.
It utilizes RegExp and PHP's anonymous functions to create a lightweight and fast routing system.
The router supports dynamic path parameters, special 404 and 405 routes as well as verification of request methods like GET, POST, PUT, DELETE, etc.
The codebase is very small and very easy to understand. So you can use it as a boilerplate for a more complex router.

Take a look at the index.php file. As you can see the `Route::add()` method is used to add new routes to your project.
The first argument takes the path segment. You can also use RegExp in there to parse out variables.
All matching variables will be pushed to the handler method defined in the second argument.
The third argument will match the request method. The default method is 'get'.

## Simple example:
```php
use Steampixel\Route;
include 'src\Steampixel\Route.php';

Route::add('/user/([0-9]*)/edit', function($id) {
  echo 'Edit user with id '.$id.'<br>';
}, 'get');

Route::run('/');
```

You will find a more complex example with a build in navigation in the index.php file.

## Use a different basepath
If your script lives in a subfolder (e.g. /api/v1) set this basepath in your run method:

```php
Route::run('/api/v1');
```

Do not forget to edit the basepath in .htaccess too if you are on Apache2. In order to run the test files correctly inside a basepath you should also adjust the navigation links inside the index.php.

## Enable case sensitive routes, trailing slashes and multi match mode
The second, third and fourth parameters of `Route::run('/', false, false, false);` are set to false by default.
Using this parameters you can switch on and off several options:
* Second parameter: You can enable case sensitive mode by setting the second parameter to true.
* Third parameter: By default the router will ignore trailing slashes. Set this parameter to true to avoid this.
* Fourth parameter: By default the router will only execute the first matching route. Set this parameter to true to enable multi match mode.

## Something does not work?
* Don't forget to set the correct basepath as the first argument in your `run()` method and in your .htaccess file.
* Enable mod_rewrite in your Apache2 settings, in case you're using Apache2: `a2enmod apache2`

## Test setup with Docker
I have created a little Docker test setup.

1. Build the image: `docker build -t simplephprouter docker/image-php-7.2`

2. Spin up a container
	* On Linux / Mac or Windows Powershell use: `docker run -d -p 80:80 -v $(pwd):/var/www/html --name simplephprouter simplephprouter`
	* On Windows CMD use `docker run -d -p 80:80 -v %cd%:/var/www/html --name simplephprouter simplephprouter`

3. Open your browser and navigate to http://localhost

## Test setup with Vagrant (no longer maintained)
There is a little Vagrant test setup. Just run `vagrant up` to spin up an Apache2 web server on Ubuntu. Then navigate to http://router.local after adding the machine IP to your hosts file. This test setup is no longer maintained and will probably break in the future. Use the Docker test setup instead.

## Themes, layouts, pages and components
If you are interested in some basic concepts on how to build a simple PHP page using this router including themes, layouts, pages and components checkout this repo: https://github.com/steampixel/simplePHPPages
This project will give you some ideas and basics on how to get started without any dependencies.

## Todo
* Create demo configuration for nginx
* Create Composer configuration and upload to packagist.org

## License
This project is licensed under the MIT License. See LICENSE for further information.
