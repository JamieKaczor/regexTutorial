# regexTutorial

This tutorial is to explain what a regular expression, or regex, is and how they are used in the world of coding.  Firstly, a regular expression is a sequence of symbols and characters expressing a string or pattern to be searched for within a longer piece of code.  Think of it as a heat seeking missile variant of Ctrl+F(or Command+F on a Mac).  Whereas the normal 'find' feature can be bland and one-note, by using regular expression, a programmer can widen the scope of a search, while also applying very defined filters.

## Summary

To demonstrate what this all means in practical terms, I will go through a sample regex used in matching an email, explaining each bit of code along the way.  We will be working off of this example:<br>
 `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

 ## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [Sample Regex](#sample-regex)
- [Resources Used](#resources-used)
- [Contact](#contact)

## Regex Components

Before we get to the meat of the regex, you'll notice it begins and ends in slash characters(`/`).  This is because regex is considered a literal, using a slash(`/`) at the beginning and at the end is one way for Javascript to create a regex object.

### Anchors

`^` and `$` are both anchors in regex.  They do not match any actual characters, but instead, match a position before or after characters.  The caret (`^`) corresponds to the beginning of the text, and the dollar sign (`$`) corresponds to the end of the text.  An example of what we mean here is as follows-<br>
`let example = 'RegularExpression';`<br>
`console.log(/^R/.test(example));`<br>
If you ran this bit of code you would see `true` printed to the console because R is the 1st letter after the `^` anchor in our example.  If you were to test this using the `$` anchor on a literal string make sure to position the final character before the `$`, not after it like we've shown in the above example, because remember, the `$` anchor means the end of the text, so it would be `/n$/` not `/$n/` or else it will always print out `false`.

### Quantifiers

Quantifiers specify how many instances of a character, group, or character class must be present in the input for a match to be found.  Quantifiers are considered 'greedy' by default, meaning they cause the regular expression engine to match as many occurrences of particular patterns as possible.  If we were to append our quantifier with a question mark (`?`) that would make it 'lazy', which causes matches to occur as few times as possible.  In our example regex under 'Summary', both plus signs (`+`) and `{2,6}` are quantifiers and they're all considered greedy. The pluses (`+`) match the previous token between one and unlimited times, as many times as possible, giving back as needed.  `{2,6}` matches the previous token between 2 and 6 times, as many times as possible, giving back as needed.

### Grouping Constructs

Grouping constructs break up regular expressions into smaller, more manageable pieces as they get larger and more complicated.  The primary way you group a section of a regex is by using parentheses (`()`). Each section within parentheses is known as a subexpression.  In our example you'll notice 3 completed sets of parentheses (`()`), that means this line of code can be broken down into three subexpressions.  Grouping constructs can also be a useful way for the user to identify what they're trying to find a match for even if they haven't previously been informed so long as they have a little knowledge of regex.  You'll notice in between the 1st and 2nd subexpression, there's an at sign (`@`) and in between the 2nd and 3rd theres a slash (`\`) followed by a dot (`.`).  `@` and `\.` are both literally the `@` sign and a `.`(the `.` being preceeded by the `\` makes it literal), so now we know we've got (Grouping 1)@(Grouping 2).(Grouping 3)...which looks an awful lot like the skeleton of an email address(which we already know we're trying to find).

### Bracket Expressions

A bracket expression is a list of characters enclosed by (`[`) and (`]`).  It matches any single character in that list.  If the first character in the list is the caret (`^`) it is telling us not to match the proceeding characters in that list.  For syntax, in most cases unless otherwise specified, `[abcd]` === `[a-d]`.  In our example in the 1st grouping of `([a-z0-9_\.-]+)`, bracket expression creates the character class of `[a-z0-9_\.-]`...this tells the search to look for any lowercase letter between a-z, any number between 0-9, and also the literal characters (`_`), (`.`), and (`-`).  In the second grouping the character `\d` is telling the search to match any digit equivalent to [0-9].

### Character Classes

Briefly mentioned under 'Bracket Expressions', character classes are simply a special notation that matches any symbol from a certain set.  Square brackets are used to specify character classes. Use a hyphen inside a character class to specify the characters' range.

### Flags

Flags affect regular expression searches.  There are none used in our example, but there are a few important ones to know that are used in JavaScript.<br>
`i`-means the search will be case insensitive: no difference between `a` and `A`.<br>
`g`-means the search will look for all matches, not just the first one.<br>
`m`-means a multi-line input string should be treated as multiple lines.

### Character Escapes

If you want to use any character as a literal in regex, you need to escape them with a backslash (`\`) so that 1\+1=2...otherwise something simple like 1+1=2 could result in an error message, or it can be read as something entirely different because `+` has its own special meaning in regular expression.

### Sample Regex

Now back to the sample regex we previously referenced.  I'll explain it in it's entirety in one place for easy reference.<br>
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`<br>
`^` asserts the position at the start of the string.  It is a meta escape.<br>
`([a-z0-9_\.-]+)` is the first grouping created by `(` and `)`, inside that, `[` and `]` is a bracket expression which creates a character class, inside that `a-z` matches a single character in the alphabetical range of a and z, `0-9` matches a single character in the numerical range of 0 and 9, `_` is a literal (_), `\.` is a literal (.) as the (\) means the next character is literal, and `-` is a literal -.  The `+` after the character class, but still before the end of group 1 is a quantifier which matches the previous token between one and unlimited times, as many times as possible, giving back as needed.<br>
`@` means it's a literal at sign @.<br>
`([\da-z\.-]+)` is the second grouping, refer to the first grouping to define this section.  The only new character is `\d`, which is a meta escape that matches a digit equivalent to [0-9].<br>
`\.` means it's a literal dot (.).<br>
`([a-z\.]{2,6})` is the third and final grouping, again, refer to the first grouping for definitions.  The only new character here is the `{2, 6}` quantifier, which matches the previous token between 2 and 6 times, as many times as possible, giving back as needed.<br>
`$` asserts the position at the end of the string.  It is a meta escape.

### Resources Used
- YouTube
- Google
- JavaScript: The Definitive Guide 7th Edition by David Flanagan

### Contact
If you have any questions, please refer to my Github page, [JamieKaczor](https://github.com/JamieKaczor), or contact me through my email, Dignanjk@aol.com