# Circular dependencies

Type hinting can introduce circular dependencies. To fix circular dependencies while keeping type hints we need to do the following.&#x20;

## Example

```python
from __future__ import annotations
from typing import TYPE_CHECKING

if TYPE_CHECKING:
    from models import User

class UserController:
    def __init__(self, book: User) -> None:
        self.user = user
```

The import from \_\_future\_\_ import annotations makes it possible to call the User object without making it a string. The TYPE\_CHECKING variable is False by default but True for linters making it possible to support type hinting while not having any circular dependencies at runtime.

## Resources

* [https://stackoverflow.com/questions/33837918/type-hints-solve-circular-dependency](https://stackoverflow.com/questions/33837918/type-hints-solve-circular-dependency)
* [https://adamj.eu/tech/2021/05/13/python-type-hints-how-to-fix-circular-imports/](https://adamj.eu/tech/2021/05/13/python-type-hints-how-to-fix-circular-imports/)
