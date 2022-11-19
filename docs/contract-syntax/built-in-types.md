---
sidebar_position: 2
---

# Table Of Contents

- [Table Of Contents](#table-of-contents)
- [Types](#types)
  - [Constraint Rules](#constraint-rules)
  - [Syntactical Guide For Types](#syntactical-guide-for-types)
  - [Boolean](#boolean)
    - [Syntax](#syntax)
    - [Setting Optional Parameters](#setting-optional-parameters)
  - [Decimal](#decimal)
    - [Syntax](#syntax-1)
    - [Setting Optional Parameters](#setting-optional-parameters-1)
  - [Integer](#integer)
    - [Syntax](#syntax-2)
    - [Setting Optional Parameters](#setting-optional-parameters-2)
  - [String](#string)
    - [Syntax](#syntax-3)
    - [Setting Optional Parameters](#setting-optional-parameters-3)
    - [Use Cases/FAQs](#use-casesfaqs)

# Types

Types define the `datatype` of what an attribute in a `class` should be. It defines constraints (if any), enables type checking, and provides a way to flexibly deal with most business cases out there.

The `Contract` language sports the following types as by default to be parsed,

- **Boolean**: A `true` or `false` value
- **Decimal**: A floating point value, such as `1.52`, `46555.5333`, `4455000.0005`
- **Integer**: A numeric value, such as `1`, `655`, `25`, etc.
- **String**: A `literal string`, such as `Hello World!`, `Do you know how awesome you are?`
- **Date**: A date, datetime representation, needs explicit mention of the format

## Constraint Rules

- Order does not matter when defining constraints.

## Syntactical Guide For Types



## Boolean

### Syntax

Syntax,

```text
AreYouAwesome Boolean(TRUE ONLY | FALSE ONLY)
```

Where,

- `TRUE ONLY`, only accept true as value
- `FALSE ONLY`, only accept false as value

### Setting Optional Parameters

- Defining a boolean attribute that can only be true,

```text
Create Class NewClass (AreYouAwesome Boolean(TRUE ONLY))
# If the response sets this to False, the "mock output" would be true
```

- What about an only `false` option?

```text
Create Class NewClass (ThisIsInMarkdown Boolean(FALSE ONLY))
# If the response sets this to False, the "mock output" would be false
```

## Decimal

### Syntax

Syntax,

```text
Score Decimal([MIN=-5.0 × 10−324] | [MAX=1.7 × 10+308])
```

Where,

- `MIN`, the lowest value that should be accepted. By default is set to `-5.0 × 10−324`
- `MAX`, the highest value that should be accepted. By default is to `1.7 × 10+308`

### Setting Optional Parameters

- Setting a minimum value,

```text
Create Class DecimalClass (Score Decimal(MIN=0.0))
# If the response sets a lower min, the "mock output" would be 0.0
```

- Setting a maximum value,

```text
Create Class DecimalClass (Score Decimal(MAX=10.0))
# If the response sets a higher max, the "mock output" would be 10.0
```

- Both together,

```text
Create Class DecimalClass (Score Decimal(MIN=0.0, MAX=10.0)) # OR
Create Class DecimalClass (Score Decimal(MAX=10.0, MIN=0.0))
```

## Integer

### Syntax

Syntax,

```text
Score Integer([MIN=-2147483648] | [MAX=2147483647])
```

Where,

- `MIN`, the lowest value that should be accepted. By default is set to `-2147483648`
- `MAX`, the highest value that should be accepted. By default is to `2147483647`

### Setting Optional Parameters

- Setting a minimum value,

```text
Create Class DecimalClass (Score Decimal(MIN=0.0))
# If the response sets a lower min, the "mock output" would be 0.0
```

- Setting a maximum value,

```text
Create Class DecimalClass (Score Decimal(MAX=10.0))
# If the response sets a higher max, the "mock output" would be 10.0
```

- Both together,

```text
Create Class DecimalClass (Score Decimal(MIN=0.0, MAX=10.0)) # OR
Create Class DecimalClass (Score Decimal(MAX=10.0, MIN=0.0))
```

## String

### Syntax

Syntax,

```text
Name String([(MIN_CHAR=0, [ON_ERROR={"" * MIN_CHAR}])] | [(MAX_CHAR=255, [ON_ERROR={"" * MIN_CHAR}])] | [(ALPHABETS_ONLY=false, [ON_ERROR={"" * MIN_CHAR}])] | [(UPPERCASE_ONLY=false, [ON_ERROR={"" * MIN_CHAR}])] | [(LOWERCASE_ONLY=false, [ON_ERROR={"" * MIN_CHAR}])] | [(NUMERICS_ONLY=false, [ON_ERROR={"" * MIN_CHAR}])] | [(ALPHANUMERICS_ONLY=false, [ON_ERROR={"" * MIN_CHAR}])] | [(SPECIAL_ONLY=false, [ON_ERROR={"" * MIN_CHAR}])] | [(ALPHA_SPECIAL_ONLY=false, [ON_ERROR={"" * MIN_CHAR}])] | [(NUMERICS_SPECIAL_ONLY=false, [ON_ERROR={"" * MIN_CHAR}])] | [(NO_SPACES=false, [ON_ERROR={"" * MIN_CHAR}])] | [(NOT_EMPTY=false, [ON_ERROR={"" * MIN_CHAR}])] | [(REQUIRED=false, [ON_ERROR={"" * MIN_CHAR}])] | [(REGEX="", [ON_ERROR={""}])])
```

Where,

- `MIN_CHAR` (**integer**), the lowest number of characters the attribute is allowed to have. By default is set to `0`. Accepts integer.
- `MAX_CHAR` (**integer**), the highest number of characters the attribute is allowed to have. By default is set to `255`.
- `ALPHABETS_ONLY` (**boolean**), only allows characters, both lowercase and uppercase. Only English at the moment.
- `UPPERCASE_ONLY` (**boolean**), only uppercase characters in the range `[A-Z]`. Must not be empty.
- `LOWERCASE_ONLY` (**boolean**), only lowercase characters in the range `[a-z]`. Must not be empty.
- `NUMERICS_ONLY` (**boolean**), only allows numerics in the range `[0-9]`. Must not be empty.
- `ALPHANUMERICS_ONLY` (**boolean**), allows alphabets and numerics only in the range `[A-Za-z0-9]`. Must not be empty.
- `SPECIAL_ONLY` (**boolean**), only allow special characters, ie, anything in the set of `;:'"{}[]!@#$%^&*()-=_+\|/.><,~`. Must not be empty.
- `ALPHA_SPECIAL_ONLY` (**boolean**), both alphabets (lower + upper), and aforementioned special characters.
- `NUMERICS_SPECIAL_ONLY` (**boolean**), both numerics, and special characters
- `NO_SPACES` (**boolean**), no spaces are allowed.
- `NOT_EMPTY` (**boolean**), and empty string (`""`) is not acceptable/
- `REQUIRED` (**boolean**), if required, the value may not be null or the empty string. If not required, and the
value is null or the empty string and the other validation constraints are skipped.
- `REGEX` (**string**, **literal**), use set regex to validate string. Regex depends on implementation language.

### Setting Optional Parameters

- Setting `MIN_CHAR`,

```text
Create Class StringClass (Name String((MIN_CHAR=0)))
# If the response gives a null, the "mock output" would be ""
```

- Setting `MAX_CHAR`,

```text
Create Class StringClass (Score String(MAX_CHAR=10))
# If the response gives a longer string, the "mock output" would be spaces times MIN_CHAR
# If MIN_CHAR is 2, then "  " is returned to the client
```

- Setting `ALPHABETS_ONLY`

```text
Create Class StringClass (Score String(ALPHABETS_ONLY=true))
# If the response violates, 
```

### Use Cases/FAQs

- How do I set a fixed length for a string?
  - Set both `MIN_CHAR` and `MAX_CHAR` to the same number
