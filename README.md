﻿# CS361-Project: String to Image Association
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

# CS361-Project: Microservice Instructions and Communication Contract
The microservice portion of this project is designed to be a flexible way for other programs to quickly associate one of the images available to the program with a string. The intention is that this can be used to quickly and dynamically generate content where you may have a large library of images available, and you do not want to manually assign an image in an accompanying space every time.  

To achieve this, the service uses socekts via ZeroMQ (https://zeromq.org/get-started/). JSON-formatted infromation is sent form a requesting client to the microservice, which acts as a server, listening in the socket's port for a request. Once the request is recieved, it runs a process to associate the strings in the request to one of the image filepaths in the request and it sends back the association to the requesting client.  

The JSON object sent by the requesting client should be the JSON-encoded form of a dictionary with two specific keys, "strings" and "images". These two keys are expected to have arrays as values, with the former being an array of strings to associate with an image, and the latter being an array of images that the requesting client has available within the client program's files. An example of a valid JSON request would be: {"strings": ["Pizza eating!", "Eat your veggies!"], "images": ["pizza.png", "carrot-veggies.png"]}  

Once the microservice has assigned images into a string:image dictionary, it will encode the dictionary to a JSON object and send it back to the requesting client. This JSON object will need to be decoded back into its non-byte form using the JSON decoding methods available to whatever respective programming language is used by the client. An example of what to expect from a decoded JSON (continuing the above example) would be: {"Pizza eating!": "pizza.png", "Eat your veggies!": "carrot-veggies.png"}  

Once the client-side program stores the results dictionary, this allows the client to directly index into matching image files using a string as a key. For example, this might allow a client to auto-generate an image to match an accompanying line of text, based on appropriate images that are already available in the client's file database.
