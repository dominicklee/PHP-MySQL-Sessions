# PHP-MySQL-Sessions
This is a native solution to easily store PHP session data in a MySQL database.<br />
## Overview ##
Session variables contain data that is saved for a specific user by associating the user with a unique identity. Typically, PHP would store session variables in a local file system on the server by default. While this may be acceptable to many people who are running small to moderate PHP applications, some larger applications that require load balancing would need to be run on multiple server with a load balancer. In such cases, each server running PHP would need a way to ensure that sessions continue to work properly. One common way to achieve this is to override where PHP opens, reads, writes, and destroys the session variables so that it can perform these operations on a table inside of a MySQL database. When this is performed, the web application can gain advantages such as session management, session logging, and session interactions.
## Installation ##
This solution can be easily integrated with your existing PHP code that uses PHP sessions. Simply perform the following steps:

1. Upload the files in this repository to your Apache server running PHP. You can store these files inside any resource folder of your desire. It is not recommended that these files be located in the root directory since it contains some sensitive database information.

2. Create a new MySQL database if you do not already have an existing one. Note down your MySQL credentials. Go to PHPMyAdmin or your database manager and run the following command:

	```mysql
	CREATE TABLE sessions
	(
		id varchar(32) NOT NULL,
		access int(10) unsigned,
		data text,
		PRIMARY KEY (id)
	);
	```

3. Edit the file `database.class.php` and change the following variables to your existing database. 
	```php
	define("DB_HOST", "localhost");
	define("DB_USER", "yourusername");
	define("DB_PASS", "1234567890");
	define("DB_NAME", "yourdbname");
	```

4. Make sure PHP has sufficient privileges and make sure that your MySQL server accepts connections if separate from your localhost.

## Usage ##
An example script called `example.php` has been provided for your convenience. This contains all the basic functionality you would need for storing, retrieving, and destroying a session. One thing to note is that you do not have to call `session_start()` on your code as that is already taken care of inside the `mysql.sessions.php` class.

- **Declarations** (include these on the top of your PHP):
	```php
	include("database.class.php");	//Include MySQL database class
	include("mysql.sessions.php");	//Include PHP MySQL sessions
	$session = new Session();	//Start a new PHP MySQL session
	```
- **Storing in a session variable**:
	```php
	//Store variable as usual
	$_SESSION['user'] = "johnsmith@example.com";
	```
- **Retrieving session variable**:
	```php
	//Show stored user
	echo $_SESSION['user'];
	```
- **Unset and Destroy** (use these for signing out a user):
	```php
	//Clear session data (only data column)
	session_unset();
	//Destroy the entire session
	session_destroy();
	```
## Troubleshooting ##
If for some reason your code does not work, you can add the following lines to the top of your PHP script to show the errors:
	```php
	error_reporting(E_ALL);
	ini_set('display_errors', '1');
	```

In addition, use PHPMyAdmin or your database manager to check your `sessions` table to see if the table has been altered in any way. For example, the table should populate as more session variables are being added.