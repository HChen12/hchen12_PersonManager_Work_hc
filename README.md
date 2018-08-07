for my work
---------------------------------------------------------------------------------
Us_E    --the source code of the program
us_Txt  --the txt version of the program source code

---------------------------------------------------------------------------------



One 、detailed rules
 Language：     PHP 5.6.9
DateBase：   mysql 5.5
DesignMode： mvc
BackgroundAddresse： (DomainName)/admin
BackgroundPwd： 123456
Address of attached to the database: 
/data/class.databse.php   
/admin/data/class.databse.php 

 


Two、Directory Structure

├─admin		 				// BackgroundAddresse
│  ├─app							// Background application directory
│  │  ├─Applys						// Application Record
│  │  ├─Companyedit					// Company Details/Edit | Add
│  │  ├─Companys					// Company List
│  │  ├─Index						// Home page architecture
│  │  ├─Locationedit					//Address Details/Edit | Add
│  │  ├─Locations						// Address List
│  │  ├─login							// Login
│  │  ├─Useredit						// User Details/Edit | Add
│  │  └─Users						// User List
│  ├─data							// Encapsulation Methods、Class
│  └─public						// StaticResource
│	└─index.php					// Background entry page
├─app							// Foreground application directory	
│  ├─About						// About
│  ├─Companys					// Company List
│  ├─Detail						// Company Detail
│  ├─Index						// Home
│  ├─Login						// Login
│  └─Reg							// Reg
├─data							// Encapsulation Methods、Class
├─public						// StaticResource
│  ├─css							// Styles
│  ├─font							// Fonts
│  ├─images						// img
│  ├─js							// js
│  └─module						// Common Mode
├─uploads					// Uploads File
└─index.php 				// Home Page 


App: Each page in the directory contains three files
1.	controller.php （Control） The control unit of the page，Get the data through the model and pass it to the view.
2.	Model.php （DateBase）Gets the data in the database.
3.	View.php  （View） Render the data passed by the controller to the foreground page.


THREE、MVCimplementation mechanism
This project implements the most basic MVC
The core code is in this file: /app/router.php 

The first step is to specify the format of the URL, as agreed below in this projecthttp://www.server.com/?(Page Address)&param1=test1&param2=test2

http://www.server.com/       The first part, the current project binding domain name
?(Page Address)		       The second part is the address of the page to visit
&param1=test1&param2=test2  Part three, page parameters

1.Parse the URL to get the page address
 
There is still a problem with this. Most websites will only enter a domain name http://www.server.com/，

So we're going to make a default address
 
2.Get the page parameters, explode() method to divide the third part into key-value pairs, stored as an associative array
 
3.	The Controller of the page is introduced and the init() method of the Controller is called. Here we have a constraint on the class name of the Controller and the Model, the page name Controller (the class name of the Controller) and the page name Model (the class name of the data Model), so that we can get the following information through the page name ($page)
	/app/$page           Page path
	$page_Controller      The class name of the controller
	$page_Model         The class name of the data model
 
There is actually an error running the above code. We did not introduce the controller file and the data model file. With PHP's built-in autoloa function, we can write an autoloa to load the required file automatically.
 

4.	  Next, we need to look at the way the page controller is written. The controller of each page is much the same, which can be divided into three steps
	1.Get objects for the model and view
	2.Get data
	3.Pass the data to the view

 
This is not a view.php  inside each View_Model , but /app/views.php

5.The function of the View_Model  is to load the file of the foreground page and pass the data to the foreground page，It has a assign method that stores the data, all of which is stored in $data
 
6.It's also simple to call the foreground page   <?=$data[‘page’]?> 
  This gets the name of the page


7.In the foreground page we used the native PHP template syntax, Reference:
https://blog.csdn.net/wozaixiaoximen/article/details/49301033
 
