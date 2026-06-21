---
layout: default
title: Enhancement Three - Databases
permalink: /enhancement-three/
---

{% include navigation.html %}

# Enhancement Three: Databases

On this page, I will detail the third enhancement that was successfully completed from the original code review of the mobile version of the Inventory Tracker.

## Overview

The third enhancement was focused in making imporvements in the use of databases in the original mobile application. SQLite was used for local storage and proof of concept like the original mobile application, but now features robust data validation and security improvements. 

Key aspects I aim to address were: 
- For the User Table: 
  - Store hashed passwords instead of plaintext
    - Use Bcrypt library to support password hashing
  - Add username uniqueness and validation
  - Validate log in credentials securely
- For the Inventory Table: 
  - Add a new category field
  - Add a new timestamp field (created/modified)
  - Add quantity threshold values (minimums and maximums)
  - Add transaction/update logging
- Create New Activity Log Table
  - New table featured in database responsible for logging different events
  - Create events for ADD, EDIT, DELETE etc...
  - Ensure the records logged are accurate and capture the correct timestamp and item information
- Lastly, for Security Enhancements:
  - Ensure parameterized SQL queries are resilient against SQL injection attacks
  - Input validation for any input fields
  - Separate database logic from GUI logic


## Before and After Comparison

pending images to use for comparison

## Reflection

### What was the original artifact? 

The original artifact is an Android mobile application, written in Java that was original created by closely following for materials for course CS 360. The foundation provided by this course allowed me to successfully recreate the entire application in Python for my proposed enhancement plan of the application.

### Why did I select this artifact to improve and what skills did it show case? 

pending narritive justification

### Final Reflection

I have successfully completed all features I set out to finish at the beginning of the course. I reimagined the overall structure of the application with a clear separation of concerns for all original activities from the java mobile application. Previously tightly coupled logic for both UI and functionality is now contained in dedicated classes that work together seamlessly. This is especially true for the database of the application and how it works with SQLite. The application is now incredibly well fortified against potential malicious actions normally exploited through input fields and interactable objects. 

I learned a great more about SQLite best practices and parameterized queries. I also learned how to ensure all database related functionality was clearly localized in dedicated classes and functions that handled very specific functions. For example, the db_manager.py file is solely responsible for ensuring the database exists or is created upon launch of the application, whereas the dedicated repository files communicate with the database’s individual tables. All functionalities defined in the repository files are then called upon by the dedicated service files with contain all input validation logic and edge cases before any data is passed. Finally, the view files for the UI where actual entry boxes and interactable objects are define make use of the service functionalities when passing user inputs or actions. 

This decoupling ensures the application has many fallbacks when processing data or inputs and can fail gracefully rather than crashing altogether when running. In the original java application, a single typo in any file would cause a catastrophic failure in the application and it would cease to run. The newly enhanced application is much more resilient to these short coming when working with the database in any view, input field, or interactable table in the application. 



[← Back to Home](/)
