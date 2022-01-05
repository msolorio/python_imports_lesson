# Python 3 Imports for 6 Year Olds

Learn once and for all how to use relative and absolute imports in Python 3!

## Quick Notes
- When a file is run directly, it is denoted as the `__main__` file.
- Absolute imports specify a path relative to the `__main__` file.
- Relative imports specify a path relative to the current file of the import statement.
- The `__main__` file can only include absolute imports and not relative imports.
- Prefer absolute imports when possible, as scripts that use relative imports cannot be run directly.
- Python 3.3 and above only allows explicit relative imports, and not implicit relative imports, so those will not be covered.

---

Assume this file structure.
```
project
├── main.py
└── my_package
    ├── my_module.py
    └── my_other_module.py
```

## \_\_main\_\_ File
- When a file is run directly it is denoted as the "\_\_main\_\_" file. That is, `__name__` is set to `__main__` for that file.
- If a file is run indirectly, by being imported from another file, `__name__` is set to the name of the module, For example, `__my_module__`.

---

### Absolute Import - Case #1

in `main.py`
```py
from my_package.my_module import my_var

print(my_var)
```

in `my_package/my_module.py`
```py
my_var = 'a variable'
```

Now run `main.py`
```bash
python3 main.py
```

In Case #1, we include the absolute path to `my_module.py` and import `my_var`

---

### Absolute Import - Case #2
in `main.py`
```py
from my_package.my_module import my_var

print(my_var)
```

in `my_package/my_module.py`
```py
from my_package.my_other_module import my_other_var

my_var = 'some text and ' + my_other_var
```

in `my_package/my_other_module.py`
```py
my_other_var = 'my other variable'
```

Now run `main.py`
```bash
python3 main.py
```

In Case #2,
- we include an absolute path to `my_module` within `main.py`, as well as an absolute path `my_other_module` in `my_module.py`.
- The absolute import specifies the path relative to the `__main__` file, the file being run directly from the command line, in this case, `main.py`.
- If we were to try and run `my_package/my_module.py` directly, the import statement would break. The absolute path is assuming `main.py` is the \_\_main\_\_ file.

---

### Relative Import - Case #1

A relative import specifies a path relative to the current file of the import statement. Let us now assume this code, changing the import statement in `my_package/my_module.py`

in `main.py`
```py
from my_package.my_module import my_var

print(my_var)
```

in `my_package/my_module.py`
```py
from .my_other_module import my_other_var

my_var = 'some text and ' + my_other_var
```

in `my_package/my_other_module.py`
```py
my_other_var = 'my other variable'
```

Now run `main.py`
```bash
python3 main.py
```

In Case #1,
- The import statement in `my_package/my_module.py` has been changed to a relative import.
- The import statement specifies a file path relative to the current location of the import statement.
- This code should still function properly when running `python3 main.py`.
- If we were to try to run `my_package/my_module.py` directly, the code would break. `my_module.py` would then be the `__main__` file and relative imports are not allowed in the `__main__` file.

---

### Relative Imports - Other Uses

Stepping into a nested directories
```py
from .dir1.dir2.my_module import my_var
```

Steping out of a directory - Here we step out of our current directory to access a file at a higher level
```py
from ..main import other_var
```

Stepping out of 2 Directories
```py
from ...main import other_var
```

- Using relative paths we can not run these files directly by calling `python3 name_of_file.py`.
- We can however run the file as a module using the `-m` flag.
  - as in `python3 -m name_of_file`
  - notice we do not include the file extension here.
