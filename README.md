This repository contains **Python transformation scripts** for **Hevo Data**, helping users modify incoming data before ingestion into the destination.  

1. Introduction
When working with Hevo Data, you might have multiple source tables that need to be merged into a single table for better analysis and reporting.
What Does This Transformation Do?
It takes incoming data from multiple tables in Hevo.


It renames them so that they all load into one common destination table.


This helps simplify data organization and makes querying easier.


When to Use This?
✅ You have multiple source tables (e.g., orders, customers, products).
 ✅ You want to combine them into a single table (new_common_table).
 ✅ You want to apply simple transformations before loading data into a destination.

2. How Hevo Transformations Work
In Hevo, incoming data events contain:
Event Name → The table name from which the data is coming.


Properties → The actual data fields (columns and values).


Hevo allows you to modify these events before they are loaded into the final database.
We use a transformation script to rename the event name, so data from different tables is directed into one table.

3. Transformation Scripts
🔹 3.1. Merging All Tables into One
If you want all incoming tables to be merged into one destination table, use this script:
📌 Code:

from io.hevo.api import Event

def transform(event):
    # Get event name from the event
    eventName = event.getEventName()

    # Get properties (actual data) from the event
    properties = event.getProperties()

    # Rename the event to the destination table
    event.rename('new_common_table')

    return event

🔹 How This Works:
Any table (orders, customers, etc.) will have its name changed to new_common_table.


The data will be stored in this single destination table in Hevo.



🔹 3.2. Merging Only Selected Tables
If you only want specific tables (e.g., city, bcd) to be merged, use this script:
📌 Code:
from io.hevo.api import Event

def transform(event):
    # Get event name from the event
    eventName = event.getEventName()

    # Get properties from the event
    properties = event.getProperties()

    # Only rename specific tables (e.g., city, bcd)
    if eventName in ['city', 'bcd']:  
        event.rename('new_common_table')

    return event

🔹 How This Works:
Only tables named city and bcd will be merged into new_common_table.


Other tables will remain unchanged.



4. Setting Primary Keys in Hevo
If your new_common_table needs a Primary Key (e.g., id), you can:
Set the Primary Key in the Hevo Schema Mapper.


Set it via Transformation Rules inside Hevo.


🔗 Reference: Setting Primary Keys in Hevo

5. How to Test Your Transformation
Before applying the transformation, you should test it in Hevo:
Go to Hevo → Pipelines → Transformations.


Paste the script and run a test event.


Check if data is getting renamed correctly to new_common_table.


🔗 Reference: Testing Transformations in Hevo

