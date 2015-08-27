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
