#Steps to deploy Laravel app to Heroku with ease

After adding and commiting to git
Make sure you have heroku CLI installed

Create your Heroku app using the command below.
NB: It will give your app a wierd name.

``` heroku create ```

Create Procfile. This file is very important and have the abillity to impact your life negatively if you fail to onfigure it properly.

use the following command in your CLI. Then check the Procfile and remove the
quotation("") marks around the string.

``` echo "web: vendor/bin/heroku-php-apache2 public/" > Procfile ```

If you don't remove the quotes, Heroku may not append the public/ directive.

Clear your cache. This is because the is an anticipated issue where a Laravel 
package class will not be found.

``` php artisan cache:clear ```

After clearing your cache. Check composer.json and composer.lock and move the 
following package from require-dev to require

``` "fzaninotto/faker": "^1.9@dev" ```

After relocating the Faker, 

``` composer install ```

Then 

``` composer update ```

Now you can add the changes
``` git add ```

And commit them

``` git commit -m "updated composer files" ```

And then push to Heroku

``` git push heroku master ```
