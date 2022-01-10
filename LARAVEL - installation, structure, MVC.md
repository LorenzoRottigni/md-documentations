# LARAVEL - installation, structure, MVC

* Install Composer Packet Manager
* Create new Laravel project: 

	`composer create-project --prefer-dist laravel/laravel^7.0 < project-name >`
	
## Project structure

###	1.	/app => contains models in root and controllers under /controllers

 
###	2. /config => configuration file, array and objects static data:
		/config/numbers.php
		
		```
		<?php
		
		return [
			"one",
			"two",
			"three",
			...
		]
		
		?>
		```
		
		Retrieve data:
		
		```
		<?php
			$data = config('numbers')
		?>
		```
### 	3.	/database => DB files, DB migrations, DB seeds

### 	3.	/public => .htaccess, index.php public page, favicon ...
### 	4.	/resources => JS, CSS-SASS, views/BLADE TEMPLATES 
### 	5.	/routes => web.php laravel router, api.php for API calls
### 	6. .env => DB connection and PHP enviroment variables
### 	7. composer.json, package.json => packet manager dependencies

## CONCEPTS

### MVC - Model View Controller

1. Model => retrievement and manipulation of data
2. View => represent any output
3. Controller => is the bidirectional middleware between Model and View: the brain.