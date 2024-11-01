### Meta
2024-10-29 13:12
**Tags:** [[python]] [[py_basics]] [[py_lists]]
**Status:** #pending 

### Avoiding Index Errors when Working with Lists
```Python title:motorcycles.py
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles[3])
```

This example results in an *index error*:
```BASH title:output.sh
Traceback (most recent call last):
  File "motorcycles.py", line 2, in <module>
    print(motorcycles[3])
          ~~~~~~~~~~~^^^
IndexError: list index out of range
```

An index error means Python can’t find an item at the index you requested.

Whenever you want to access the last item in a list, you should use the index `-1`. The only time it produces an error is when requesting the last item from an empty list.