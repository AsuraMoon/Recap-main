# Regular Expressions - 1 - The basics

## Theory

### The problem

Let's say you want to check if the word `furious` is present in the sentence `Fast and Furious`. Using the function [match()](), you'll have to write something like:

```javascript
const sentence = 'Fast and Furious'

if(sentence.match('furious')){
  console.log('match 1')
} // false, because Furious starts with a capital letter
else if(sentence.match('Furious')){
  console.log('match 2')
} // true
```

Or with the following sentence:
```javascript
const sentence = 'The movie "It", is called "Ça" in french'

if(sentence.match('ça')){
  console.log('match 1')
} // false, because "Ça" starts with a capital letter
else if(sentence.match('Ca')){
  console.log('match 2')
} // false, still wrong
else{
  console.log('no match')
}
```

How can we deal with this ?

### Creating patterns

Let's introduce a new concept. Let's say we are looking for a specific `pattern` in the sentence. We can write it like this:
```javascript
const pattern = /ça/i
const sentence = 'The movie "It", is called "Ça" in french'

if(sentence.match(pattern)){
  console.log('pattern found')
}
```

The text between `/ /` is called a **regular expression** or (**regex** in short). The letter `i` is a **flag**, the `i` stands for case **insensitive**, which means that it will work even if the text is in capital letters.

![aNotHeR onE](https://media.giphy.com/media/VgqQhscr0X22jfxU6w/giphy.gif)

```javascript
const pattern = /fast and furious/i
const sentence = 'fAsT aNd FurIoUS!'

if(sentence.match(pattern)){
  console.log('pattern found')
}
```


### The replace function

So we now have a basic idea of what the `match()` function does. But you can also use regular expression to search and [replace](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace) patterns in text.

A basic example:

```javascript
const pattern = /fast/i
const sentence = 'fAsT aNd FurIoUS!'
const newSentence = sentence.replace(pattern, 'quick')

console.log(newSentence) // quick aNd FurIoUS!
```

### Flags

We've already seen a flag `i` at the end of the regex, which allows us to do case insensitive search. There is another one called `g` for **global**, this allows us to replace every occurence of the pattern.

**Without** the `g` flag...

```javascript
const pattern = /al/i
const sentence = 'Albert loves algebra'
const newSentence = sentence.replace(pattern, 'hu')

console.log(newSentence) // hubert loves algebra
```

**With** the `g` flag...
```javascript
const pattern = /al/gi
const sentence = 'Albert loves algebra'
const newSentence = sentence.replace(pattern, 'hu')

console.log(newSentence) // hubert loves hugebra
```


There are other handy flags. By default, the regex does not work on multiline text. Adding the `m` flag will allow the regex to work on the whole text, even if there are multiple lines.

```javascript
const pattern = /ça/im
const multilineSentence = `
A DIALOG:
--------
Mike asked, how do you say "It" in french?
Jean-Pascal replied: "Ça"!`

if(sentence.match(pattern)){
  console.log('pattern found')
}
```


| Flag | Usage            |
|------|------------------|
| `i`  | Case insensitive |
| `g`  | Global           |
| `m`  | Multiline        |

## Variable pattern

There is another way to write regular expressions. The following method is less efficient performance-wise, so only use it if you need to have a variable pattern (for example if you need to create a pattern from a user-input).

```javascript
// These two methods do the same thing :
const pattern = /fast/gi
const pattern = new RegExp('fast', 'gi')
```

An example is worth a thousand words:
```javascript
const sentence = 'fAsT and fUrious'
const userInput = document.createElement('input')
userInput.type = 'text'
userInput.addEventListener('keyup', (e) => {
  const inputValue = e.target.value
  const pattern = new RegExp(inputValue, 'gi')

  if(sentence.match(pattern)){
    console.log('found: "'+ e.target.value +'" in '+ sentence)
  }
})
```

That's it, for now...


## Exercices

### Exercise 1

Write a regular expression to replace every occurence of `Emily` with `Kelian` in the following constant.

```javascript
const text = `Emily is probably the best coach I've ever had. I'm an absolute fan of Emily's exercices on regular expressions. 
I wouldn't be as fluent in JavaScript if I had not crossed Emily's path`
```

### Exercise 2

Replace every occurence of the word `god` (with a lower g) with the word `deity`, the word `God` (with a capital letter) should be left untouched!
```javascript
const text = `In ancient Egypt a god was an entity with the head of an animal and a human body. An egyptian god is not to be mistaken with the God that is worshipped in churches and mosque around the globe these days! God is not a god!`
```

### Exercise 3

Use the text from exercise two and split it into an array of words (using [`split(' ')`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split)). Create a text input, listen for `keyup` events and return an array of words that matches the value entered in the input using a **case insensitive** pattern.

For example: if I enter `eg` in the input, the array should contain `['Egypt', 'egyptian']`

### Bonus exercise

Go back to the [collection project](../../../The%20Field/5.leaving_the_field) you made a few days ago and add some filtering to the display with your new skills!