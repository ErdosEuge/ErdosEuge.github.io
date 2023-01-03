---
layout: default
---

# Tech Notes

Here you're going to find some code notes recorded along the way.
Blocks are mainly written  in *Python* or *Pyspark*, but of course, *R* is always in my  ❤️

Please have a look (forgive the mess). 😊



*How to except all errors in Python (ugly and dangerous way)*
```python
import traceback
import logging

try:
    whatever()
except Exception as e:
    logging.error(traceback.format_exc())
    # Logs the error appropriately. 
```

*How to check if a pd.DataFrame object is empty*:
```python
import pandas as pd

# Create an empty DataFrame
df = pd.DataFrame()

# Check if the DataFrame is empty
if df.empty:
    print('DataFrame is empty')
else:
    print('DataFrame is not empty')
```

[back](../)