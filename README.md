
`regreplace` replaces regex matches with named groups by their group name.

# Installation

```
pip install regreplace
```

# Usage

```
from regreplace import Replacer

s = r'C:\Folder\file_19001010-010101.txt'
new_date = "20001111-101010"

# Instantiate for every pattern a new Replacer Instance
r = Replacer(pattern=r".*?_(?P<date>\d{8}-\d{6}( \(1\))*)(?P<ext>\..+$)")  

# inspect what was matched for each group by name
r.match(s, 'date') # '19000101-014356'
r.match(s, 'ext')  # '.spc'

r.replace(s, 'date', new_date) # 'C:\\Folder\\file_19001010-010101.csv'
r.replace(s, 'ext', '.csv')    # 'C:\\Folder\\file_20001111-101010.txt'
```

In this way, you can replace matches to named groups of a regex by the given value.



```
