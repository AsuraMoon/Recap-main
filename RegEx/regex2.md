# Regular Expressions - 2 - Varying characters in pattern

## Theory

We merely scratched the surface of regex. Now that you know what is a pattern. Let's dive into more advanced stuff.

### The "OR" identifier

Let's say we want to validate someone's surname to be either:
- Théodore
- Théophile
- Théobald

They all start with the same 4 letters but end differently. Additionally this could be written with an `é` or an `e`. We could write:
```javascript
const pattern1 = /théodore/i
const pattern2 = /théophile/i
const pattern3 = /théobald/i
const pattern4 = /theodore/i
const pattern5 = /theophile/i
const pattern6 = /theobald/i

const sentence = "I really hate that guy, named Théodore!"

if(sentence.match(pattern1) || sentence.match(pattern2) || sentence.match(pattern3) || /* ... */){
  console.log('found')
}
```

But this is a bit redundant, regex provides a useful tool for that:
```javascript
const pattern = /th(é|e)o(dore|phile|bald)/i
const sentence = "I really hate that guy, named Théodore!"

if(sentence.match(pattern)){
  console.log('found')
}
```

Let's just go through another example:
```javascript
const pattern = /(i|you) (hate|love) (pizza|pasta|burritos|tacos)/i
const sentence = "I love Burritos"
const sentence2 = "You HATE tacos, bastard!"

if(sentence.match(pattern)){
  console.log('found')
}
if(sentence2.match(pattern)){
  console.log('found')
}
```

Without the `|` we would have to write 16 different condtions!

### Quantifiers

Quantifiers allow you to specify how many times you would like to find an occurence in a string. For instance let's say you want to validate that there is at least 3 `ha` in the string `hahahahahaha` but no more than 8 you could write :
```javascript
const pattern = /(ha){3,8}/i
const sentence = "hAhaHahAhaHa"

if(sentence.match(pattern)){
  console.log('found')
}
```

This can be useful to spot some ortographic difference among surnames. For example the french name `Thibault` could be written with or without an `l`:
```javascript
const pattern = /Thibau(l){0,1}t/i
const sentence = "my name is Thibault"

if(sentence.match(pattern)){
  console.log('found')
}
```

#### `+`, `*` and `?` quantifiers

In addition to the `{min,max}` syntax you can also use:
- `?` : to say the text between parenthesis can be written once or not at all
- `+` : to say the text between parenthesis needs to be written **AT LEAST once** (or more than once)
- `*` : to say the text between parenthesis cannot be written or can be written multiple times

In our previous example we could have written:
```javascript
const pattern = /Thibau(l)?t/i
const sentence = "my name is Thibault"

if(sentence.match(pattern)){
  console.log('found')
}
```

### Begining and end of string

You can specify that the pattern you're looking for is at the begining of the string using `^` . Example:
```javascript
const pattern = /^happy/i
const sentence = "I'm not happy!" // will NOT work because happy should be at the begining
```

Similarly you can specifythe end of a string using `$`:
```javascript
const pattern = /the end$/i
const sentence = "It was the end" // will work
const sentence2 = "The end is near!" // will NOT work
```


### Quick recap

| Name         | Symbol             | Description                                                                 |
|--------------|--------------------|-----------------------------------------------------------------------------|
| OR           | `/(A|B)/`          | The string must contain A or B                                              |
| Quantifier   | `/(AB){min, max}/` | The string must contain at least `min` occurence, and `max` occurence of AB |
| At least one | `/(AB)+/`          | The string must contain AB at least once (or more).                         |
| 0 or more    | `/(AB)*/`          | The string can contain AB multiple times or not at all                      |
| Optional     | `/(AB)?/`          | The string can contain AB once or not at all. (= `/(AB){0,1}/`)             |
| Start        | `/^AB/`            | The string should start with AB                                             |
| End          | `/AB$/`            | The string should end with AB                                               |
| Exact match  | `/^AB$/`           | The string should start with AB and only contain that                       |


## Exercises

### Exercise 1

In the following sentence replace every occurence of the word `clef`/`clé` (including plurals) by the emoji `🔑` with a single pattern.
```javascript
const sentence = `In french the word "key" used to be written "clef", but now it is written with an accent : "clé".
You might find medieval stories, such as the "clefs sanglantes de barbe bleue" and more recents ones "les clés du mystère"`
```

### Exercise 2

Write a regex pattern to validate that credit card number are well encrypted in the database. It can be encrypted with `X` or `Y` or `Z` and must be exactly 4 blocks of 4 chars. 

Example: `XXYX XYYY XXXX YYYY` is valid 

### Exercise 3

Write 2 regex patterns to verify that blog posts starts with a greetings that could be either:
- Hello
- Hi
- Hey
- Hej
- Greetings

And ends with at least 2 ending formulas:
- Thank you
- Thanks
- Merci
- Cheers 
- I am grateful


## Exercise 4

Write a regex to find out which message **only contains** laughing comments in English or Spanish. In Spanish laughing is expressed with `jaja` in english using `haha` or `lmao` (with at least one `o` but as many as you want, ex: `lmaoooooooooo`). Examples:
- `jajajaja` should work
- `lmaooooooooo` should work
- `ja` should **NOT** work
- `lma`  should **NOT** work
- `I said haha` should **NOT** work
