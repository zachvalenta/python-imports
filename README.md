# what is this?

* exploration of Python's import system

# examples

## same pkg

```sh
├── bar.py
├── foo.py
```

```python
# bar.py
import foo
```

```python
# foo.py
def foo_func():
    print('hi from foo_func')
```

```sh
$ py3 bar.py
$
```

```sh
>>> import bar
>>> bar.foo.foo_func() # bar knows about all of foo's attributes
hi from foo_func
```

## child pkg (namespace) - whole pkg

```sh
├── bar.py
├── foo.py
├── child
│   └── kid.py
```

```python
# bar.py
import foo
import child
```

```python
# foo.py
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
