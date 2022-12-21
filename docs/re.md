# [正则表达式 regular expression](https://docs.python.org/3/library/re.html)


```python
import re
```



## Match Object

A Match Object is an object containing information about the search and the result.

`.span()` returns a tuple containing the start-, and end positions of the match.
`.string` returns the string passed into the function
`.group()` returns the part of the string where there was a match

```python
#Search for an upper case "S" character in the beginning of a word
txt = "The S rain in Spain"
x = re.search(r"\bS\w+", txt)
print(x.span())  # (14, 19)
print(x.string)  # The S rain in Spain
print(x.group())  # Spain
```



## Functions

| Function              | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| [findall](###findall) | Returns a list containing all matches                        |
| [search](###search)   | Returns a [Match object](##Match Object) if there is a match anywhere in the string |
| [split](###split)     | Returns a list where the string has been split at each match |
| [sub](###sub)         | Replaces one or many matches with a string                   |



### findall

The `findall()` function returns a list containing all matches.

```python
txt = "The rain in Spain"
x = re.findall("^ai", txt)  # []
x = re.findall("ai", txt)  # ['ai', 'ai']
x = re.findall(r".i", txt)  # ['ai', ' i', 'ai']
```



### search

The `search()` function searches the string for a match, and returns a [Match object](##Match Object) if there is a match.

If there is more than one match, only the first occurrence of the match will be returned:

```python
txt = "The rain in Spain"
x = re.search("\s", txt)  # <re.Match object; span=(3, 4), match=' '>
x = re.search("ai", txt)  # <re.Match object; span=(5, 7), match='ai'>
x = re.search("aai", txt)  # None
```



### split

The `split()` function returns a list where the string has been split at each match:

```python
txt = "The rain in Spain"
x = re.split("\s", txt)  # ['The', 'rain', 'in', 'Spain']
x = re.split("aai", txt)  # ['The rain in Spain']
```



### sub

The `sub()` function replaces the matches with the text of your choice:

```python
txt = "The rain in Spain"
x = re.sub("\s", "_", txt)  # The_rain_in_Spain
x = re.sub("aai", "_", txt)  # The rain in Spain
x = re.sub("\s", "_", txt, count=2)  # The_rain_in Spain
```



## Metacharacters

| Character | Description                                                  | Example        |
| --------- | ------------------------------------------------------------ | -------------- |
| []        | A set of characters                                          | "[a-m]"        |
| \         | Signals a special sequence <br />(can also be used to escape special characters) | "\d"           |
| .         | Any character (except newline character)                     | "he..o"        |
| ^         | Starts with                                                  | "^hello"       |
| $         | Ends with                                                    | "planet$"      |
| *         | Zero or more occurrences                                     | "he.*o"        |
| +         | One or more occurrences                                      | "he.+o"        |
| ?         | Zero or one occurrences                                      | "he.?o"        |
| {}        | Exactly the specified number of occurrences                  | "he.{2}o"      |
| \|        | Either or                                                    | "falls\|stays" |
| ()        | Capture and group                                            |                |



## Special Sequences

| Character | Description                                                  | Example           |
| --------- | ------------------------------------------------------------ | ----------------- |
| \A        | Returns a match if the specified characters are at the beginning of the string | "\AThe"           |
| \b        | Returns a match where the specified characters are at the beginning or at the end of a word | r"\bain" r"ain\b" |
| \B        | Returns a match where the specified characters are present, but **NOT** at the beginning (or at the end) of a word | r"\Bain" r"ain\B" |
| \d        | Returns a match where the string contains digits (numbers from 0-9) | "\d"              |
| \D        | Returns a match where the string **DOES NOT** contain digits | "\D"              |
| \s        | Returns a match where the string contains a white space character | "\s"              |
| \S        | Returns a match where the string **DOES NOT** contain a white space character | "\S"              |
| \w        | Returns a match where the string contains any word characters (characters from a to Z, digits from 0-9, and the underscore _ character) | "\w"              |
| \W        | Returns a match where the string **DOES NOT** contain any word characters | "\W"              |
| \Z        | Returns a match if the specified characters are at the end of the string | "Spain\Z"         |



## Sets

| Set         | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| [arn]       | Returns a match where one of the specified characters (`a`, `r`, or `n`) is present |
| [a-n]       | Returns a match for any lower case character, alphabetically between `a` and `n` |
| [^arn]      | Returns a match for any character **EXCEPT** `a`, `r`, and `n` |
| [0123]      | Returns a match where any of the specified digits (`0`, `1`, `2`, or `3`) are present |
| [0-9]       | Returns a match for any digit between `0` and `9`            |
| [0-5] [0-9] | Returns a match for any two-digit numbers from `00` and `59` |
| [a-zA-Z]    | Returns a match for any character alphabetically between `a` and `z`, **lower case OR upper case** |

