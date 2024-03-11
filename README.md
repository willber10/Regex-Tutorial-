# Understanding Email Matching Regex

This tutorial will explain a regular expression (regex) used to validate email addresses. The regex we will be discussing is: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

## Summary

The regular expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` is used to validate email addresses. It ensures that the input string follows the standard format of an email address, which consists of a username, domain, and extension. The username can include lowercase letters, numbers, underscores, dots, and hyphens. The domain can include digits, lowercase letters, dots, and hyphens. The extension must be between 2 to 6 characters long and can only contain lowercase letters and dots.

## Regex Components 

### Anchors 

The `^` and `$` symbols are anchors used in regular expressions to specify the start and end of a line, respectively. These anchors do not match any characters themselves, but rather indicate the position before or after characters in a line of text.

The `^` symbol, known as the start of line anchor, asserts that the following pattern must start at the beginning of a line. For example, the regex `^abc` will match any line that starts with "abc".

The `$` symbol, known as the end of line anchor, asserts that the preceding pattern must be at the end of a line. For example, the regex `abc$` will match any line that ends with "abc".

When used together, as in `^abc$`, the regular expression will match an entire line that consists only of "abc". Any additional characters at the start or end of the line will result in no match.

It's important to note that the behavior of these anchors can be influenced by the multiline mode of the regex engine. In multiline mode, `^` and `$` match the start and end of each line, rather than the start and end of the entire input string.

Code:
```javascript
let regex = /^abc$/;
console.log(regex.test("abc")); // true
console.log(regex.test("abcd")); // false
console.log(regex.test("abcdabc")); // false
console.log(regex.test("abcabc")); // false 
```

### Quantifiers 

The `+` quantifier in regular expressions indicates that there must be one or more occurrences of the preceding element. On the other hand, the `{2,6}` quantifier specifies that there should be between 2 and 6 occurrences of the preceding element.

Quantifiers are used in regular expressions to define the required number of repetitions for a match. They determine the amount of repetition.

The `+` quantifier means that the preceding character, group, or character class must exist at least once for a match to occur. For example, in the regex `a+`, it will match "a", "aa", "aaa", and so on, but not an empty string.

The `{n,m}` quantifier means that there should be between n and m occurrences of the preceding element, where n and m are integers. This quantifier is useful when you want to specify a specific range of repetitions. For example, in the regex `a{2,6}`, it will match "aa", "aaa", "aaaa", "aaaaa", "aaaaaa", but not "a" or "aaaaaaa".

It's important to note that quantifiers are greedy by default, meaning they will match as many instances of the preceding element as possible. For example, in the string "aaaaa", the regex `a+` will match the entire string, not just the first "a". However, this behavior can be modified using certain flags or additional quantifiers.


### Character Classes

The email matching regex uses character classes to match specific characters in an email address.

Character classes, denoted by square brackets `[]`, allow you to match any one character within the specified range. In this regex, three character classes are used:

1. `[a-z0-9_\.-]`: This character class matches any lowercase letter (a-z), digit (0-9), underscore (_), dot (.), or hyphen (-). It is used to match the username part of the email address.

2. `[\da-z\.-]`: This character class matches any digit (\d), lowercase letter (a-z), dot (.), or hyphen (-). It is used to match the domain part of the email address.

3. `[a-z\.]`: This character class matches any lowercase letter (a-z) or dot (.). It is used to match the extension part of the email address.

The dot and hyphen are escaped with a backslash to avoid confusion. The dot does not need to be escaped within a character class, but the hyphen does when it's not used to specify a range.

Remember that character classes allow you to match one of many characters within a specified range.

### Grouping and Capturing 

The parentheses `()` in regular expressions are used for grouping and capturing. They allow you to divide the regex into three sections: the username, domain, and extension.

Grouping and capturing are important functionalities in regular expressions that enable you to group specific parts of your pattern together. This grouping allows you to treat those parts as a single unit. The grouping is achieved by enclosing the desired pattern within parentheses `()`.

### Grouping 

Grouping in regular expressions is a useful technique when you want to apply a quantifier to a specific set of characters. It allows you to treat multiple characters as a single unit. For example, in the regex `(ab)+`, the `+` quantifier applies to the entire group `ab`, not just the individual character `b`. This regex will match "ab", "abab", "ababab", and so on.

In the context of the email matching regex, grouping is used to separate the email address into three distinct parts: the username, domain, and extension. Each part is enclosed in parentheses, such as ([a-z0-9_\.-]+), ([\da-z\.-]+), and ([a-z\.]{2,6}). This allows for easier manipulation and validation of each component of the email address.

### Capturing 

In addition to grouping, parentheses in regular expressions also serve as capturing groups. A capturing group captures the part of the string that matches the pattern inside the parentheses. These captured groups can be referenced later using backreferences (e.g., `\1`, `\2`).

In the email matching regex, there are three capturing groups that correspond to the username, domain, and extension of the email address. However, this regex does not utilize backreferences, so the capturing feature is not used in this case.

It's important to note that not all parentheses create capturing groups. To group without capturing, you can use non-capturing parentheses, denoted as `(?:...)`.

### Bracket Expressions 

This regular expression utilizes bracket expressions to define the allowable characters for each part of an email address.

Bracket expressions, also known as character classes, are a feature of regular expressions that enable matching any single character from a specified set. They are denoted by square brackets `[]`.

Within a bracket expression, you can specify individual characters or a range of characters. For instance, `[abc]` will match any one of the characters "a", "b", or "c". Similarly, `[a-z]` will match any lowercase letter from "a" to "z".

In the context of this email matching regex, bracket expressions are used to define the character ranges allowed in different sections of an email address:

- `([a-z0-9_\.-]+)`: The bracket expression `[a-z0-9_\.-]` specifies that the username part of the email address can consist of lowercase letters (a-z), digits (0-9), underscores (_), dots (.), or hyphens (-).
- `([\da-z\.-]+)`: The bracket expression `[\da-z\.-]` specifies that the domain part of the email address can include digits (\d represents any digit), lowercase letters (a-z), dots (.), or hyphens (-).
- `([a-z\.]{2,6})`: The bracket expression `[a-z\.]` specifies that the extension part of the email address can contain lowercase letters (a-z) or dots (.).

It's important to note that within a bracket expression, most special characters lose their special meaning and are treated as literal characters. For example, the dot (.) typically matches any character, but inside a bracket expression, it represents a dot itself. However, certain characters like the hyphen (-) can have a special meaning within a bracket expression (to specify a range), so they need to be escaped with a backslash if they are intended to be interpreted as literal characters.


### Greedy and Lazy Match

The regular expression in this code snippet utilizes a greedy match approach, which aims to match the longest possible substring.

In the realm of regular expressions, the terms "greedy" and "lazy" are used to characterize the matching behavior of quantifiers.

### Greedy Match

By default, quantifiers in regular expressions are "greedy", meaning they will attempt to match as much as possible. For instance, if we have the string "aaaaa" and the regex `a+`, the `+` quantifier is greedy and will match the entire string, not just the first "a".

This greedy behavior is a result of how the regex engine operates. It starts at the beginning of the string and tries to match the entire pattern at that position. If it fails, it moves to the next position and repeats the process. This continues until a match is found or the end of the string is reached.

In the case of the email matching regex, the `+` and `{2,6}` quantifiers exhibit greedy behavior. They will attempt to match as many characters as possible while still allowing the entire regex to match.

### Lazy Match 

In contrast, a "lazy" or "non-greedy" quantifier aims to match the smallest possible substring. It is denoted by appending a `?` after the quantifier. For instance, the regex `a+?` will match only one "a" in the string "aaaaa", instead of the entire string.

Lazy quantifiers are useful when you want to find the shortest substring that satisfies the pattern. However, the email matching regex does not utilize lazy quantifiers. All quantifiers in this regex are greedy, meaning they try to match as much as possible.
