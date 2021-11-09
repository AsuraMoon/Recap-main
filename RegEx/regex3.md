# Regular Expressions - 3 - Character classes

## Theory

### Ranges

What if you want to check if a string contains **any number** at least once? You could write:
```javascript
const pattern = /(0|1|2|3|4|5|6|7|8|9)?/
```

But this is a bit long. Instead we could use ranges. For instance if we'd like to check if there is **at least one number between 0 and 9**, we could write:
```javascript
const pattern = /[O-9]?/
```

And if we want to check if there are exactly **6 numbers between 1 and 5** ?
```javascript
const pattern = /[1-5]{6}/
```

Ranges also work with letters:
```javascript
const pattern1 = /[a-z]{1, 3}/ // any word of 1 to 3 letters from a to z (lowercase)
const pattern2 = /[A-Z]{1, 3}/ // any word of 1 to 3 letters from A to Z (uppercase)
```

You can combine ranges and regular search patterns:
```javascript
const pattern = /^playstation( [2-5])?$/i // matches playstation, playstation 2, playstation 3, playstation 4, playstation 5
```

### Not in range

You can also use ranges to specify characters that should not pass the test, using `[^]`. 
```javascript
const pattern = /^([^a-d]{5} ){3}$/i // 3 words of 5 letters, except a, b, c, d
```

### Meta sequences

Ranges are really useful, but if you want to be more general there are some available shorthands.

| Symbol | Range equivalent | Description   |
|--------|------------------|---------------|
| `/./`     | n/a               | Any possible character (every letter, number, punctuation, emojis, ...) |
| `/\s/`     | n/a               | Any spacing character (whitespace, tab, ...)* |
| `/\S/`     | n/a               | Any **non**-spacing character (the opposite of \s) |
| `/\d/`     | `[0-9]`               | Any number |
| `/\D/`     | `[^0-9]`               | Not a number (the opposite of \d) |
| `/\w/`     | `[a-zA-Z0-9_]`               | Any letter or number (and `_`) |
| `/\W/`     | `[^a-zA-Z0-9_]`               | Not a letter, or number or `_` (opposite of \w) |
| `/\n/`     | n/a               | New line |
| `/\t/`     | n/a               | Tab |

__*__ : When using the `m` flag (`/regex/m`, multiline mode) also includes newline.

For example if I want to check if a sentence contains 3 words of at least 3 characters I could write:
```javascript
const pattern = /^(\w{3,} ){3}$/i // 3 words
```


### Escaping characters

Since regex use a lot of special characters (`+`, `?`, etc), we need a way to still be able to use them.

The trick is simple, if I want to check if there is a question mark (`?`), i just need to put a backslash (`\`) in front of it. This is called **escaping**. 
```javascript
const pattern = /\.$/i // Checks if the sentence ends with a .
```

## Exercises

### Exercise 1

Create a regular expression that validates if the sentence is a question. A question starts with :
- What
- Why
- How
- When
- Who

and ends with a question mark `?`. It should have at least 3 words.

Examples:
- `Why am I ugly?` valid
- `How do you make babies?` valid
- `What the fuck` **NOT** valid (no question mark)
- `Who?` **NOT** valid (single word)

### Exercise 2

Validate a credit card number. A credit card number is in the form of 4 group of 4 numbers separated by a space.

Examples:
- `3567 2587 1212 9978` valid
- `A123 GG78 9017 1245` **NOT** valid (contains letters)
- `1113 14` **NOT** valid (too short)
- `3567 2587 1212 9978 9096` **NOT** valid (too long)

### Exercise 3

Create a function (multiple patterns) to validate a password. The password should:
- Contain at least 1 lowercase letter
- Contain at least 1 uppercase letter
- Contain at least 1 number
- Contain a special character (`+`, `?`, `$`, `^`)
- Be between 8 and 18 characters long

### Exercise 4 : BeKnit

The following picture is a mockup a future project called **BeKnit**, a 7 months bootcamp to become a professional at knitting. You have to create the frontend of their registration form.

![beknit mockup](beknit/wf.png)

Each field has to be validated once it is completed using the `change` event. The conditions are listed below:
![requirements](beknit/requirements.png)

If the field has been validated, the progression on the side gets completed, if it does not pass the validation an error is displayed below the field.
![example](beknit/example.png)

The page has to be centered vertically and horizontally!

Good luck, in knit we trust!
