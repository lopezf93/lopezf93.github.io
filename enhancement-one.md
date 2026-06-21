---
layout: default
title: Enhancement One: Software Design and Engineering
permalink: /enhancement-one/
---

{% include navigation.html %}

# Enhancement One: 
# Software Design and Engineering

On this page, I will detail the first enhancement that was successfully completed from the original code review of the mobile version of the Inventory Tracker.

## Overview

The first enhancement was focused on the over all design and structute of the original application. 

Key aspects I aim to address were: 

- [x] Recreate the application in Python from Java
- [x] Clear separation of concerns between logic layers: GUI layers, database logic etc...
- [x] Improve interface design, ensure final application is cohesive in theme and styling
- [x] Make use of resources such as a TKinter, Figma to accomplish visual components
- [x] Make use of traditional software engineering tools like UML diagrams and flow charts during planning stages

## Before and After Comparison
### Original Application GUI
![Mobile Application Screens 1](assets/images/Mobile_Inventory_Tracker_Screens_1.png)

![Mobile Application Screens 2](assets/images/Mobile_Inventory_Tracker_Screens_2.png)

### New Python Application GUI

![Python Application Screens 1](assets/images/Final_Login_View.png)

![Python Application Screens 2](assets/images/Final_Create_Account_View.png)

![Python Application Screens 3](assets/images/Final_Inventory_View.png)

![Python Application Screens 4](assets/images/Final_Item_Form_Add_View.png)

![Python Application Screens 5](assets/images/Final_Item_Form_Edit_View.png)

![Python Application Screens 6](assets/images/Final_DashBoard_View.png)

## Reflection

### What was the original artifact? 

The original artifact is an Android mobile application, written in Java that was original created by closely following for materials for course CS 360. The foundation provided by this course allowed me to successfully recreate all back-end logic of the application in Python for my proposed enhancement plan for the application.

### Why did I select this artifact to improve and what skills did it show case? 

My new program has been completely rebuilt in python, leveraging the java application as the blueprint in foundation to successfully recreating functionality as well as implementing other improvements to flesh out the application into something much more verbose than the original project.

I successfully translated my original application from Java to Python using best practices for “Pythonic” writing. I leveraged many sources to accomplish this, from stack overflow to geeksforgeeks to refamiliarize myself with python as best I could. I also used other resources to refamiliarize myself with SQLite which was pivotal to ensure I could make a data driven application that relied on a locally stored database created by the user. 

Compared to the original application that had tightly coupled logic for all activity screens, the final python application features a much clearer separation of concerns for all logic layers. For example, all GUI logic now lives in dedicated view files, and logic that supports these visual components now lives exclusively in the service layer files. The old application had some of the database logic within some of the activity files as well, which should have been exclusively responsible for the logic of elements drawn on the screen such as button presses. Now the database logic has been centralized in a dedicated database layer, which is leverage by the service layer. Finally, the last two layers created, the security layer and model layer ensure no one file is carrying too heavy a burden for any feature of the application. 

Focusing on the design of the project, by leveraging tools such as Figma for visual design and the standard Python interface Tkinter to utilize the Tcl/Tk GUI toolkit, I constructed an application that is aesthetically pleasing and intuitive to use on a desktop. This allowed me to completely rebuild the entire original java mobile application in Python with a GUI that will work across both MacOS and Windows OS. Although the Tkinter library is considered dated, I needed to ensure I fleshed out my ability to work with a more foundational library before moving on to one that is much more sophisticated to add things like animations and transitions between screens. The scope of my enhancement did not animations but will be an improvement I will consider in future improvements to the application.  

### Final Reflection

I learned a great deal in desktop application development and feel as though this foundation I have built for myself is the first step in making more applications for MacOS or WindowsOS or perhaps even in pivoting to focusing more on web application development as well. More than anything I love to create things, in any shape or form, and being able to see an application like this come to life as I built each component is incredibly rewarding and satisfying. Even if it does become increasingly difficult to land a formal 9-5 job in this field, I feel as though I can always have a place in this world as a freelancer building things I love to solve problems at a smaller scale for individuals over larger user bases.

[← Back to Home](/)
