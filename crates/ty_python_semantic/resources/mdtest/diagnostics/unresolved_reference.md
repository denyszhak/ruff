# Diagnostics for unresolved references

## New builtin used on old Python version

<!-- snapshot-diagnostics -->

```toml
[environment]
python-version = "3.9"
```

```py
aiter  # error: [unresolved-reference]
```

## Typing builtin has Info help

A special diagnostic is emitted when using a deprecated alias from Typing that is builtin in this
version of Python. (full diagnostic captured in snapshot)

### Info present in Python 3.9+

<!-- snapshot-diagnostics -->

```toml
[environment]
python-version = "3.9"
```

```py
foo: List[int]  # error: [unresolved-reference]
bar: Type  # error: [unresolved-reference]
```

### Info not present before Python 3.9

<!-- snapshot-diagnostics -->

```toml
[environment]
python-version = "3.8"
```

```py
foo: List[int]  # error: [unresolved-reference]
bar: Type  # error: [unresolved-reference]
```

## Internal builtins typevars are unresolved

Typeshed's `builtins.pyi` can define helper `TypeVar` names (such as `_T`) for stub internals.
Those names are not user-facing builtins and should be unresolved in normal user code.

```py
x: _T  # error: [unresolved-reference]
y: _T_co  # error: [unresolved-reference]
z: _VT  # error: [unresolved-reference]
```
