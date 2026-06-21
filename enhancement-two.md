---
layout: default
title: Enhancement Two - Algorithms and Data Structures
permalink: /enhancement-two/
---

{% include navigation.html %}

# Enhancement Two: Algorithms and Data Structures

On this page, I will detail the second enhancement that was successfully completed from the original code review of the mobile version of the Inventory Tracker.

## Overview

The second enhancement was focused in making use of algorithms and datastructures to improve the original Inventory Tracker.

Key aspects I aim to address were: 

- I made the inventory data model more useful. Instead of only storing item name and quantity, the enhanced version includes fields such as category, minimum threshold, maximum threshold, created date, and modified date.
- I added search, sort, and filter functionality. This allows users to search by item name or category.
- The ability to alpha-numerically sort items by name, category, and quantity was added so that the table was not completely static.
- I added dashboard-style logic for a new view that summarizes the inventory data. For example: the application now shows total items, low-stock items, out-of-stock items, or items that have not been updated recently.
- These enhancements demonstrate stronger use of Python data structures such as lists, dictionaries, and custom objects.
- This shows more meaningful algorithmic thinking because the program will not just store and display records; it will present inventory data in a way that users such as a business managers can make actionable and informed decision at a quick glance. 

## Before and After Comparison

### Original Item Model

The original application only featured an inventory item model and did not have a model for a user class. 

```java
public class InventoryItem {

    // Variable declarations
    private final int id;
    private final String name;
    private final int quantity;

    // Constructor
    public InventoryItem(int id, String name, int quantity) {
        this.id = id;
        this.name = name;
        this.quantity = quantity;
    }
}
```
### New User Model

The new application features a user model class and an inventory model class. This allowed for greater complexity for functions created for updating records in the databases for both users and inventory items. 

```python
# User class defined, contain parameters username, password_hash, user_id
# and created_at
class User:
    def __init__(self, username: str, password_hash: str, user_id: Optional[int] = None, created_at: Optional[str] = None):
        self.username = username
        self.password_hash = password_hash
        self.user_id = user_id
        self.created_at = created_at
```
### New Inventory Model

```python
# InventoryItem class defined, contains parameters item_name, category,
# quantity, min_threshold, max_threshold, item_id, created_at, updated_at
class InventoryItem:
    def __init__(self, item_name: str, category: str, quantity: int,
                 min_threshold: int = 0, max_threshold: int = 100,
                 item_id: Optional[int] = None, created_at: Optional[str] = None,
                 updated_at: Optional[str] = None):
        self.item_name = item_name
        self.category = category
        self.quantity = quantity
        self.min_threshold = min_threshold
        self.max_threshold = max_threshold
        self.item_id = item_id
        self.created_at = created_at
        self.updated_at = updated_at
```
### No prior sorting/searching algorithms present in the original application
Due to the scope of the original application being entirely focused on building a functional application, there was no focus on complex alogrithms that could perform any sort of mutations or look ups on data. 

### Search/Scan methods introduced in the new application

The dashboard_view.py that was newly introduced in the python application is where the majority of algorithmic principles are explored for the application. 

This enhancement makes use of of the following methods: 

Linear Scan Methods:
All methods share the same patterns of fetching all items, then looping through the list once. 
- `get_total_item_count()`
- `get_total_quantity()`
- `get_low_stock_items()`
- `get_over_stock_items()`
- `get_category_breakdown()`

This is to say, if you have n items in inventory, the algorithm will do n units of work, for a time complexity of O(n), or linear time. 

Min Max Reduction:
The `max()` and `min()` built in python functions scan a full list once to find the corresponding extreme value. By nature, they must inspect every element for an unsorted list. 
- `get_highest_quantity_item()`
- `get_lowest_quantity_item()`
- `get_newest_item()`
- `get_oldest_item()`

This also features a time complexity of O(n)

### Solution to category breakdown

The category breakdown feature needed a unique fix to return the needed data to present in the dashboard. 

In order to present the quantities of all items in all given categories, a dictionary was built in a single O(n) pass, using the dictionary as a running tally for each time a category is read. A less efficient manner may have included looping through the list for each unique category, bringing the complexity up to O(n * k) where k is each unique category. 

```python
# builds and returns a dictionary mapping each category name to the count of items
# in that category
def get_category_breakdown(self) -> dict:
    all_items = self.inventory_repository.get_all_items()
    category_breakdown = {}

    for item in all_items:
        if item.category in category_breakdown:
            category_breakdown[item.category] += 1
        else:
            category_breakdown[item.category] = 1

    return category_breakdown
```
### Table sorting
Sorting algorithms for the tables were much more difficult to implement but were also not previously implemented in the original application. 

Pythons built in `.sort()` was leveraged over a manual sort such as bubble sort or insertion sort. Pythons built in sort function makes use of an algorithm called Timsort, with a complexity of O(n log n). As a comparison based sort, it can do no better than O(n log n) generally, however in the event that something is already sorted or partially sorted, the method benefits and can better complexity in certain scenarios.

There are 3 main components for the sort:
- Build rows list - O(n)
- Sort - O(n log n)
- Reorder Table - O(n)

The dominant term in this case trumps the others, resulting in an overall complexity for the algorithm as O(n log n)

```python
def _sort_table(self, table, column, numeric=False):
    # rows list declared used for collect all rows
    rows = []

    # iterate through all every row's iid, for each one, read current
    # values of those cells, return both value and iid makes sort possible via
    # iid value
    for iid in table.get_children():
        cell_value = table.set(iid, column)
        rows.append((cell_value, iid))

    # build unique key value in dictionary _sort_state{}
    # each key will be unique with id(table) + column
    key = f"id{id(table)}{column}"
    ascending = self._sort_state.get(key, True)

    # attempt numeric sort, if not numeric, then try alpha sort
    # note about sorting: reverse not ascending means:
    # if ascending is True, reverse is False (normal order)
    # if ascending is False, reverse is True (reversed order)
    if numeric:
        # convert the cell value to int before comparing
        def get_number(value_of_cell):
            if value_of_cell[0]:
                return int(value_of_cell[0])
            else:
                return 0

        rows.sort(key=get_number, reverse=not ascending)

    # use .lower() to make sorting case-insensitive
    else:
        def get_text(value_of_cell):
            return value_of_cell[0].lower()

        rows.sort(key=get_text, reverse=not ascending)

    # in order to accomplish re-ordering without deleting and
    # inserting values again, .move() utilized to move existing
    # row to new position
    index = 0
    for (_, iid) in rows:
        table.move(iid, "", index)
        index += 1

    # if ascending was True on click, store False so the next click
    # toggles the other way
    self._sort_state[key] = not ascending
```

## Reflection

### What was the original artifact? 

The original artifact is an Android mobile application, written in Java that was original created by closely following for materials for course CS 360. The foundation provided by this course allowed me to successfully recreate the entire application in Python for my proposed enhancement plan of the application.

### Why did I select this artifact to improve and what skills did it show case? 

The dedicated service files are where the main meat and focus on algorithms and date structures lie, mostly in the inventory_service and the dashboard_service file. The serach_items() function in the inventory_service files demonstrates an algorithm that performs a linear search across a list of objects, evaluating each item against a query string across two fields, item_name and category. It also simultaneously handles edge cases such as an empty string being entered returning the full unfiltered list and exiting immediately. While simple in nature, it is an integral part of what makes the table in the inventory_view file possible when it comes to sorting through larger sets of data. 

Another few examples from the dashboard_service file are the get_highest_quantity_item() and get_lowest_quantity_item() functions that use many of pythons functions such as max()/min() and lambda in order to return whichever items has the most or least units on hand in the inventory table. Another algorithmic example is the get_category_breakdown() function which builds a frequency dictionary from a list. Converting one data structure to another is a valuable skill to have and was necessary to summarize all categories in the inventory table. 

### Final Reflection

I have met the above outcome specifically with all through different functionalities in the dashboard_service as these enhancements were crucial to being able present summarizations of the data present in the inventory database. Without it, all the inventory tracking app was essentially a glorified list maker. Now with the dashboard, common insights needed in reporting and operations for companies that need an inventory tracking app are made possible thanks to sorting, summation and data structure conversion algorithms introduced in this enhanced version of the application. 

I learned a great deal in common sorting practices when working with tables in python. Ensuring I was making targeted specific functions that pulled very specific data was paramount to ensuring the dashboard would be successful. I leveraged my own knowledge from excel and thought about common patterns I would leverage when presenting data to peers when considering what sort of data should be presented in the dashboard. Making these functions work was a reward and the application is became something I am quite proud of that I may leverage in my own day to day life. Maybe I will not use specifically for tracking inventory, but perhaps I can rebrand it track anything that is quantifiable. 

[← Back to Home](/)
