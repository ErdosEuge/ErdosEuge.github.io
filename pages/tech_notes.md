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


[back](../)