# Modern & Secure PHP: Not Your Grandma's PHP
**by Ben Edmunds @benedmunds**

## Exceptions

PHP has exceptions: 'this thing happened, what do you want to do with it'

Specific exceptions, generic exceptions

	try {
    	// your code goes here
    }
    catch (Exception $e) {
    	die($e->getMEssage());
    }
    
## Closures

Anonymous functions you can pass around like variables

	// laravel style
	Route::get('/', function() {
    	return View::make('index');
    });
   
## Namespaces

PHP code can get sloppy very easy

Namespaces give you a nice clean way to group classes together

Composer is a package management tool.  You can pull in packages that are all self-contained.

	// laravel
    namespace Illuminate\Console;
    class Command
    {
    	// ...
    }
    
    // Use it later and for the rest of that script you'll
    // have access to that namespace
    use Illuminate\Console\Command

You can have another Command class in the same app but it's ok because it's in a different namespace

## Statics

Statics aren't new, but there's still a lot of confusion.  Basically a one time use class structure.

	Class Route {
    	public static function get() {}
    }
    
    Route::get();
    
    
One time use classes.  YOu don't instantiate it.  Quick and easy to use.

Double colon vs. arrow that tells PHP it's static.  There's ways to access variables and inheritance, but you
don't really want to do that with statics or it gets messy very quickly.

Trend is to use statics when you need to

No `$this`

Two kinds of access


## Short Array Syntax

Use square brackets.  Like JS arrays but with arrows not colons.  Just a normal array, but a different syntax.

## Traits

Way to group without the strict inheritance model you're used to in a normal class.

	trait baseUser {
    	function getName() {
    		return 'Jon Snow';
    	}
    }
    // adminuser can just use this without extending it or anything
    class adminUser {
    	use BaseUser;
    }
    
    $adminUser = new adminUser;
    echo $adminUser->getName()
    
You're going to see a lot more traits coming up where a lot more liraries and frameworks are using the because you can get a lot more flexibility.

## PDO

Cross System database access layer built into PHP.  Supports MSSQL, MySQL, Oracle, etc.).

Supports safe binding.

	$stmt = $db-.prepare('
		SELECT *FROM users
        WHERE id=:id
    ');
    
    $stmt->bindParam(':id', $id);
    $stmt->execute();
    
You don't have to remember to escape anything.  Nice clean way to write SQL and just bind your params.

## Escaping i/o
	
    // escaping input
    $stmt->bindParam(':id', $id);
    
	// escaping output
    // 90% of time htmlentities will do what you need
    htmlentities($_POST['name']);
    
## HTTPS/SSL

## Authentication

Not just logging in a user.  More about what to do with their credentials.  Anything you let something happen that requires permission you need to check persmission.

Make sure login methods include some sort of brute force login detection

PHP now includes functions for safe password hasing.  Now in PHP 5/6 it's built into the language.  Will use the best hashing algorithim at the time built into PHP.

	password_hash($_POST['pass']);

Also includes unique salt in there.

To verify passwords afterwords
	
    password_verify($_POST['pass'], $u->pass);
    
## Safe Defaults

One thing you want to make sure you do when writing classes is make sure the default value of the variable defined somewhere.

## Persistent and Non Persistent XSS

Non-persistent XSS doesn't stay with your site.  Example, pass in GET params in a URL.  If you can pass a user ID into a delete end point. Then send to someone who's an admin for the site.

Persistent is the same id but data is saved in the application

	htmlentities($name)
    
## Cross Site Request Forgery (CSRF)

Add CSRF tokens

	function generateCsrf() {
    	$token = mcrypt_create_iv(
        16, MCRYPT_DEV_URANDOM);
        Session::flash('csrfToken', $token);
        return $token;
    }
    
    if($_POST['token'] == Session::get('csrfToken')) {
    
    }
    
Check token later when form is submitted to see if it matches the users valid session.

Array of tokens with timestamps and check if it's valid in a certain time frame.

## Built in Web Server

	$ php -S localhost:8000
    
## Composer

Yet another package manager.  Better than PEAR.  Biggest problem with PEAR wasn't the technology but that the packages were out of date and it was hard to find what package you needed.  Has autoloading so all you have to do is require your composer autoload file and add you use for classes throughout it's going to automatically load them in.

packagist.org

You can have an internal version as well.

	{
    	"require" : {
        	"stripe/stripe-php": "dev-master",
            "twilio/sdk": "dev-master"
        }
    }
    
Always lock in production to certain versions.

	// Will create a lock file which you will commit to your git repo; lots of opinions on this.
	$ php composer.phar update
    $ php composer.phar install
    
	$client = new Services_Twilio($sid, $tkn);

## Unit Testing

* PHPUnit
* Behat
* Mink
* Selenium
* CodeCeption (BDD style)
* PHPSpec

        public function testVerify() {
    		$auth = new apiAuth();
        	$this->assertTrue($auth->verify());
    	}
    
		$ phpunit tests
    
## Resources

[PHP.net](http://php.net)

Modern Frameworks

* Laravel
* SlimPHP 2
* Symfony2
* Aura for PHP
* Fuel PHP 
* Silex

[PHPtheRightWay.com](http://www.phptherightway.com)

[BuildSecurePHPapps.com](BuildSecurePHPapps.com)
