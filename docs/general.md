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

This is a general best practice so that files are unix friendly. Due to the
definition of a "Line" from the [Posix standard](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap03.html#tag_03_206), some unix tools may not recognize or play "nice" with files that do not conform.
<sup>[[1]](http://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline#comment-17614747)</sup>
<sup>[[2]](http://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline#comment-20018808)</sup>
<sup>[[3]](http://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline#comment-52935541)</sup>

Should be:
```
module.exports = {
     handleDropDownClick: handleDropDownClick
};⏎

END_OF_FILE
```

Should not be:
```
module.exports = {
     handleDropDownClick: handleDropDownClick
};END_OF_FILE
```

All non-unix newlines (CR `\r` & CR+LF `\r\n`) are automatically converted by git to a **unix new line** (`\n`) upon commit, so no need to be concerned when working across windows/mac.
