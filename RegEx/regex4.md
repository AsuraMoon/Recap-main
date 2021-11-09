# Regular Expressions - 4 - Capture and replace

## Theory

Let's get back to the replace function. Let's look at an example
```
I hate people named Robert, they are the worst! People named Norbert are okay though.
```

Let's say that we want to keep the names in the sentence, but get rid of the repetition `people named`:
```javascript
const pattern = /people named (\w+)/gi
const sentence = "I hate people named Robert, they are the worst! People named Norbert are okay though."

const newSentence = sentence.replace(pattern, '$1s') // I hate Roberts, they are the worst! Norberts are okay though.
```

The `$1` symbol refers to the first set of parentheses in the regex pattern.

We can go a bit further and extract a few more parts of the sentence.

```javascript
const pattern = /(04\d{2})(\d{2})(\d{2})(\d{2})/gi
const sentence = "Call me! 0467541237"

const newSentence = sentence.replace(pattern, '$1/$2.$3.$4') // Call me 0467/54.12.37!
```

### Visual example

![capture](capture.png)

In the following example we're going to work with the sentence:
```javascript
const sentence = "I have 3 cats, 2 dogs and 1 cow"
const pattern = /(\d) (\w{3}s?)/gi

// I have <em>3 cats</em>, <em>2 dogs</em> and <em>1 cow</em>
sentence.replace(pattern, '<em>$0</em>')

// I have <em>3</em>: cats, <em>2</em>: dogs and <em>1</em>: cow
sentence.replace(pattern, '<em>$1</em>: $2')

// I have cats33, dogs22 and cow11
sentence.replace(pattern, '$2$1$1')
```

### Replace with function

You can also access to your capturing parentheses with a function

```javascript
const sentence = "I have 3 cats, 2 dogs and 1 cow"
const pattern = /(\d) (\w{3}s?)/gi

// match == $0
// number == $1
// animal == $2
const replaceFunction = (match, number, animal) => {
  const times = parseInt(number)
  let replacement = ''

  for(i=0;i<times;i++){
    replacement += animal
  }

  return replacement
}

// I have catscatscats, dogsdogs and cow
sentence.replace(pattern, replaceFunction)
```

## Exercices

### Exercise 1

Create an HTML file, put the following text in a `<p>`aragraph.
- Write a regex to replace all the years in the following text between `<strong>` tags. (ex: `<strong>2009</strong>`).
- Write a regex to put the word before `illegal street racing` in red.
- Write a regex to underline any word that is 3 letters or less.


```
Fast & Furious (originally The Fast and the Furious) is a media franchise centered on a series of action films that are largely concerned with illegal street racing, heists and spies.

The first film was released in 2001, which began the original trilogy of films focused on illegal street racing, and culminated in the film The Fast and the Furious: Tokyo Drift (2006). The series went under a change with Fast & Furious (2009), which transitioned the series toward heists and spying, and was followed by four sequels. F9 is set to be released in 2021, with a tenth and eleventh film planned. The main films are collectively known as The Fast Saga.
```

### Exercice 2

In english, the word "fuck" is a rather common swear word. It is often used in combination with other letters to express an even deeper insult such as `fucking` or `motherfucker`

Write a single regex that catches all of these slurs and replace them by a word of stars of the same length.

ex: `motherfucker` (12 letters) becomes `************`

### Exercise 3

In css the `box-model` is a way to encode four values in a single property.

```
padding: top right bottom left
```

Write a regex that takes a css property (margin or padding), and rewrites every property using the full notation, for example:
```
padding : 5px 0 0 18px;
```

becomes

```
padding-top: 5px;
padding-right: 0;
padding-bottom: 0;
padding-left: 18px;
```

Units can be either `px`, `%`, `em`, `vh` or `vw` and there can be any amount of spaces between the properties and the name (ex: `padding  :    5px 0      0 7px`)