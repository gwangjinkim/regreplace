
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
# The regex pattern must contain at least one named group
# which have the form `(?P<name>...)` where `...` is placeholder for some regex pattern and `name`
# the place folder for some group name.
r = Replacer(pattern=r".*?_(?P<date>\d{8}-\d{6}( \(1\))*)(?P<ext>\..+$)")  

# inspect what was matched for each group by name
r.match(s, 'date') # '19001010-010101'
r.match(s, 'ext')  # '.txt'

r.replace(s, 'date', new_date) # 'C:\\Folder\\file_19001010-010101.csv'
r.replace(s, 'ext', '.csv')    # 'C:\\Folder\\file_20001111-101010.txt'
```

In this way, you can replace matches to named groups of a regex by the given value.


While replacing, you can use also matches:
```
import datetime

DATE="%Y%m%d-%H%M%S"

def add_3_days(datestr, _format=DATE):
    dt = datetime.datetime.strptime(datestr, _format) + datetime.timedelta(days=3)
    return dt.strftime(_format) # return same format
    
r.replace(s, 'date', add_3_days(r.match(s, 'date'))  ## 'C:\\Folder\\file_19001013-010101.txt'
```
