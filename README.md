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
>>> bar.foo.foo_func()
hi from foo_func
```

## child pkg (namespace)

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
>>> bar.child.kid_func()
Traceback (most recent call last):
  File "<input>", line 1, in <module>
    bar.child.kid_func()
AttributeError: module 'child' has no attribute 'kid_func'
```

## child pkg (regular)

* otherwise same as namespace but w/ addition of `__init__.py` in `child` directory

```sh
>>> bar.child
<module 'child' from '/Users/zach/Desktop/zvmac/materials/sw/lang/python/impor
tmess/child/__init__.py'> 
```