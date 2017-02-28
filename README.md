# PHP-MySQL-Sessions
This is a native solution to easily store PHP session data in a MySQL database.<br />
## Overview ##
Session variables contain data that is saved for a specific user by associating the user with a unique identity. Typically, PHP would store session variables in a local file system on the server by default. While this may be acceptable to many people who are running small to moderate PHP applications, some larger applications that require load balancing would need to be run on multiple server with a load balancer. In such cases, each server running PHP would need a way to ensure that sessions continue to work properly. One common way to achieve this is to override where PHP opens, reads, writes, and destroys the session variables so that it can perform these operations on a table inside of a MySQL database. When this is performed, the web application can gain advantages such as session management, session logging, and session interactions.
## Installation ##
This solution can be easily integrated with your existing PHP code that uses PHP sessions. Simply perform the following steps:

1. Upload the files in this repository to your Apache server running PHP. You can store these files inside any resource folder of your desire. It is not recommended that these files be located in the root directory since it contains some sensitive database information.

2. Edit the file `database.class.php` and change the following variables to your existing database. 
```php
define("DB_HOST", "localhost");
define("DB_USER", "yourusername");
define("DB_PASS", "1234567890");
define("DB_NAME", "yourdbname");
```