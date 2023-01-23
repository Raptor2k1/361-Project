# CS361-Project: String to Image Association
This program has two components - a local client service and a microservice that can respond to a request.  
Local users can input a string and the program will load an image from an image folder that best matches their  
string's content, based on an algorithm analysis (related to keywords stored within the program).

The user can further customize this by using a settings menu to enter additional keywords to be used as a factor in  
analyzing strings and what images best fit. Any images in the images/ folder relatively local to the script will be  
considered. A "default.png" file is expected as part of minimum functionality, so that some form of image is always  
returned. By appropriately naming images and adding them to the image folder and creating additional keywords, the
user can expand the potential image associations created by the application.  

The user can also execute the early stages of a microservice in this first version. There is a command available to  
manually check a request pipeline JSON file for request content. If content is found, it is returned via a response  
pipeline JSON file, which can be accessed by other applications. Current microservice implementation relies on the  
other application knowing where to submit a request and find a response, and they must wait for a local user to  
manually activate the request/response function.  

The current implementation of this is a console application navigated primarily by numerical option navigation and  
typing words or strings when prompted by the system.