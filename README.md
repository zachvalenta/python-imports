# what is this?

* sandbox to explore Python's import system

# examples

## from same directory

```sh
├── bar.py
├── foo.py
```

```python
# bar.py
import foo
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
