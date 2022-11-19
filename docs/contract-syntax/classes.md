---
sidebar_position: 3
---

# Creating A Class

The basic syntax that goes into writing a class is the following,

```text
Create Class [ClassName].
```

That's it!

Some points about class names,

* ClassNames, once set, cannot be changed
* ClassNames must be unique in a "namespace"

## Adding Attributes

To help with making people somewhat familiar with technology and development, `Contract` follows the pattern similar to what `SQL` follows, that is, creating attributes inside a braces for a table. This results in the following syntax,

```text
Create Class Pet (name String, owner String,
species String, sex String, birth Date, death Date);
```

The keyword `String` is used here in abstraction in `Contract`, what if `name` is only 5 characters long, what about 20, what if it gets 6000 characters? Because we are not storing this, but rather validating against, whatever response we get to validate, we only need to check if name IS a string.

You may already be thinking, what if `name` happens to be completely empty? What if I want to limit how many characters it can have? What if I only want it to have specific characters? What if I want to use regex here?

I heard you, but if you think about it, we also have similar concerns with the `Date` type as well.

### Defining Constraints



#### Boolean

## Inheriting Classes

One existing notion of classes that comes into mind is that of `Inheritance`, and depending on. `Contract` tries to apply the idea of dealing with classes as objects, that means talking primarily about the attributes, and nested attributes that may exist.

What happens when you have a class that does most things for you, but then you get requirements that in many other cases, you still need to have the attributes that your first class has, but depending on varying situations, you need other attributes as well?

`Contract` addresses this with the following example.
