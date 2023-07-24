# Django Language Template:
## Variables:
- Variables look like this: `{{variable}}`
- When the template engine encounters a variable, it evaluates that variable and replaces it with the result.
#### Rules:-
- Variable names consist of any combination of alphanumeric characters and the underscore.
- Variable name should not start with underscore.
- Variable name can not have spaces or punctuation characters.

#### [Basic Example](https://github.com/IshaanAdarsh/TIL/blob/main/Django/Django_cc.md#dynamic-template-files-using-dtl)

## Filters:
- When we need to modify variable before displaying we can use filters. Pipe `|` is used to apply filter.
- Syntax:- `{{variable | filter}}`
```html
{{name|upper}}
```
### Filter Properties:
1) Some of filters take arguments.
- Syntax:- `{{variable | filter : argument}}`
```
{{article|truncateword:40}}
```
2) Filter can be chained.
- Syntax:- `{{variable | filter | filter}}`
```html
{{article upper|truncateword:40}}                // Slice + ...
```
### Special Filters: 
1) **capfirst:** It capitalizes the first character of the value. If the first character is not a letter, this filter has no effect.
```html
{{value|capfirst}}
```

2) **default:** If value evaluates to False or an empty string (""), uses the given default. Otherwise, uses the value.
```html
{{ value|default:"nothing" }}
```

3) **length:** It returns the length of the value. This works for both strings and lists. The filter returns 0 for an undefined variable.
```html
{{ value|length }}
```

4) **upper:** It converts a string into all uppercase.
```html
{{value|upper}}
```

5) **lower:** It converts a string into all lowercase.
```html
{{ value|lower }}
```

6) **slice:** It returns only a stated amount of string
```html
{{value|slice = "n"}}         // if value = ishaan & n =2 , Output = is
```

7) **truncatechars:** It truncates a string if it is longer than the specified number of characters. Truncated strings will end with a translatable ellipsis character (" ..."). Argument: Number of characters to truncate to
```html
{{ value|truncatechars:7 }}
```

8) **truncatewords:** It truncates a string after a certain number of words. Newlines within the string will be removed. Argument: Number of words to truncate after
```html
{{value|truncatewords:2}}
```

9) **date:** It formats a date according to the given format.
```html
{{value|date:"D d M Y"}}
```

10)**time:** It formats a time according to the given format.
```html
{{value|time:"H:i""}
```
> Note: from datetime import datetime
[More Information about Date and Time]()
```
{{ value date:"SHORT DATE FORMAT" }}
{{ value time:"TIME FORMAT" }}
```
