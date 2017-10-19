
In general we try to follow the common community guidelines,
including PEP-8 and PEP-257. But these don't cover everything
important and we make a few exceptions.

## flake8

Every commit should pass an automated flake8 check with the plugins `pep8`,
`mccabe`, and `pep8-naming` and this configuration:

```ini
# one section of flake.cfg

[flake8]
#ignore=E501,E225,E261,W391,E241,E203,W292,W391

exclude=.git,migrations,docs,scripts
max-complexity=8
max-line-length = 119
statistics=True
jobs=1
```

### Commit hooks

Git hooks are great for fast and light-weight tests. Here's how you can setup
your commit hooks for automated style checks. This assumes your project has a
Makefile with a linter command named `check`:

    # .git/hooks/pre-commit

    #!/bin/sh
    make check

Make sure that your virtualenv containing flake8 is activated when committing.
Also note that this probably won't work form within Sourcetree, but it's better
for you to stay in the shell anyway.

*TODO: consider also using the `flake8-pep257` and `flake8-print` plugins to
automate more tests.*

## Documentation

### class docstrings

Whenever you create a class, add a docstring with at least a one-liner:

```py
class SomeClass(object):
    """The one-line explaination"""
    pass
```

If a longer description would be helpful, skip a line and use more sections
(each is optional).  Don't provide useless information like "the attribute
`name` is the name of the object":

```py
class SomeClass(object):
    """Always start with a stand-alone one-liner

    This class has no side-effects.

    Attributes:
        name: what end-users call this instance
    """
    pass
```

### Function docstrings

Similarly:

```py
def simple_function(abc):
    """This function ignores the arguments and always returns None"""
    pass

def complex_function(abc):
    """Always use a one-liner

    Arguments:
        abc: the letters of the alphabet
    """
    pass
```

### Blank lines

Don't include unnecessary blank lines around the docstrings.

## Imports

Do not use wildcard imports.

Imports don't have to be in alphabetical order. It is however more or less of a
convention that imports that are the furthest away from the current module in
are the highest on top. So standard library imports like `os`, `system` etc. go
on top. Then come imports from installed packages; `django`, `celery` etc. and
finally that belong to the current project.

Prefer one line for one import

## Libraries

Before adding a new library, consider the long-term maintenance cost and risk
of abandoned projects. It's often easier to copy code into our project or write
it ourselves. If we can't use a stable and recent PyPi release, the threshold
for time-saved should be even higher.

We have agreed that the following Python libraries are definitely worth it:

- Django
- Django REST Framework
- Flask
- Swagger / OpenAPI
- psycopg2
- elasticsearch
- elasticsearch-dsl

## Naming

- don't start method names with `get_` or `set_`. Use properties if possible.

## Testing

- new behaviors should be accompanied by new tests
- if a behavior is changed and no tests break, that indicates
  an important hole in our coverage.
- tests should work without internet access or a local database installed

Use the following testing libraries:

- Mock
- py.test

