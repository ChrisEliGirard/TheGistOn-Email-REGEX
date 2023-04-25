# Using RegEx to Match an Email

This tutorial will get you up to speed on the basics you need to know as well as some bonuses in order to use and understand a regex expression that will match any instance of an email for you

## Summary

The Email Regex we will be going over is the following `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`. I will be explaining its components and how they work to match any string that is an email.

## Table of Contents

- [Using RegEx to Match an Email](#using-regex-to-match-an-email)
  - [Summary](#summary)
  - [Table of Contents](#table-of-contents)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [Grouping Constructs](#grouping-constructs)
    - [Bracket Expressions](#bracket-expressions)
    - [Character Classes](#character-classes)
    - [The OR Operator](#the-or-operator)
    - [Flags](#flags)
    - [Character Escapes](#character-escapes)
  - [Author](#author)

## Regex Components

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

### Anchors

Anchors in a Regex `Anchor` their attached regex match at specific positions. These positions can be before, after, and between characters or groups of characters. The `^ (caret)` character found at the start of the regex for the first match grouping `^([a-z0-9_\.-]+)` that appears before the `@` this specifically checks for a match in the position before the first character in the string which in this case would be the string that takes place before the `@` symbol. The `$ (Dollar Sign)` character found at the end of the string `([a-z\.]{2,6})$` anchoring itself right after the last character of the string and matching that character. Either will only make a match aslong as said character their anchored to meets their matching constraints which for the `^` in this case will only match any lowercase character a thorugh z, numbers 0 through 9, and special characters `_`, `.`, and `-`. so if the first character of the string was a `#` it would not match it as it does not meet the parameters required of the match. There are other components at play in each of these matches but we will go over those in the following sections for now understand that anchors will allow matching at the start and end of a string as well as between strings.

### Quantifiers

Quantifiers allow us to increase our match length much more easily than on a per character basis. ***By default Quantifiers will try and match the pattern match group as many times as possible***. Our Quantifier operands are `* multiplication or star character`, `+ addition character`, `? question character`, and `{} paired open and closed curly brackets characters`. We aren't using `*` and `?` with our regex but for your knowledge:
  - `*` Will match our pattern match group zero or more times
  - `?` Will match our pattern match group zero or one time
    - The `?` has double use by being able to apply it to any other operand including itself by placing it directly after the Quantifier you want to apply it to inorder make them match as few occurences as possible
  
Now back to our RegEx starting with the `+` Quantifier since it appears first in our expression. ***the `+` Quantifier will match the pattern one or more times***. So for our first Pattern Group `([a-z0-9_\.-]+)` will try and match anystring of characters that contain and only contain *Lowercase characters a thorugh z, Numbers 0 through 9, and special characters ``_``, ``.``, ``-``.* If it reaches any other character than those it will break the match before that character and normally check for more matches after. Our other Quantifier in this Regex is the `{}` Quantifier which has a couple of configurations.
 - `{ x(exact) }` Will match the pattern group an exact number of times given what number you supply for x
 - `{ x(min), }` The only change in Syntax is the comma must be included and Will match the pattern group at the minimum of x amount of times while assuming a max of infinite.
 - `{ x(min), y(max) }` Will match the pattern group at the minimum of x amount of times and maximum of y amount of times.
The `{}` Quantifier in our expression appears her `([a-z\.]{2,6})` setting a minimum of 2 matches and a maximum of 6 matches.

### Grouping Constructs

Grouping Constructs `() A pair of parenthesis` are what allow us to make this Regex to be more complex and check or match multiple sections of a string with different criteria for each. These Grouping Constructs are called subexpressions. Our Regex `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` has three groups.
1. ([a-z0-9_\.-]+)
2. ([\da-z\.-]+)
3. ([a-z\.]{2,6})

### Bracket Expressions

Bracket Expressions `[] a pair of Square Brackets` allow us to choose a range of characters to match. These are extremely customizeable allowing for a wide range of matches
- [abc] Will search for a string of characters that contains a, b, or c, regardless of the length of the string.
- [a-z] Will search for a string of characters that contains any letter in the alphabet
- [0-9] Will search for a string of characters that contains any numbers 0 through 9
- [_\.] Will search for a string of the special characters _ or . with the \ allowing us to use the period as a character and not its regex character class. 
- [a-d4-6_\.] These can be of any combination of any characters or special characters this particular bracket matching anything that contains the letters a, b, c, or d, the numbers 4, 5, or 6, and special characters _ and . of which the string does not have to meet all the requirements to be a match, i.e. it doesnt have to contain numbers as acdc_ would still be a match.

Our Regex has three Bracket Expressions one in every group:
1. [a-z0-9_\.-] Will match any string that has the letters a thorugh z, numbers 0-9, and special characters `_`, `.`, `-` - This will be to find the string before the `@` in an email address
2. [\da-z\.-] Will match any string that has the `\d (digits 0-9)`, letters a through z and special characters `.`, `-` - This will be used to find the string after the `@` in an email address
3. [a-z\.] Will match any string that has the letters a through z and special character `.` this is used to find the `.com` so to speak

### Character Classes

Character Classes allows us to use special characters that represent a predefined set of characters. The Character Classes were using in this regex are:
- `.` Which will match any character except the newline character \n
- `\d` Which will match any Numeric Character, can be used in place of `[0-9]`
We could have also used but didnt `\` which could be used in place of `[A-Za-z0-9_]` if we were trying to match capital letters in our regex this could have been used in the first group

There are more Character classes but I wont go into them here and they can be easily searched.

### The OR Operator

The Or Operator ` | ` allows us to look for different characters in a string so the following (a|b|c) would match for characters a or b or c

### Flags

Flags are placed outside the regex literal `/'s` These add optional functions and limits for the regex. Common flags are:
- `g (Global Search)` To test the regex against all potential matches strings
- `i (Case-insensitivivity)` To ignore case while matching a string
- `m (Multi-Line)` Input Strings that are multiple lines should be treated as multiple lines

### Character Escapes

Character Escapes were mentioned earlier as we used them to escape the period `.` character from its character class and be matched as just the period `.` character.

## Author

Written up by Christopher Girard a Junior Full-Stack Web Developer   

Github User: [ChrisEliGirard](https://github.com/ChrisEliGirard)    