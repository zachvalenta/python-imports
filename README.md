# overview

This is an exploration of Python's import system.

Some imports are easy (stdlib, third-party package from a virtual environment), but user-defined modules can get tricky as you move beyond importing sibling modules.

# examples

📝 An alternate interactive interpreter like `bpython` or `ptpython` will have autocomplete, so as you type you'll be able to see what attributes are available on the module you've imported:

```sh
$ bpy
bpython version 0.17.1 on top of Python 3.6.1 /Library/Frameworks/Python.framework/Versions/3.6/bin/python3.6
>>> import alice
>>> alice.
bob    grandkid    kid
```

## same pkg

```sh
├── alice.py # import bob
├── bob.py # def bob_func(): print('hi from bob func')
```

```sh
$ py3 alice.py
$
```

```sh
>>> import alice
>>> alice.bob.bob_func1()
hi from bob func 1
>>> alice.bob.bob_func2()
hi from bob func 2
```

## child pkg (namespace) - whole pkg

```sh
├── bar.py
├── baz.py
├── child
│   └── kid.py
```

```python
# bar.py
import baz
import child
```

```python
# kid.py
def kid_func():
    print('hi from kid_func')
```

```sh
$ py3 bar.py
$
```

```sh
>>> import bar

>>> bar.child
<module 'child' (namespace)>

>>> bar.child.kid # bar has attr child but doesn't know about child's attr
AttributeError: module 'child' has no attribute 'kid'

>>> bar.child.kid.kid_func() # at any level
AttributeError: module 'child' has no attribute 'kid_func'
```

## child pkg (regular) - whole pkg

* otherwise same as namespace but w/ addition of `__init__.py` in `child` directory

```sh
>>> bar.child
<module 'child' from '/Users/zach/Desktop/zvmac/materials/sw/lang/python/impor
tmess/child/__init__.py'> 
```

## child pkg (namespace) - specific submodule

* otherwise same as 'child pkg (namespace) - whole pkg' but update import syntax:

```diff
- import child
+ from child import kid
```

```sh
>>> import bar
>>> bar.kid.kid_func()
hi from kid_func
```

## grandchild pkg (namespace)

```sh
├── README.md
├── bar.py
├── child
│   ├── grandchild
│   │   └── grandkid.py
│   └── kid.py
└── foo.py
```

```python
# bar.py
import foo
from child import kid
from child.grandchild import grandkid
```

```sh
$ py3 bar.py
$
```

```sh
$ bpy
>>> import child.grandchild
>>> import child.grandchild.grandkid
```
