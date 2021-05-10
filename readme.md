# Steps to deploy Laravel app to Heroku with ease

_decided to document this after spending hours between Stackoverflow, Heroku docs and other options.
  Hope it helps you save time and avoid brain drain_

After adding and commiting to git
Make sure you have heroku CLI installed

Create your Heroku app using the command below.
NB: It will give your app a wierd name.

``` heroku create ```

Create Procfile. This file is very important and has the abillity to impact your life negatively if you fail to configure it properly.

use the following command in your CLI. Then check the Procfile and remove the
quotation("") marks around the string.

``` echo "web: vendor/bin/heroku-php-apache2 public/" > Procfile ```

If you don't remove the quotes, Heroku may not append the public/ directive.

Clear your cache. This is because there is an anticipated issue where a Laravel 
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

Go to *Resources* and create a database addon. I use ClearDB and I think you should too.

After that, If you visit the app at this point you will get an error 500. If you see that then you are on track.
Go to *Settings* and hit the *Reveal Config Vars* button

You can add your .env settings from here. *Where you see key and value input fields* or you can use the command line.
When you are done,

enter the code below in your cmd to get your database config keys.

```heroku config```  

You will see the config values you entered and then you will see another value CLEARDB_DATABASE_URL. The CLEARDB_DATABASE_URL
has the values you need for your database connection.

 ```heroku config:set DATABASE_URL='mysql://DB_USERNAME:DB_PASSWORD@DB_HOST/DB_DATABASE?reconnect=true'```
 
 As represented in the string above. The value in the position of DB_USERNAME is your database username and its the same for
 the other values too. I generally use the cmd to add this part cause first time I used the GUI the vars got rejected. So...
 
 ```heroku config:add DB_USERNAME=jghk54fsff56``` whatever your username is. DO same for the others
 
 You can now go back to the config variables button and you will see your variables.
 
 Lastly, you can run the migrations
 
 ```heroku run php artisan migrate```.
 
 Once again, I hope this helps you.
 
 #NB
 You can rename your project using the following code in command line

```heroku apps:rename newname --app oldname```
 
 If you cloned your project from a github repo, you need to run these codes for Heroku to initialize your project as a Heroku app

```git remote rm heroku```

```heroku git:remote -a newname```

## Running Laravel Commands on Heroku
You can run Laravel commands on Heroku using the ```heroku run``` as shown below:
```heroku run php artisan migrate```


 
 ## Want To Thank Me?
 A Github star will be perfect. Cheers!

Please feel free to contribute




