# My friend named RegEx AKA Regular Expressions

✨ Here's a Regex tutorial that will help you understand the parts of an e-mail regex ✨

## Summary

A regular expression (shortened as regex or regexp) is a sequence of characters that specifies a search pattern in text. Regex is supported in all scripting languages (I.E. JavaScript, PHP, Python, etc.); as well as general purpose programming languages such as Java. This tutorial will explain how a specific regular expression, functions by breaking down each part or component i.e. #regex-components of the expression and describing what it does.

Programmers utilize regular expressions to navigate through text, test if the input of a program is functioning, and to check if end-users made errors. This example below is to verify the user's input as a valid e-mail address:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

Although it looks like some cryptic language from the dark realms, but we can break it down into parts:

- You can see letters, dots, underscores, digits, `%` signs and hyphens.
- We then encounter the `@` symbol which is followed by a series of letters, digits, and hyphens.
- Lastly, we get to a single `.` which is followed by two or more letters.
- If you haven't seen the pattern already, we just broke down the parts of an e-mail address, I.E: `firstName.lastName69@aol.com`

I will be walking you through this a little more in depth below--let's go!

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## User Story

```
AS A web development student
I WANT a tutorial explaining a specific regex
SO THAT I can understand the search pattern the regex defines
```

## Regex Components

### Anchors

We consider the characters `^` and `$` to be 'anchors'. An anchor is symbolized as `^` and signifies a string that starts with characters following it, we then get to the `$` anchor which ends with characters that precede it. Kind of like a burger with two pieces of buns on each end--`^` is the top bun and the `$` is the bottom bun 🍔. The contents in the middle make up the e-mail address!

Here's an example:

```
^[0-9]+$ -> Numeric string
in$  ->  ending with 'in'
^testing 123$ ->  Matches only one pattern

```

`\b` and `\B` are also considered position anchors. `\b` matches the boundary of a word, and `\B` matches the non-word-boundary. For example:

    \pizza\b --> matches the word "pizza" in the input string "I like pineapple on pizza.", but does not match the input "Show me some pizzaz!"

### Quantifiers

Quantifiers define the limits of the string that our regex matches. When we look at the subexpression `.([a-z\.]{2,6})` as shown in the Summary section. The `{2,6}` part is a quantifier that limits the minimum and maximum number of characters that your regex is looking for. It means this part of the string must be between 2 and 6 characters in length. As a default, a quantifier tells the engine to match as many occurrences of a particular pattern as possible. This behavior is called 'greedy'. The quantifiers include:

    +,*,? and {n}

Note: `{}`—Curly brackets can provide three different ways to set limits for a match: `{n}`, `{n,}` and `{n,m}`. There cannot be any space after the comma in {n,m}, otherwise it won't match correctly.

### Grouping Constructs

As regular expressions increase in complexity, it's important to use 'grouping constructs' to partition regex using () in order to match only a portion of the string at a time. In this case, the regex is divided by three different parts: `([a-z0-9_\.-]+)`, `([\da-z\.-]+)`, and `([a-z\.]{2,6})`. Each portion is also called as a 'subexpression'.

### Bracket Expressions

A bracket expression represents a list of characters enclosed by `[]`. Let's analyze the first bracket expression: `[a-z0-9_\.-]`. Instead of listing all characters, we use a range expression inside the bracket. `a-z` defines a range of lowercase letters from "a" through to "z", and `0-9` defines a range of numbers from "0" through "9". By the same token, if inside the brackets, there is `e-i`, it's the same as `[efghi]`. That would include "e", "f", "g", "h" or "i".

### Character Classes

A character class defines a set of characters that can appear in the input string for a successful match. For example: we have a phone number such as `+1(206)-987-6543` and we need to convert it to a ONLY numbers: `12069876543`. To do this, we can find and delete everything that is not a number. Character classes help with this. The most common character classes are as follows:

    \s ("s" comes from "space") ----->Space symbols: include spaces, newline \n, tabs \t, and other rare characters such as \v, \r and \f.
    \S - except \s.
    \d ("d" comes from "digit") -----> Numbers: Characters from 0 to 9.
    \D  -----> Non-digit.
    \w ("w" comes from "word") ----->"Latin letters or numbers or underscore '_'. Non-Latin letters (such as Cyrillic or Hindi) do not belong to \w.
    \W -----> except \w.
    . -----> any character with the 's' flag, otherwise any character except a newline \n.

Let's explore the "Number" class. Without the flag g, the regular expression looks only for the first match, which is the first digit \d. Let's add the flag g to find all numbers:

    let str = "+1(206)-987-6543";
    let regexp = /\d/g;
    alert( str.match(regexp) ); // array of matches: 1,9,1,1,1,2,3,4,5,6,7
    // let's make the digits-only phone number
    alert( str.match(regexp).join('') ); // 19111234567

### The OR Operator

`|` represents the OR operator. For example, we need to find a programming language: JavaScript, PHP, Java or HTML.

    let reg = /html|php|css|java(script)?/gi;
    let str = "First HTML appeared, then CSS, then JavaScript";
    alert( str.match(reg) ); // 'HTML', 'CSS', 'JavaScript'

### Flags

Also known as 'modifiers, flags in regular expressions are used to specify additional matching methods. Flags aren't written in the regular expression, but instead outside of the expression, with a format as follows:

    /pattern/flags

In JavaScript, there are 6 optional flags, but the most commonly used are below:

    i — Case-insensitive search, see the example below
    m — Multi-line search, see the example below
    g — Global search. Look back the phone number example above, I used 'g' to find all matches

Example 1. Find `DESPISE` in a string:

    let str = "I despise JavaScript!";
    alert( str.search(/DESPISE/) ); // -1（not found, because it's case sensitive by default）
    alert( str.search(/DESPISE/i) ); // 2

Example 2. Find `shoe` in a string:

    var str="shoegoogle\naskjeeves\nshoebing";
    var n1=str.match(/^shoe/g);   // one match
    var n2=str.match(/^shoe/gm); //multi-line matches

### Character Escapes

The backslash `\` in a regex escapes a character that otherwise would be interpreted literally. In order to use a special character as a regular character, we can precede it with a `\`. For example, we need to find a dot `.`. A dot in a regular expression refers to "any character except a newline", so if we want to actually express a query for a "dot", we can add a backslash before the dot.

    alert( "Chapter 8.9".match(/\d\.\d/) ); // 8.9

## Author

This Regular Expression (regex) tutorial created by [Andrew Tran](https://github.com/AndrewTranMSW). You can access the repo for this regex tutorial [here](https://github.com/AndrewTranMSW/regex-tutorial).
