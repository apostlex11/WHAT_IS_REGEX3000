# Matching an Email & PhoneNumber Regex.exec()

Regex or Regular Expressions is a method of identifying and describing,
patterns in a string of data. Which after they form a small language on their own.
They are used in lots of programming languages, such as JavaScript, Python, PHP, and more! We will dive in on a singular Regex, Regex.exec(). By the end of this tutorial you will fully understand how it works and why we use it.

## Summary

Regex.exec() is a method used in JavaScript to search a string for a pattern and returns an array of data or none (null) if there are no data to be found. This method is called on by a regular expression object that takes a string as the argument. It will search the string for the first occurence of the pattern defined by the Regex. It will then return the containing data about the match. The data contained in the array includes the matched text, the index of that matched text is the original string, and any capturing groups that were used in the Regex.

Regex is often used to check a string of characters such as passwords, emails, and phone numbers. They look for a pattern to see if they match the pattern defined by the Regex and return accessible data. We will be using this as an example to dive deeper into how this method works.


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
CODE EXAMPLE

const str = "My email address is john.doe@example.com and my phone number is +1 (555)               123-4567";

const emailRegex = /\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z]{2,}\b/gi;
const phoneRegex = /\+?\d{1,3}[-.\s]?\(?(\d{3})\)?[-.\s]?(\d{3})[-.\s]?(\d{4})/g;

let match;
while ((match = emailRegex.exec(str)) !== null) {
  console.log(`Email found: ${match[0]}`);
}

while ((match = phoneRegex.exec(str)) !== null) {
  console.log(`Phone number found: ${match[0]}, area code: ${match[1]}, number: ${match[2]}-${match[3]}`);
}

In this example, we have a string that contains an email address and a phone number. We want to extract the email address and the phone number separately using regular expressions.

We define two regular expressions: 'emailRegex' to match email addresses and 'phoneRegex' to match phone numbers. The email regex pattern is a complex combination of characters to match valid email addresses. The phone regex pattern matches phone numbers in different formats with optional country code.

We then use a 'while' loop with the 'exec()' method to search for all occurrences of the email and phone patterns in the string 'str'. The loop continues as long as 
'exec()' returns a non-null value. Each time the loop runs, it extracts the next match and logs it to the console.

For the email regex, we simply log the entire match using 'match[0]'. For the phone regex, we extract the area code and the phone number separately from the match array and log them in a formatted string.

This example demonstrates how 'regex.exec()' can be used in a loop to find multiple occurrences of a pattern in a string and extract specific information from each match.


### Anchors
Anchors are special characters in a regular expression that match specific positions in a string, rather than matching any character.

Commonly used anchors in regular expressions:
'^' - The caret symbol is an anchor that matches the start of a string.
'$' - The dollar sign symbol is an anchor that matches the end of a string.
'\b' - The word boundary anchor matches the position between a word character and a non-word character.

In the example code, the regular expressions do not use any anchors to match specific positions in the string. Instead, they use specific patterns to match email addresses and phone numbers in any position within the string.

However, if we wanted to use anchors in the regular expressions, we could modify them to match email addresses or phone numbers that only appear at the beginning or end of a string, or that are surrounded by specific characters. For example, we could modify the email regex to match only email addresses at the beginning of a line, like this:

EXAMPLE
const emailRegex = /^[\w.%+-]+@[A-Za-z0-9.-]+\.[A-Z]{2,}$/gim;

In this modified regex, the '^' anchor matches the start of a line, and the '$' anchor matches the end of a line. The 'm' flag is also used to enable multi-line mode, allowing the regex to match email addresses that appear at the start of any line in the input string.


### Quantifiers
Quantifiers are special characters in regular expressions that specify the number of times a character or group should be matched. Here are some commonly used quantifiers:

'*' - The asterisk symbol is a quantifier that matches zero or more occurrences of the preceding character or group.
'+' - The plus symbol is a quantifier that matches one or more occurrences of the preceding character or group.
'?' - The question mark symbol is a quantifier that matches zero or one occurrence of the preceding character or group.
'{n}' - Curly braces are used to specify an exact number of occurrences to match. For example, '{3}' matches exactly three occurrences.
'{n,}' - Curly braces with a comma are used to specify a minimum number of occurrences to match. For example, '{3,}' matches three or more occurrences.
'{n,m}' - Curly braces with two comma-separated values are used to specify a range of occurrences to match. For example, '{3,5}' matches between three and five occurrences.
In the example code I provided earlier, both regular expressions use quantifiers to match specific patterns in the input string. For example, the email regex uses 
'[\w.%+-]+' to match one or more occurrences of word characters, periods, percent signs, plus signs, or hyphens. The phone regex uses '\d{1,3}' to match one to three occurrences of digits.

Quantifiers are useful in regular expressions to match repeating patterns of characters, making it easier to match complex strings.


### Grouping Constructs
Grouping constructs are used in regular expressions to group multiple characters or sub-patterns together, so that they can be treated as a single unit. This allows us to apply quantifiers and other modifiers to the group as a whole, rather than to individual characters.

Here are some commonly used grouping constructs in regular expressions:

'( )' - Parentheses are used to group characters or sub-patterns together.
'(?: )' - Non-capturing parentheses are used to group characters or sub-patterns together without creating a capture group.
'(?= )' - Positive lookahead is used to match a pattern only if it is followed by another pattern.
'(?! )' - Negative lookahead is used to match a pattern only if it is not followed by another pattern.
In the example code I provided earlier, the phone number regex uses grouping constructs to capture the area code and phone number separately:

EXAMPLE
const phoneRegex = /\+?\d{1,3}[-.\s]?\(?(\d{3})\)?[-.\s]?(\d{3})[-.\s]?(\d{4})/g;

In this regex, the area code is captured using the parentheses '(\d{3})', which groups three consecutive digits together. The phone number is also captured using parentheses '(\d{3})' and '(\d{4})', which group the next three digits and four digits together, respectively. These groups can then be accessed using the 'match' array, as shown in the previous example.

Grouping constructs are useful in regular expressions when we want to match or capture multiple patterns that occur together, or when we want to apply quantifiers or modifiers to a specific group of characters.


### Bracket Expressions
Bracket expressions, also known as character classes, are used in regular expressions to match any one character within a set of characters. Bracket expressions are enclosed in square brackets, and any character within the brackets will be matched. Here are some examples of bracket expressions:

'[abc]' - Matches any one of the characters a, b, or c.
'[a-z]' - Matches any one lowercase letter from a to z.
'[A-Z]' - Matches any one uppercase letter from A to Z.
'[0-9]' - Matches any one digit from 0 to 9.
'[^abc]' - Matches any one character that is not a, b, or c.
We can also use shorthand character classes in bracket expressions to match common types of characters, such as:

'\d' - Matches any one digit character.
'\w' - Matches any one word character (letter, digit, or underscore).
'\s' - Matches any one whitespace character (space, tab, or newline).
'.' - Matches any one character except newline.
In the example code I provided earlier, both the email regex and the phone number regex use bracket expressions to match specific patterns in the input string. For example, the email regex uses '[A-Za-z0-9._%+-]' to match any one letter, digit, or special character that is commonly found in email addresses. The phone regex uses 
'[-.\s]' to match any one of the characters '-', '.', or space.

Bracket expressions are useful in regular expressions when we want to match any one character within a specific set of characters, or when we want to match a specific type of character (such as digits or whitespace).


### Character Classes
Character classes, also known as shorthand character classes, are shorthand representations of common bracket expressions. They are used in regular expressions to match a specific type of character, such as a digit or a whitespace character. Here are some commonly used character classes:

'\d' - Matches any digit character (equivalent to '[0-9]'
'\D' - Matches any non-digit character (equivalent to '[^0-9]'
'\w' - Matches any word character (equivalent to '[A-Za-z0-9_]'
'\W' - Matches any non-word character (equivalent to '[^A-Za-z0-9_]'
'\s' - Matches any whitespace character (equivalent to '[ \t\n\r\f]'
'\S' - Matches any non-whitespace character (equivalent to '[^ \t\n\r\f]'
'.' - Matches any character except newline.
In the example code I provided earlier, both the email regex and the phone number regex use character classes to match specific types of characters in the input string. For example, the email regex uses '\w' to match any word character (letter, digit, or underscore) in the username and domain parts of the email address. The phone regex uses '\d' to match any digit character in the area code and phone number.

Character classes are useful in regular expressions when we want to match a specific type of character, without having to specify each individual character in a bracket expression. They can help make regular expressions shorter and more readable.


### The OR Operator
The OR operator in regular expressions is represented by the vertical bar ('|') character. It is used to match either one pattern or another pattern, and is similar to the logical OR operator in programming languages.

For example, the regular expression '/apple|orange/' would match either the string "apple" or the string "orange". If we applied this regular expression to the input string "I like apples and oranges", it would match both "apple" and "orange".

We can also use the OR operator in combination with other regular expression constructs, such as character classes, quantifiers, and grouping constructs. Here are some examples:

'[a-z]|[\d+]' - Matches any lowercase letter from a to z, or the plus symbol (+).
'(apple|orange)+' - Matches one or more occurrences of the strings "apple" or "orange".
'\d{3}|[A-Za-z]{2}' - Matches either three consecutive digits, or two consecutive letters (either uppercase or lowercase).
The OR operator is useful in regular expressions when we want to match one pattern or another pattern, without having to write separate regular expressions for each pattern. It can help make regular expressions shorter and more concise.


### Flags
Flags in regular expressions are used to modify how the regular expression behaves. They are placed after the closing forward slash of the regular expression, and are represented by a single letter.

Here are some commonly used flags:

'i' - Case-insensitive matching. When this flag is used, the regular expression will match both uppercase and lowercase letters.
'g' - Global matching. When this flag is used, the regular expression will match all occurrences of the pattern in the input string, instead of just the first occurrence.
'm' - Multiline matching. When this flag is used, the regular expression will treat the input string as multiple lines, and the '^' and '$' anchors will match the beginning and end of each line, instead of just the beginning and end of the entire string.
's' - Single-line matching. When this flag is used, the regular expression will treat the input string as a single line, and the '.' character will match newline characters as well.
'u' - Unicode matching. When this flag is used, the regular expression will use Unicode rules to match characters, instead of just ASCII rules.
To use a flag in a regular expression, simply add it after the closing forward slash of the regular expression. For example, the regular expression '/hello/i' would match both "hello" and "Hello", because the 'i' flag makes the matching case-insensitive.

Flags are useful in regular expressions when we want to modify how the regular expression behaves, such as making it case-insensitive or global. They can help make regular expressions more flexible and powerful.


### Character Escapes
In regular expressions, a backslash ('\') is used as an escape character to represent special characters that have a special meaning in regular expressions. For example, the period ('.') is a special character that matches any character except newline. If we want to match a literal period character, we can escape it with a backslash: '\.'.

Commonly used Character Escapes:

'\\' - Matches a literal backslash character.
'\.' - Matches a literal period character.
'\d' - Matches any digit character equivalent to '[0-9]'
'\D' - Matches any non-digit character equivalent to '[^0-9]'
'\w' - Matches any word character equivalent to '[A-Za-z0-9_]'
'\W' - Matches any non-word character equivalent to '[^A-Za-z0-9_]'
'\s' - Matches any whitespace character equivalent to '[ \t\n\r\f]'
'\S' - Matches any non-whitespace character equivalent to '[^ \t\n\r\f]'

We can also use backslashes to escape special characters in regular expressions, such as the OR operator ('|') or the opening and closing brackets ('[' and ']').

For example, if we want to match the string "hello|world", we need to escape the vertical bar character with a backslash: 'hello\|world'

Character escapes are useful in regular expressions when we want to match literal special characters that have a special meaning in regular expressions, or when we want to escape special characters in regular expressions. They can help make regular expressions more precise and accurate.

## Author

Soon to be Software Developer, inspired by the technology advancement. Learning more everyday, realizing knowledge is endless...

https://github.com/apostlex11
