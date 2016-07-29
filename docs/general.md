# [REI Code Style Guides](/README.md) // General

> Code style guidelines that apply to all programming languages at REI

## filenames

Filenames should be **lower-case and dash-delimited**:

```
// good
my-directory/
    my-sub-directory/
    my-file.txt

// bad
myDirectory/
    mySubDirectory/
    myFile.txt
```

## indentation

Indentation should be **four-space soft-tabs**:

```
// good
.foo {
    margin: 0;
}

function foo () {
    return 'foo';
}

<body>
    <p>Yay! Paragraphs rule!</p>
</body>

// bad
.foo {
   font-size: 12;
  margin: 0;
 padding: 0;
}

function foo () {
  return 'foo';
}

<body>
  <p>Yay! Paragraphs rule!</p>
 <p>But these want better spacing.</p>
</body>
```

## contents

The contents of a file should **end with a new line**

This is a general best practice so that files are unix friendly, due to the
defintion of a "Line" from the Posix standard:
> A sequence of zero or more non- <newline> characters plus a terminating <newline> character.

For example:
```
module.exports = {
     handleDropDownClick: handleDropDownClick
};EOF
```

Should be:
```
module.exports = {
     handleDropDownClick: handleDropDownClick
};
new line goes here (\n)EOF
```


ALL new lines should be **unix new line**: `\n` *also known as LF or line feed*

Do **NOT** use windows carriage return `\r` (CR, Carriage Return, ^M) or a mac new line `\r\n` (CR+LF)

