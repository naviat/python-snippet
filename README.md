# Python Snippet

Some snippet use for daily tasks

## 1. Invert a Dictionary

```python
# Use to invert dictionaries that have unique values
my_inverted_dict = dict(map(reversed, my_dict.items()))
 
# Use to invert dictionaries that have unique values
my_inverted_dict = {value: key for key, value in my_dict.items()}
 
# Use to invert dictionaries that have non-unique values
from collections import defaultdict
my_inverted_dict = defaultdict(list)
{my_inverted_dict[v].append(k) for k, v in my_dict.items()}
 
# Use to invert dictionaries that have non-unique values
my_inverted_dict = dict()
for key, value in my_dict.items(): 
  my_inverted_dict.setdefault(value, list()).append(key)
 
# Use to invert dictionaries that have lists of values
my_dict = {value: key for key in my_inverted_dict for value in my_map[key]}
```

## 2. Sum Elements of Two Lists in Python

```python
ethernet_devices = [1, [7], [2], [8374163], [84302738]]
usb_devices = [1, [7], [1], [2314567], [0]]
 
# The long way
all_devices = [
  ethernet_devices[0] + usb_devices[0], 
  ethernet_devices[1] + usb_devices[1], 
  ethernet_devices[2] + usb_devices[2], 
  ethernet_devices[3] + usb_devices[3], 
  ethernet_devices[4] + usb_devices[4]
]
 
# Some comprehension magic
all_devices = [x + y for x, y in zip(ethernet_devices, usb_devices)]
 
# Let's use maps
import operator 
all_devices = list(map(operator.add, ethernet_devices, usb_devices))
 
# We can't forget our favorite computation library
import numpy as np 
all_devices = np.add(ethernet_devices, usb_devices)
 
```

## 3. Check if a File Exists

```python
# Brute force with a try-except block (Python 3+)
try: 
  with open('/path/to/file', 'r') as fh: 
    pass
except FileNotFoundError: 
  pass
 
# Leverage the OS package (possible race condition)
import os 
exists = os.path.isfile('/path/to/file')
 
# Wrap the path in an object for enhanced functionality
from pathlib import Path
config = Path('/path/to/file') 
if config.is_file(): 
  pass
```

## 4. Convert Two List Into a Dictionary

```python
column_names = ['id', 'color', 'style']
column_values = [1, 'red', 'bold']
 
# Convert two lists into a dictionary with zip and the dict constructor
name_to_value_dict = dict(zip(column_names, column_values))
 
# Convert two lists into a dictionary with a dictionary comprehension
name_to_value_dict = {key:value for key, value in zip(column_names, column_values)}
 
# Convert two lists into a dictionary with a loop
name_value_tuples = zip(column_names, column_values) 
name_to_value_dict = {} 
for key, value in name_value_tuples: 
  if key in name_to_value_dict: 
    pass # Insert logic for handling duplicate keys 
  else: 
    name_to_value_dict[key] = value
```

## 5. Check if a List in Empty

```python
my_list = list()
 
# Check if a list is empty by its length
if len(my_list) == 0: 
  pass # the list is empty
 
# Check if a list is empty by direct comparison (only works for lists)
if my_list == []: 
  pass # the list is empty
 
# Check if a list is empty by its type flexibility **preferred method**
if not my_list: 
  pass # the list is empty
```

## 6. Clone a List

```python
my_list = [27, 13, -11, 60, 39, 15]
 
# Clone a list by brute force
my_duplicate_list = [item for item in my_list]
 
# Clone a list with a slice
my_duplicate_list = my_list[:]
 
# Clone a list with the list constructor
my_duplicate_list = list(my_list) 
 
# Clone a list with the copy function (Python 3.3+)
my_duplicate_list = my_list.copy() # preferred method
 
# Clone a list with the copy package
import copy
my_duplicate_list = copy.copy(my_list)
my_deep_duplicate_list = copy.deepcopy(my_list)
 
# Clone a list with multiplication?
my_duplicate_list = my_list * 1 # do not do this
```

## 7. Get the Last Item of a List in Python

```python
my_list = ['red', 'blue', 'green']
 
# Get the last item with brute force using len
last_item = my_list[len(my_list) - 1]
 
# Remove the last item from the list using pop
last_item = my_list.pop() 
 
# Get the last item using negative indices *preferred & quickest method*
last_item = my_list[-1]
 
# Get the last item using iterable unpacking
*_, last_item = my_list
```

## 8. Make a Python Script Shortcut with Arguments

```shell
#!/bin/sh
python /path/to/trc-image-titler.py -o /path/to/output
```

## 9. Sort a List of Strings in Python

```python
my_list = ["leaf", "cherry", "fish"]
 
# Brute force method using bubble sort
my_list = ["leaf", "cherry", "fish"]
size = len(my_list)
for i in range(size): 
  for j in range(size): 
    if my_list[i] < my_list[j]: 
       temp = my_list[i] 
       my_list[i] = my_list[j] 
       my_list[j] = temp
 
# Generic list sort *fastest*
my_list.sort()
 
# Casefold list sort
my_list.sort(key=str.casefold)
 
# Generic list sorted
my_list = sorted(my_list) 
 
# Custom list sort using casefold (>= Python 3.3)
my_list = sorted(my_list, key=str.casefold) 
 
# Custom list sort using current locale 
import locale
from functools import cmp_to_key
my_list = sorted(my_list, key=cmp_to_key(locale.strcoll)) 
 
# Custom reverse list sort using casefold (>= Python 3.3)
my_list = sorted(my_list, key=str.casefold, reverse=True)
```

## 10. Parse a Spreadsheet

```python
# Brute force solution
csv_mapping_list = []
with open("/path/to/data.csv") as my_data: 
  line_count = 0 
  for line in my_data: 
    row_list = [val.strip() for val in line.split(",")] 
    if line_count == 0: 
      header = row_list 
    else: 
      row_dict = {key: value for key, value in zip(header, row_list)}
      csv_mapping_list.append(row_dict) 
    line_count += 1
 
# CSV reader solution
import csv
csv_mapping_list = []
with open("/path/to/data.csv") as my_data: 
  csv_reader = csv.reader(my_data, delimiter=",") 
  line_count = 0 
  for line in csv_reader: 
    if line_count == 0: 
      header = line 
    else: 
      row_dict = {key: value for key, value in zip(header, line)} 
      csv_mapping_list.append(row_dict) 
    line_count += 1
 
# CSV DictReader solution
import csv
with open("/path/to/dict.csv") as my_data: 
  csv_mapping_list = list(csv.DictReader(my_data))
```

## 11. Sort a List of Dictionaries

```python
csv_mapping_list = [
  { "Name": "Jeremy", "Age": 25, "Favorite Color": "Blue" }, 
  { "Name": "Ally", "Age": 41, "Favorite Color": "Magenta" }, 
  { "Name": "Jasmine", "Age": 29, "Favorite Color": "Aqua" }
]
 
# Custom sorting
size = len(csv_mapping_list)
for i in range(size): 
  min_index = i 
  for j in range(i + 1, size): 
    if csv_mapping_list[min_index]["Age"] > csv_mapping_list[j]["Age"]: 
      min_index = j 
      csv_mapping_list[i], csv_mapping_list[min_index] = csv_mapping_list[min_index], csv_mapping_list[i]
 
# List sorting function
csv_mapping_list.sort(key=lambda item: item.get("Age"))
 
# List sorting using itemgetter
from operator import itemgetter
f = itemgetter('Name')
csv_mapping_list.sort(key=f)
 
# Iterable sorted function
csv_mapping_list = sorted(csv_mapping_list, key=lambda item: item.get("Age"))
```

## 12. Write a List Comprehension

```python
# Define a generic 1D list of constants
my_list = [2, 5, -4, 6]
 
# Duplicate a 1D list of constants
[item for item in my_list]
 
# Duplicate and scale a 1D list of constants
[2 * item for item in my_list]
 
# Duplicate and filter out non-negatives from 1D list of constants
[item for item in my_list if item < 0]
 
# Duplicate, filter, and scale a 1D list of constants
[2 * item for item in my_list if item < 0]
 
# Generate all possible pairs from two lists
[(a, b) for a in (1, 3, 5) for b in (2, 4, 6)]
 
# Redefine list of contents to be 2D
my_list = [[1, 2], [3, 4]]
 
# Duplicate a 2D list
[[item for item in sub_list] for sub_list in my_list]
 
# Duplicate an n-dimensional list
def deep_copy(to_copy): 
  if type(to_copy) is list: 
    return [deep_copy(item) for item in to_copy] 
  else: 
    return to_copy
```

## 13. Merge Two Dictionaries

```python
yusuke_power = {"Yusuke Urameshi": "Spirit Gun"}
hiei_power = {"Hiei": "Jagan Eye"}
powers = dict()
 
# Brute force
for dictionary in (yusuke_power, hiei_power): 
  for key, value in dictionary.items(): 
    powers[key] = value
 
# Dictionary Comprehension
powers = {key: value for d in (yusuke_power, hiei_power) for key, value in d.items()}
 
# Copy and update
powers = yusuke_power.copy()
powers.update(hiei_power)
 
# Dictionary unpacking (Python 3.5+)
powers = {**yusuke_power, **hiei_power}
 
# Backwards compatible function for any number of dicts
def merge_dicts(*dicts: dict): 
  merged_dict = dict() 
  for dictionary in dicts: 
    merge_dict.update(dictionary) 
  return merged_dict
```

## 14. Format a String in Python

```python
name = "Jeremy"
age = 25
 
# String formatting using concatenation
print("My name is " + name + ", and I am " + str(age) + " years old.")
 
# String formatting using multiple prints
print("My name is ", end="")
print(name, end="")
print(", and I am ", end="")
print(age, end="")
print(" years old.")
 
# String formatting using join
print(''.join(["My name is ", name, ", and I am ", str(age), " years old"]))
 
# String formatting using modulus operator
print("My name is %s, and I am %d years old." % (name, age))
 
# String formatting using format function with ordered parameters
print("My name is {}, and I am {} years old".format(name, age))
 
# String formatting using format function with named parameters
print("My name is {n}, and I am {a} years old".format(a=age, n=name))
 
# String formatting using f-Strings (Python 3.6+)
print(f"My name is {name}, and I am {age} years old")

```

## 15.  Print on the Same Line in Python

```python
# Python 2 only
print "Live PD",
 
# Backwards compatible (also fastest)
import sys
sys.stdout.write("Breaking Bad")
 
# Python 3 only
print("Mob Psycho 100", end="")
```

## 16. Performance Test Python Code

```python
# Brute force solution
import datetime
start_time = datetime.datetime.now()
[(a, b) for a in (1, 3, 5) for b in (2, 4, 6)] 
# example snippet
end_time = datetime.datetime.now()
print end_time - start_time
 
# timeit solution
import timeit
min(timeit.repeat("[(a, b) for a in (1, 3, 5) for b in (2, 4, 6)]"))
 
# cProfile solutionimport cProfile
cProfile.run("[(a, b) for a in (1, 3, 5) for b in (2, 4, 6)]")
```

... Updating !