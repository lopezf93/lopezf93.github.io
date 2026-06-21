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

## Reflection

### What was the original artifact? 

The original artifact is an Android mobile application, written in Java that was original created by closely following for materials for course CS 360. The foundation provided by this course allowed me to successfully recreate the entire application in Python for my proposed enhancement plan of the application.

### Why did I select this artifact to improve and what skills did it show case? 

pending narritive justification

### Final Reflection

pending narrative reflection

[← Back to Home](/)
