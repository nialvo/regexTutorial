## Summary

Javascript uses ECMA regular expressions (regex), which are essentially a search criterion for a string.<br>
In this tutorial, "regex" refers to an ECMA regex.<br>
A regex allows a a developer to search a string for a sequence of characters which matches the criterion defined by said regex.<br> 
There are several ways to implement regex in Javascript, depending on the purpose.<br>
A common use example is to verify input. For instance, to verify that an input has the format of  an email address, we could simply do: <br>
let email = input.match(/^\w+([\\.-]?\w+)*@\w+([\\.-]?\w+)*(\\.\w{2,3})+$/);<br>
if(email) return input;<br>
A regex criterion always begins and ends with "/".<br>
By default, a regex matches the first instance inside the string which matches the criterion, but regex can be used to search for all occurences., by using flags after the criterion.<br>

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

Anchors denote the beginning and end of a string.<br>
"^" marks the beginning and "\$" marks the end.<br>
/^x/ matches an "x" at the beginning of a string, /x$/ matches an "x" at the end of a string.<br>
In the email format verification given above, we have both: we want to make sure that the whole string corresponds to an email format, rather than simply verifying that the string contains an email but possibly other things in addition.<br>
Similar to anchors is the \b, signifying a word boundary. /\ba/ matches the second "a" in "sad actor".<br>
The opposite also exists: \B denotes a non-word boundary, that is the limit between two characters or two spaces:<br>
/\Ba/ matches the second "a" in "alligator".<br>

### Quantifiers

Quantifiers denote the quantity of a given character to match, by a value or range inside braces.<br>
/x{3}/ matches a substring composed of "xxx".<br>
/x{2,4}/ matches "xx", "xxx", and "xxxx".<br>
The upper bound is optional:<br>
/x{2,}/ matches "xx", "xxx", "xxxx", "xxxxx", etc.<br>
In our email example, we use {2,3} in (\\.\w{2,3})+$/) to match for 2 or 3 alphanumeric characters (\\w) between a period (\\.) and the end of the string (\$).<br>
This corresponds to all the email endings: .edu, .com, .co, .fr, .ru, etc.<br>



### Grouping Constructs
Parentheses are used to group together elements to apply an alternation or quantifier to whatever is within the parentheses.<br>
/gr(e|a)y/ will match "gray" and "grey".<br>
/r(at){3,}/ will match "ratatat", "ratatatat", "ratatatatat" etc.<br>
Groups are captured for future reference, this uses time and memory. If capture is not needed, we may include "?:" at the beginning.<br>
Thus our examples could be optimized to /gr(?:e|a)y/ and /r(?:at){3,}/.

### Bracket Expressions

Brackets allow us to specify a range of characters to match.<br>
/[abcde]/ matches any of those characters, it is equivalent in a sense to /a|b|c|d|e/.<br>
Another way to write this is /[a-e]/.<br>
We may combine the notations within a set of brackets.<br>
For example to match any character upper or lowercase from a to e or any integer from 1 to 4: /[a-eA-E1-4]/.<br>
We may also use brackets to specify characters by negative: /[^a-zA-Z]/ matches any character except a regular latin alphabet character.<br>

### Character Classes

"." matches any character except line terminators. Inside a character class, "." becomes simply the period.<br>
"\d" matches any arabic digit, equivalent to [0-9].<br>
"\D" matches any non-digit, equivalent to [^0-9].<br>
"\w" matches any alphanumeric character from the basic latin alphabet, equivalent to [a-zA-Z0-9].<br>
"\w" matches anything except an alphanumeric character from the basic latin alphabet, equivalent to [^a-zA-Z0-9].<br>
"\s" matches a single whitespace including space, tab, line feed, etc.<br>
"\S" matches anything except a whitespace.<br>
"\t" matches a horizontal tab.<br>
"\r" matches a carriage return.<br>
"\n" matches a linefeed.<br>
"\v" matches a vertical tab.<br>
"\f" matches a form-feed.<br>

There are more character classes, but these are probably beyond the scope of this tutorial:
"[\b]" matches a backspace, "\0"  matches a NUL character, "\cX" matches a control character using caret notation, where "X" is a letter from A–Z, etc.<br><br>
Maybe one of the more arcane character classes that the user will find of use is the "\p{UnicodeProperty}" or "\P{UnicodeProperty}" which match positively or negatively repectively a character based on Unicode properties, when seeking for example emoji or katakana or Han/Kanji.


### The OR Operator
"|" indicates that the elements on either side are both to be matched.<br>
/dog|cat/ will match both "dog" and "cat".<br>
/reali(s|z)e/ will match both "realise" and "realize".<br>

### Flags


Flags are added after the "/" ending the criterion. They specify search parameters.<br>

"d" 	generates indices for substring matches.<br> 	
"g" 	performs a global search, that is it matches all occurences matching the criterion rather than simply the first.<br>	
"i" 	makes the search case-insensitive.<br>
"m" 	performs a multi-line search. Practically speaking, this flag changes the interpretation of "^" and "$" anchors to mean beginning and end of line rather than beginning and end of string.<br>	
"s" 	allows "." to match newline characters.<br> 
"u" 	treats a pattern as a sequence of unicode code points.<br> 	
"y" 	performs a sticky search: it starts at the current position in the target string.<br>

### Character Escapes
"\\" serves two opposite purposes.<br>
For characters that are noramlly treated literally, the "\\" makes the character special. For instance "/d/" matches "d", but "/\d/" matches digits.<br>
Conversely, if a character is normally special, the "\\" makes it literal. For instance "/\\\\/" matches the character "\\".

## Author

I am a student at the UCI full stack coding bootcamp, I put this tutorial together drawing heavily on 
<a href='https://www.regular-expressions.info/tutorial.html'>regular-expressions.info</a> and 
<a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions'>Mozilla Regex Guide</a>.<br>
Please find me on Github at <a href='https://github.com/nialvo'>nialvo github</a>
