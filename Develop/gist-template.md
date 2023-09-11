# Regex Tutorial for HTML Tag

In this tutorial I will explain how matching an HTML tag regular expression functions by breaking down each part of the expressions and describe its function.

## Summary

A regular expression, often abbreviated as "regex" or "regexp," is tool for pattern matching and text manipulation. It's a sequence of characters that defines a search pattern. Regular expressions are used in various programming languages, text editors, and tools to search, match, and manipulate strings of text based on specific patterns or rules.

In this tutorial, we will look into a string of code for a Matching an HTML Tag.

Regex code as follow:
`/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

Anchors are characters within the regular expression that allow the user to match strings that begin with or ends with (or both) certain characters.

The `^` and `$` anchors ensure that the tag is matched from the beginning to the end of a line.

Let's break down the components of this regular expression and explain the anchors used:

1. `^`: This is the caret symbol, and it's called the "beginning of line" anchor. It asserts that the matched pattern should start at the beginning of a line.

2. `$`: This is the dollar sign symbol, and it's called the "end of line" anchor. It asserts that the matched pattern should end at the end of a line.

Now, let's break down the rest of the regular expression:

- `<([a-z]+)`: This part matches the opening tag. It starts with <, followed by capturing group ([a-z]+), which matches one or more lowercase letters (the tag name). The tag name is captured inside parentheses for later reference.

- `([^<]+)*`: This part matches any attributes or text content within the opening tag. [^<]+ matches one or more characters that are not <. The \* at the end allows for zero or more of these attribute/content segments.

- `(?:>(.*)<\/\1>|\s+\/>)`: This part captures the closing tag or self-closing tag. It's wrapped in a non-capturing group

To summarize, this regular expression is designed to match and capture HTML tags in a specific format, ensuring that they are properly opened and closed within the same line and correctly formatted.

### Quantifiers

Quantifiers in regular expressions are symbols or characters that specify the quantity or repetition of the preceding element in the pattern. They control how many times a character, group, or character class can appear in the matched text. Quantifiers are essential for specifying patterns that involve repetition.

The regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/` includes several quantifiers that control the repetition of characters or groups within the pattern. Let's break down the quantifiers used in this regex:

1. `*` (Asterisk): The asterisk quantifier matches zero or more occurrences of the preceding element. In this regex:

- `([^<]+)*` matches zero or more sequences of characters that are not `<`, effectively allowing for the matching of attributes or text content within an opening tag.

2. `+` (Plus): The plus quantifier matches one or more occurrences of the preceding element. In this regex:

- `([a-z]+)` matches one or more lowercase letters (the tag name), ensuring that a tag name must contain at least one lowercase letter.

- `\s+` matches one or more whitespace characters (used in the alternative pattern for self-closing tags), ensuring there is at least one whitespace character before the `/>`.

3. `?` (Question Mark): The question mark quantifier matches zero or one occurrence of the preceding element. In this regex:

- `(?:>(.*)<\/\1>|\s+\/>)` uses the `?` quantifier for the entire non-capturing group. This allows for an optional closing tag or self-closing tag. If a closing tag is present, it matches `>(.*)<\/\1>`, but if not, it matches `\s+\/>` (self-closing tag).

To summarize, these quantifiers provide flexibility in matching different parts of HTML tags:

- `*` allows for zero or more attributes or text content within an opening tag.
- `+` enforces that there must be at least one lowercase letter in the tag name and at least one whitespace character before a self-closing tag.
- `?` makes the closing tag or self-closing tag optional, allowing for both open and self-closed tags to be matched by the pattern.

### OR Operator

The OR operator in regular expressions is represented by the pipe symbol `|`. It allows you to specify multiple alternatives within a regular expression pattern. When using `|`, the regular expression engine will attempt to match any of the alternatives, and if one of them succeeds, the entire pattern is considered a match.

In the regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$`, the `|` symbol is used as the "OR" operator, denoting an alternation between two different patterns. It allows the regex to match one of two alternatives on the same input string. Let's break down the two alternatives:

1. `(?:>(.*)<\/\1>)`: This alternative matches an opening tag with content and a corresponding closing tag. Here's what it does:

- `>` matches the closing angle bracket of the opening tag.
- `(.*)` captures any content between the opening and closing tags. `.*` matches any character (except for newline) zero or more times, essentially matching the content.
- `<\/\1>` matches the corresponding closing tag using a backreference `\1` to the tag name captured in the opening tag.

2. `\s+\/>`: This alternative matches a self-closing tag. Here's what it does:

- `\s+` matches one or more whitespace characters (such as spaces or tabs).
- `\/>` matches the self-closing angle bracket `/>`.

Therefore, when the regex is applied to an input string, it will look for matches that satisfy either of these two alternatives:

- An opening tag with content and a corresponding closing tag.
- A self-closing tag.

This allows the regex to handle both types of HTML tag structures and capture the relevant parts as needed.

### Character Classes

Character classes in regular expressions (regex) are used to define a set or group of characters that can match a single character at a specific position in the text being searched or manipulated. They are enclosed in square brackets `[...]` and allow you to specify a list of characters, character ranges, or predefined character sets that the regular expression engine will match against.

In the regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, character classes are used to specify which characters are allowed in certain parts of an HTML tag. Let's break down how character classes are used in this regex:

1. `[a-z]+`: This character class matches one or more lowercase letters (a through z). It is used to match the tag name, ensuring that it consists of only lowercase letters.

2. `[^<]+`: This character class matches one or more characters that are not `<`. It is used to match any attributes or text content within the opening tag. Essentially, it allows for any characters except `<` to be present.

3. `\1`: This is not a character class but a backreference. It references the tag name captured in the opening tag. In the closing tag portion of the regex `(?:>(.*)<\/\1>)`, `\1` ensures that the closing tag matches the same tag name as the opening tag.

Here's a brief summary of how these character classes are used within the regex:

- `[a-z]+`: Matches the lowercase tag name (e.g., "div" in `<div>`).

- `[^<]+`: Matches attributes and text content within the opening tag.

- `\1`: Ensures that the closing tag matches the same tag name as the opening tag.

The regex provided is primarily designed to match and validate HTML tags in a specific format, ensuring that they are properly structured with lowercase tag names and optional attributes or text content.

### Flags

Flags, also known as modifiers or options, are additional settings that can be applied to regular expressions (regex) to modify their behavior during pattern matching and searching. Flags are typically appended to the end of a regex pattern and control various aspects of how the regex engine interprets and processes the pattern.

The regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/` doesn't have any flags specified within the regex pattern itself.

However if we are going to use flags, the syntax could be like this:
`/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/i`

Which included the "i" flag at the end of the regex pattern. The "i" flag makes the regex case-insensitive, meaning it will match both lowercase and uppercase letters. In this case, it allows the regex to match HTML tags with tag names in any combination of uppercase and lowercase letters.

### Grouping and Capturing

Grouping and capturing are important concepts in regular expressions (regex) that allow us to organize and extract specific portions of a matched pattern. They are achieved using parentheses `( )` in the regex pattern. Another word, Capturing groups are particularly useful when we want to extract specific parts of a matched pattern for further processing or validation, such as extracting data from a structured text document or parsing information from log files.

The regular expression `/^<([a-z]+)([^<]+)_(?:>(._)<\/\1>|\s+\/>)$/` is designed to match HTML tags and capture specific parts of those tags.

The break down the capturing groups within this regex:

1. `([a-z]+)`: This is the first capturing group and captures the tag name. It matches one or more lowercase letters (a to z) in the opening tag.

2. `([^<]+)`: This is the second capturing group, and it captures any attributes or text content within the opening tag. It matches one or more characters that are not `<`, ensuring that it doesn't extend beyond the opening tag.

3. `(?:>(.\*)<\/\1>|\s+\/>)`: This part of the regex contains a non-capturing group `(?:...)` with two alternatives, separated by the `|` (OR) operator:

- ``> (.\*)<\/\1>`: This is the third capturing group. It captures the content within the HTML tag when there is a matching closing tag. The `\1` is a backreference to the first capturing group, ensuring that the closing tag matches the same tag name as the opening tag.

- `\s+\/>`: This alternative matches self-closing tags. It does not use capturing groups because it is focused on identifying self-closing tags rather than capturing content within them.

In summary, this regex uses three capturing groups:

- The first group captures the tag name.
- The second group captures attributes or text content within the opening tag.
- The third group captures content within the HTML tag when a matching closing tag is present.

These capturing groups allow us to extract specific parts of HTML tags when using this regex for parsing or processing HTML code.

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

- Name: Christian Setiawan
- Github: https://github.com/csetiawan88
- Linkin: https://www.linkedin.com/in/christian-setiawan-1564081a3/
