# yv
Simple utils to get stuff out of Mappings (dict-like objects).

To install:	```pip install yv```

## Overview
The `yv` package provides a collection of utilities designed to facilitate the extraction, manipulation, and querying of data from dictionary-like objects in Python. These utilities are particularly useful when dealing with nested or complex data structures commonly encountered in data processing tasks.

## Features
- **Key Chain Extraction**: Retrieve values from a dictionary using a list of potential keys.
- **Subdictionary Access**: Enhanced dictionary class allowing for easy subdictionary creation and batch key retrieval.
- **MongoDB-style Querying**: Filter dictionary items using MongoDB-like query language.
- **Nested Key Paths**: Functions to handle nested dictionary paths for setting and getting values.
- **Utility Functions**: Includes various utility functions for dictionary manipulation and querying.

## Usage Examples

### Key Chain Extraction
Retrieve values from a dictionary using a list of potential keys, with the first found key's value being returned.
```python
from yv import key_chain

d = {'a': 1, 'b': 2, 'c': 3}
result = key_chain(d, 'x', 'c', 'b')  # Returns 3
```

### Subdictionary Access
Enhanced dictionary class that interprets lists and sets of keys as requests for subdictionaries.
```python
from yv import Subdict

d = {'a': 1, 'b': 2, 'c': 3}
dd = Subdict(d)
subdict = dd('a', 'b', c=100, d=100)  # Returns {'a': 1, 'b': 2, 'c': 3, 'd': 100}
```

### MongoDB-style Querying
Filter dictionary items using a MongoDB-like query.
```python
from yv import dict_filt_from_mg_filt

mg_filt = {'a': {'$gte': 10, '$lt': 20}}
filt = dict_filt_from_mg_filt(mg_filt)
result = list(filter(filt, [{'a': x} for x in range(9, 22)]))  # Returns [{'a': 10}, {'a': 15}]
```

### Nested Key Paths
Set and get values in a dictionary using dot-separated string paths or lists of keys.
```python
from yv import set_value_in_nested_key_path, get_value_in_key_path

d = {}
set_value_in_nested_key_path(d, 'a.b.c', 100)
print(d)  # Outputs: {'a': {'b': {'c': 100}}}

value = get_value_in_key_path(d, 'a.b.c')  # Returns 100
```

### Utility Functions
Various utility functions to manipulate and query dictionaries.
```python
from yv import left_union, all_but

d = {'a': 1, 'b': 2}
defaults = {'b': 3, 'c': 4}
new_d = left_union(d, defaults)  # Returns {'b': 2, 'c': 4, 'a': 1}

filtered_d = all_but(d, ['a'])  # Returns {'b': 2}
```

## Documentation
Each function and class within the `yv` package is documented with docstrings, providing detailed usage instructions and examples. This documentation can be accessed via Python's built-in help system or by reading the source code directly.

For more detailed examples and usage, refer to the function and class definitions in the source code.