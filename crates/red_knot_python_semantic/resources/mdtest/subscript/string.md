# String subscripts

## Indexing

```py
s = "abcde"

reveal_type(s[0])  # revealed: Literal["a"]
reveal_type(s[1])  # revealed: Literal["b"]
reveal_type(s[-1])  # revealed: Literal["e"]
reveal_type(s[-2])  # revealed: Literal["d"]

reveal_type(s[False])  # revealed: Literal["a"]
reveal_type(s[True])  # revealed: Literal["b"]

a = s[8]  # error: [index-out-of-bounds] "Index 8 is out of bounds for string `Literal["abcde"]` with length 5"
reveal_type(a)  # revealed: Unknown

b = s[-8]  # error: [index-out-of-bounds] "Index -8 is out of bounds for string `Literal["abcde"]` with length 5"
reveal_type(b)  # revealed: Unknown

def int_instance() -> int: ...

a = "abcde"[int_instance()]
# TODO: Support overloads... Should be `str`
reveal_type(a)  # revealed: @Todo
```

## Slices

```py
s = "abcde"

reveal_type(s[0:0])  # revealed: Literal[""]
reveal_type(s[0:1])  # revealed: Literal["a"]
reveal_type(s[0:2])  # revealed: Literal["ab"]
reveal_type(s[0:5])  # revealed: Literal["abcde"]
reveal_type(s[0:6])  # revealed: Literal["abcde"]
reveal_type(s[1:3])  # revealed: Literal["bc"]

reveal_type(s[-3:5])  # revealed: Literal["cde"]
reveal_type(s[-4:-2])  # revealed: Literal["bc"]
reveal_type(s[-10:10])  # revealed: Literal["abcde"]

reveal_type(s[0:])  # revealed: Literal["abcde"]
reveal_type(s[2:])  # revealed: Literal["cde"]
reveal_type(s[5:])  # revealed: Literal[""]
reveal_type(s[:2])  # revealed: Literal["ab"]
reveal_type(s[:0])  # revealed: Literal[""]
reveal_type(s[:2])  # revealed: Literal["ab"]
reveal_type(s[:10])  # revealed: Literal["abcde"]
reveal_type(s[:])  # revealed: Literal["abcde"]

reveal_type(s[::-1])  # revealed: Literal["edcba"]
reveal_type(s[::2])  # revealed: Literal["ace"]
reveal_type(s[-2:-5:-1])  # revealed: Literal["dcb"]
reveal_type(s[::-2])  # revealed: Literal["eca"]
reveal_type(s[-1::-3])  # revealed: Literal["eb"]

reveal_type(s[None:2:None])  # revealed: Literal["ab"]
reveal_type(s[1:None:1])  # revealed: Literal["bcde"]
reveal_type(s[None:None:None])  # revealed: Literal["abcde"]

start = 1
stop = None
step = 2
reveal_type(s[start:stop:step])  # revealed: Literal["bd"]

reveal_type(s[False:True])  # revealed: Literal["a"]
reveal_type(s[True:3])  # revealed: Literal["bc"]

s[0:4:0]  # error: [zero-stepsize-in-slice]
s[:4:0]  # error: [zero-stepsize-in-slice]
s[0::0]  # error: [zero-stepsize-in-slice]
s[::0]  # error: [zero-stepsize-in-slice]

def int_instance() -> int: ...

substring1 = s[int_instance() : int_instance()]
# TODO: Support overloads... Should be `LiteralString`
reveal_type(substring1)  # revealed: @Todo

def str_instance() -> str: ...

substring2 = str_instance()[0:5]
# TODO: Support overloads... Should be `str`
reveal_type(substring2)  # revealed: @Todo
```
