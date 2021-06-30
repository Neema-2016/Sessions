---
layout: engineering-education
status: publish
published: true
url: /getting-started-with-php-sessions/
title: Getting started with PHP Sessions
description: This article will bring the readerr to a better understanding of what PHP Sessions are, why they are used and how they can be implemented.
author: neema-muganga
date: 2021-03-21T00:00:00-13:00
topics: [Languages]
excerpt_separator: <!--more-->
images:
  - url: /engineering-education/working-with-lambda-expressions-and-anonymous-functions/hero.png
    alt: Lambda expressions and Anonymous functions image
---
This article will bring the readerr to a better understanding of what PHP Sessions are, why they are used and how they can be implemented.

### Introduction
PHP Sessions provide server side storage of user information by use of session variables and makes this information accessed from several pages throughout a website.
Sessions uniquely identify users via a Session Identifier which provides connection of that particular user to their stored data on the server. 
<!--more-->
Sessions are compared to but are not the same as cookies, since cookies instead store users' information on the user's local computer.

### Prerequisites
One needs to have the following before getting proceeding with the article.
1. A basic understanding of the PHP programming language.
2. A text editor of your choice installed. I will be using Visual Studio code which you can get from [here](https://code.visualstudio.com/download)(if you already don't have it).
2. Either [xampp](https://www.apachefriends.org/download.html) or [wampp](https://sourceforge.net/projects/wampserver/) local server installed, for php to run.

### Table of contents
1. What is a PHP Session.
2. How to start a Session in PHP.
3. Accessing a created session.
4. Updating a PHP Session.
5. How to destroy a Session.

### What is a PHP Session?
A PHP Session is in simple terms a data storage for user's data that can be rendered across several pages of an application or website. A unique Session identifier or ID is used to identify the particular user the information references to.
Therefore, where a session ID is missing, it implies no session has been created yet. Hence, PHP is prompted to initiate one. 
We will learn how to start sessions and create session variables shortly.

We make use of Session variables that is written as $_SESSION(which is a global variable. Go [here](https://www.w3schools.com/php/php_superglobals.asp) to find out more about global variables.) to store one particular user's information.

### How to start a Session in PHP
Remember a user's information needs to be stored in session variables before they can be accessed across multiple pages? So, before you even use this variable, you will be required to start a session by invoking a PHP function called session_start().
This function creates a new session, or restarts an existing one then generates for the user a unique session ID, through a GET or POST request. 

> NOTE: It is always important to place the session_start() function immediately after the <?php tag at the beginning of your script that comes before the HTML tags else its functionality will not be implemented.

Create a details.php file and write the following code.
**See below how starting a session is implemented**

```php
<?php 
  //Starting session
  session_start();
?>

<!DOCTYPE html>
<html>
  <body>
    <?php 
      //Using session variables to set a session
      $_SESSION["name"] = "Neema Muganga";
      $_SESSION["hobby"] = "writing";
      
      echo "Successfully set the session variables.";
    ?>
  </body>
</html>
```

### Accessing a set session variable
Now that we have already set our sessions in the preceding section, we may want to access them just to be sure the sessions were set successfully.
Create a accessdetails.php file that will access the previosly set session variables.
We introduce a conditional statement (you may want to follow [this](https://www.w3schools.com/php/php_if_else.asp) link, which talks more on php conditional statements) and an isset() function to check if the session variables were really set.

**Accessing set Session variables**
```php

<?php 

  //Note that we call the session_start() function here also before proceeding 
  session_start();
?>
<!DOCTYPE html>
<html>
  <body>

    <?php
      
      //conditional statement with isset() function to check if session is set
      if(isset(($_SESSION["name"]) and ($_SESSION["hobby"]))){
	echo "Hi, '.$_SESSION["name"].', glad to know you enjoy '.$_SESSION["hobby"]. ' too!"; 
      }

      //if session variables do not exist, this will run instead
      else{
	echo "Sorry.. no such session variables set!";
      }
    ?>
  </body>
</html>
```

Since our sessions were set in the details.php file already, we expect it to run and give the following output.

Output:

```bash
Output:

Hi Neema Muganga, glad to know you enjoy writing too!

```
Incase you mispelt the variable sessions in the files, PHP may not recognize the session variables you are referring to and therefore return the else statement.

Output:

```bash

Sorry.. no such session variables set!
```

> NOTE: Ensure you place a semicolon at the end of a php statement to avoid syntactical errors that prevent your code from running.

### Updating a PHP Session.
Incase you want to change a session variable to a different value instead of the existing one, follow the following example below.
Replace the new session data in this case;the name, in the details.php file.

```php
<?php
//starting session
session_start();

//updating the session variable name value
$_SESSION["name"] = "Liz Muganga";
?>

<!DOCTYPE html>
<html>
  <body>
    <?php
    echo "You changed your name to '.$_SESSION["name"].'!";
    ?>
  </body>
</html>

```

This will change the name set from Neema Muganga to Liz Muganga and the following output will be seen when you run the code.

Output:

```bash
You change your name to Liz Muganga!

```

By now, you definitely have a good understanding of PHP Sessions. If not, please go through it a second time and you will see everything making better sense.
Remember you learn best by doing!

### How to destroy a PHP Session
The whole point of using sessions was to store user's data and make it accessible throughout several pages of the application. 
In other words, the server is able to know who is accessing the application at that particular point in time, by referencing the unique session identifier used,
when creating the session variable.
We definitely need to close the browser or even log out of the system at some point. This will lead to destroying a session variable.

**There are two functions we may use when destroying a session.**
1. The unset() function. This function destroy a particular session variable by passing in the session variable we want to destroy. We will soon see how.

2. The session_destroy() function. This function destroys all previously set session variables and it does not require passing any parameters to it.

The following code shows how how to destroy a php session.
```php

<?php
  //starts the session
  session_start();
?>

<!DOCTYPE html>
<html>
  <body>
    <?php
      
      //gets rid of the name session variable
      unset($_SESSION["name"]) ;

      //Eventually destroy all sessions set
      session_destroy(); 
    ?>
</body>
</html>
```

That was fun! Now I hope you understand how the logout and functionality is implemented in applications. 
The specific user data is wiped off the session variable if the unset function is used, and ultimately every other user data that was stored is destroyed 
from the session variable when the session_destroy() function is called. 


### Conclusion
Sessions to a beginner may sound hard of a concept to grasp, it is only normal to feel that way. This article therefore, is meant to simplify this concept and take you through a step by step learning process until you eventually get a hung of it.

Below you can find links to other sources you may want to look at to make your understanding even better.

#### Further reading
- [w3schools PHP Sessions](https://www.w3schools.com/php/php_sessions.asp).
- [Tutorial Republic](https://www.tutorialrepublic.com/php-tutorial/php-sessions.php).
- [Basic usage of PHP sessions from PHP Manual](https://www.php.net/manual/en/session.examples.basic.php).

Happy coding!

