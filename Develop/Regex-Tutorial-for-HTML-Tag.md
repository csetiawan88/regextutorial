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

Here are the break down of this regular expression and explain the anchors used.

1. `^`: This is the caret symbol, and it's called the "beginning of line" anchor. It asserts that the matched pattern should start at the beginning of a line.

2. `$`: This is the dollar sign symbol, and it's called the "end of line" anchor. It asserts that the matched pattern should end at the end of a line.

Now, here are the break down for the rest of the regular expression:

- `<([a-z]+)`: This part matches the opening tag. It starts with `<`, followed by capturing group `([a-z]+)`, which matches one or more lowercase letters (the tag name). The tag name is captured inside parentheses for later reference.

- `([^<]+)*`: This part matches any attributes or text content within the opening tag. `[^<]+` matches one or more characters that are not `<`. The `\*` at the end allows for zero or more of these attribute/content segments.

- `(?:>(.*)<\/\1>|\s+\/>)`: This part captures the closing tag or self-closing tag. It's wrapped in a non-capturing group

In conclusion, this regular expression is designed to match and capture HTML tags in a specific format, ensuring that they are properly opened and closed within the same line and correctly formatted.

### Quantifiers

Quantifiers in regular expressions are symbols or characters that specify the quantity or repetition of the preceding element in the pattern. They control how many times a character, group, or character class can appear in the matched text. Quantifiers are essential for specifying patterns that involve repetition.

The regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/` includes several quantifiers that control the repetition of characters or groups within the pattern.

Here are the break down for the quantifiers used in this regex:

1. `*` (Asterisk): The asterisk quantifier matches zero or more occurrences of the preceding element. In this regex:

- `([^<]+)*` matches zero or more sequences of characters that are not `<`, effectively allowing for the matching of attributes or text content within an opening tag.

2. `+` (Plus): The plus quantifier matches one or more occurrences of the preceding element. In this regex:

- `([a-z]+)` matches one or more lowercase letters (the tag name), ensuring that a tag name must contain at least one lowercase letter.

- `\s+` matches one or more whitespace characters (used in the alternative pattern for self-closing tags), ensuring there is at least one whitespace character before the `/>`.

3. `?` (Question Mark): The question mark quantifier matches zero or one occurrence of the preceding element. In this regex:

- `(?:>(.*)<\/\1>|\s+\/>)` uses the `?` quantifier for the entire non-capturing group. This allows for an optional closing tag or self-closing tag. If a closing tag is present, it matches `>(.*)<\/\1>`, but if not, it matches `\s+\/>` (self-closing tag).

In conclusion, these quantifiers provide flexibility in matching different parts of HTML tags:

- `*` allows for zero or more attributes or text content within an opening tag.
- `+` enforces that there must be at least one lowercase letter in the tag name and at least one whitespace character before a self-closing tag.
- `?` makes the closing tag or self-closing tag optional, allowing for both open and self-closed tags to be matched by the pattern.

### OR Operator

The OR operator in regular expressions is represented by the pipe symbol `|`. It allows you to specify multiple alternatives within a regular expression pattern. When using `|`, the regular expression engine will attempt to match any of the alternatives, and if one of them succeeds, the entire pattern is considered a match.

In the regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$`, the `|` symbol is used as the "OR" operator, denoting an alternation between two different patterns. It allows the regex to match one of two alternatives on the same input string.

Here are the break down for two alternatives:

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

Character classes in regular expressions (regex) are used to define a set or group of characters that can match a single character at a specific position in the text being searched or manipulated. They are enclosed in square brackets `[...]` and allow user to specify a list of characters, character ranges, or predefined character sets that the regular expression engine will match against.

In the regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, character classes are used to specify which characters are allowed in certain parts of an HTML tag.

Here are break down on how character classes are used in this regex:

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

Grouping and capturing are important concepts in regular expressions (regex) that allow user to organize and extract specific portions of a matched pattern. They are achieved using parentheses `( )` in the regex pattern. Another word, Capturing groups are particularly useful when we want to extract specific parts of a matched pattern for further processing or validation, such as extracting data from a structured text document or parsing information from log files.

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

In regular expressions, a bracket expression, also known as a character class, is a way to specify a set of characters that can match a single character at a specific position in the text being searched or manipulated. Bracket expressions are enclosed in square brackets `[...]` and allow us to define a list of characters, character ranges, or predefined character sets that the regular expression engine will attempt to match.

Bracket expressions are a very useful feature in regular expressions and are commonly used to create patterns that match specific sets of characters or types of characters within text. It provide flexibility in defining what we want to match or capture in regex patterns.

In the regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, bracket expressions (character classes) are used within the square brackets `[a-z]` to specify a range of characters that can match a lowercase letter. Specifically, `[a-z]` matches any single lowercase letter from 'a' to 'z'.

Here's how `[a-z]` is used in the regex pattern:

`[a-z]`: This character class matches a single lowercase letter from 'a' to 'z'. It is used in the regex to ensure that the tag name (e.g., "div" in `<div>`) consists of only lowercase letters.

In the context of the provided regex, `[a-z]+` is used to capture and match the tag name within an HTML opening tag. It ensures that the tag name is composed entirely of lowercase letters. For example, if the input is `<div>`, `[a-z]+` would match and capture "div" as the tag name.

The regex as a whole is designed to match and validate HTML tags in a specific format, ensuring that they are properly structured with lowercase tag names and optional attributes or text content.

### Greedy and Lazy Match

In regular expressions, "greedy" and "lazy" refer to two different approaches for quantifiers, which control how many times a particular element or group in the regex pattern is matched. Quantifiers specify the number of times a character or group should be matched, and they can be modified to exhibit either greedy or lazy behavior.

In the regular expression `/^<([a-z]+)([^<]+)_(?:>(._)<\/\1>|\s+\/>)$/`, both greedy and lazy quantifiers are used in different parts of the regex.

1. Lazy Quantifiers:

`(.*?)`: This part of the regex uses a lazy (non-greedy) quantifier `*?`. It's part of the capturing group `( ... )` that captures the content within HTML tags when there is a matching closing tag. The `*?` quantifier tries to match as few characters as possible while still allowing the rest of the pattern to match.

2. Greedy Quantifiers:

`([a-z]+)`: This capturing group uses `+` without a lazy quantifier, making it greedy. It matches one or more lowercase letters (a to z) in the opening tag. Greediness ensures that it captures as many characters as possible while still allowing the pattern to match.

`([^<]+)`: This capturing group also uses `+` without a lazy quantifier, making it greedy. It captures any attributes or text content within the opening tag, ensuring that it captures as many characters as possible before the next part of the pattern.

The use of greedy quantifiers in the regex is appropriate because they help capture the maximum amount of content within HTML tags while still ensuring that the overall pattern matches correctly.

So, in summary, the regex `/^<([a-z]+)([^<]+)_(?:>(._)<\/\1>|\s+\/>)$/` predominantly uses greedy quantifiers in capturing groups but employs a lazy quantifier within the content-capturing group to match the content within HTML tags as efficiently as possible.

### Boundaries

In regular expressions, boundaries are used to define specific positions within the text where a match should occur. They don't match any characters themselves but specify conditions for where a match can start or end. Boundaries are essential for matching text patterns in a precise and controlled way.

Some examples of boundaries:

1. Line Anchors `m` (Multiline)
2. Start of Line (^)
3. End of Line ($)
4. Word Start (\B)
5. Non-Word Boundary (\B)
6. Word Boundaries (\b)

In the regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, there are no explicit boundary assertions like `\b`, `^`, or `$`.

### Back-references

Back-references in regular expressions are a mechanism that allows user to refer back to and match the same text that was previously captured by a capturing group within the same regex pattern. They are useful for matching repeated or duplicated text and for ensuring that certain parts of a text are repeated consistently.

In the regular expression `/^<([a-z]+)([^<]+)_(?:>(._)<\/\1>|\s+\/>)$/`, back-references are used within the pattern to ensure that the opening and closing HTML tags match each other. Specifically, the back-reference `\1` is used.

1. `\1`: This is the back-reference used in the pattern. It refers back to the text captured by the first capturing group, which is `([a-z]+)`. In this regex, the first capturing group captures the tag name.

2. `<\/\1>`: This part of the pattern uses the back-reference `\1`. It matches the closing HTML tag and ensures that the closing tag has the same tag name as the opening tag. The back-reference `\1` ensures this consistency by referencing the text captured by `([a-z]+)`.

Here are the breakdown in details:

- `<([a-z]+)`: This part captures the opening HTML tag and captures the tag name within the first capturing group. For example, if the opening tag is `<div>`, it captures "div" in the first capturing group.

- `(.*?)`: This part captures the content within the HTML tag, which may include text, other tags, or attributes. It uses a non-greedy quantifier `*?` to capture as little text as possible.

- `<\/\1>`: This part matches the closing HTML tag using the back-reference `\1`. It ensures that the closing tag has the same tag name as the opening tag. For example, if the opening tag is `<div>`, it ensures that the closing tag is `</div>`.

By using the back-reference `\1`, this regex pattern ensures that HTML tags are correctly structured with matching opening and closing tags and that the tag names are consistent between them. This is a common use case for back-references when working with structured text like HTML or XML.

### Look-ahead and Look-behind

Look-ahead and look-behind assertions in regular expressions are used to define conditions that must be satisfied for a match to occur, without including the matched text in the result. These assertions allow us to specify patterns that need to be present (or absent) in the text surrounding the main pattern we're trying to match. Look-ahead and look-behind assertions are also known as zero-width assertions because they don't consume characters in the input string; instead, they only check whether a condition is met at a particular position.

In the regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, there are no explicit look-ahead or look-behind assertions (`(?=...)`, `(?!...)`, `(?<=...)`, `(?<!...)`) used.

## Author

- Name: Christian Setiawan
- Github: https://github.com/csetiawan88
