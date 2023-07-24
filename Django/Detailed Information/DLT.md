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

> Note: from datetime import datetime
9) **date:** It formats a date according to the given format.
```html
{{value|date:"D d M Y"}}
```

10)**time:** It formats a time according to the given format.
```html
{{value|time:"H:i""}
```

[More Information about Date and Time](https://github.com/IshaanAdarsh/TIL/tree/main/Django/Detailed%20Information/TIme%26Date)

```python
# Shows Current Time
def learn_django(request) :
    d = datetime.now()
    return render (request, 'course/courseone.htmI', ('dt':dy)
{{ value date:"SHORT DATE FORMAT" }}
{{ value time:"TIME FORMAT" }}
```

11) **floatformat:**
- When used without an argument, rounds a floating-point number to one decimal place but only if there's a decimal part to be displayed. 
- If used with a numeric integer argument, floatformat rounds a number to that many decimal places. If no intergers are given its set at 1.
- If intereger = 0 -> round the float to the nearest integer.
- If the argument passed to floatformat is negative, it will round a number to that many decimal places but only if there's a decimal part to be displayed

```html
# value = 56.24321
{{value|floatformat:3}}              # Decimal till 3rd decimal place : 56.243

# value = 56.24321
{{value|floatformat:"-3"}}           # Decimal till 3rd decimal place : 56.243

# value = 56.00000
{{value|floatformat:"-3"}}           # 56
```

12) **if Tag:**
#### Variable:
- The (% if %) tag evaluates a variable, and if that variable is "true" (i.e. exists, is not empty, and is not a false boolean value).
- if tags may also use the operators == ;!=, <, >, <=, >=, in, not in, is, and is not
```html
# Syntax:-
{% if variable %}
    ........
{% endif %}

# Example: 
{% if nm and st %}                    # If both nm and st are true then the if statement is executed
    <h1> For Course {{nm}} {{st}} ; Seat Available</h1>
{% endif %}
```

#### Condition:
- Returns if the condition is true.
```html
# Syntax:
{% if condition %}
      .........
{% endif %}

# Example:
{% if nm == 'Django' or st == 5 %}
    <h1>{{nm}} Seat Available</h1>
{% endif %}
{% if not st == 5 %}
    </h1>Seat Not Available</h1>
{% endif %}
```

#### if Tag with filter
```html
# Syntax:-
{% if variable|filter %}
      ...........
{% endif %}

# Example:
{% if nm|length >= 6 %}
<h1>Hello {{nm}}</h1>
{% endif %}
```
## Dot Lookup
- Technically, when the template system encounters a dot, it tries the following lookups, in this order:
  - Dictionary lookup
  - Attribute or method lookup
  - Numeric index lookup

## For Loop:
- Simple for loop with the empty Tag.
```html
# Syntax:-
{% for variable in variables %}
      {{ variable }}
{% empty %}                            # Works only when a variable doesn't have a value
    Empty
{% endfor %}
Example:
<ul>
{% for stu in student %}
    <li> {{ stu }}</li>
{% endfor %}
```
- **Key, Value Pair using for loop:**
```html
# Syntax:-
{% for key, value in data.items %}
   {{ key }}: {{ value }}
{% endfor %}
```
<img width="780" alt="Predefined_for_loop" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/6b08c37d-e1d4-49cb-a03b-bec85e1bd6db">
