# Assignment Template for Typst

A clean, customizable assignment template with themed problem boxes, multi-author support, and configurable typography.

## Quick Start

Initialize a new project from the template:

```bash
typst init @preview/stux-assignment:0.1.0
```

Or import it manually in an existing file:

```typst
#import "@preview/stux-assignment:0.1.0": *

#show: assignment.with(
  title: "Assignment - 1",
  authors: (
    (name: "Your Name", email: "you@example.com", roll: "123456"),
  ),
  course: "CS 101",
)

#problem()[
  What is $1 + 1$?
]

#solution[
  $1 + 1 = 2$
]
```

Compile with `typst compile main.typ` or use the [Tinymist VS Code extension](https://marketplace.visualstudio.com/items?itemName=myriad-dreamin.tinymist).

## Features

### Themes

Five built-in color themes for problem boxes:

| Theme    | Background | Accent   |
| -------- | ---------- | -------- |
| `teal`   | `#e9f2f0`  | `#007070` |
| `purple` | `#f2e9f2`  | `#74007b` |
| `brown`  | `#f2efe9`  | `#7b5700` |
| `red`    | `#f0e5e5`  | `#af0101` |
| `gray`   | `#f1f1f1`  | `#7e7676` |

Set a theme by name:

```typst
#show: assignment.with(
  ...
  theme: "purple",
)
```

Or pass a custom color dictionary:

```typst
#show: assignment.with(
  ...
  theme: (bg: rgb("#e6f0ff"), fr: rgb("#0055aa")),
)
```

### Multiple Authors

Pass an `authors` array. A single entry renders the standard side-by-side header, while multiple entries switch to the centered author table. Author rows with only `none` values are omitted automatically in both layouts.

The legacy `author`, `email`, `roll`, and `num_of_authors` arguments are still accepted for backward compatibility. Supplying `authors` together with any legacy author arguments is an error.

```
          Course: CS 101
    Group Assignment - 1
      Date: Jan 01, 2026
──────────────────────────────────────
   Alice    |    Bob    |    Charlie
  Roll: 101 | Roll: 102 |  Roll: 103
```

```typst
#import "@preview/stux-assignment:0.1.0": *

#show: assignment.with(
  title: "Group Assignment - 1",
  authors: (
    (name: "Alice", email: "alice@example.com", roll: "101"),
    (name: "Bob", email: none, roll: "102"),
    (name: "Charlie", email: "charlie@example.com", roll: none),
  ),
  course: "CS 101",
)
```

![Example](/thumbnail.png)

For single-author assignments, pass a one-entry `authors` array. The legacy single-author shorthand still works, but `authors` is the preferred API.

### Font Customization

Override the default font family and size:

```typst
#show: assignment.with(
  ...
  font-size: 12pt,
  font-family: "New Computer Modern",
)
```

Defaults are `11pt` and `"Linux Libertine"`.

## All Parameters

| Parameter     | Default                             | Description                                  |
| ------------- | ----------------------------------- | -------------------------------------------- |
| `title`       | `"Assignment"`                      | Assignment title                             |
| `author`      | `auto`                              | Legacy single-author name                    |
| `email`       | `auto`                              | Legacy single-author email                   |
| `roll`        | `auto`                              | Legacy single-author roll number             |
| `num_of_authors` | `auto`                           | Legacy multi-author switch                   |
| `authors`     | `auto`                              | Preferred array of `(name, email, roll)` dictionaries |
| `course`      | `"Course Name"`                     | Course identifier                            |
| `date`        | today's date                        | Display date                                 |
| `theme`       | `"teal"`                            | Theme name or custom `(bg: …, fr: …)` dict   |
| `font-size`   | `11pt`                              | Document font size                           |
| `font-family` | `"Linux Libertine"`                 | Document font family                         |
| `show-solutions` | `true`                           | Whether to render `#solution` blocks         |

## Template Functions

- **`#problem(title: none, label: none)[…]`** — Numbered problem box styled with the active theme. Optional `title` appears after the number and `label` can be referenced elsewhere.
- **`#solution[…]`** — Indented solution block with an italic "Solution:" label. Hidden when `show-solutions: false`.
>>>>>>> 365fff2 (Add solution toggle)


## License

This package is licensed under the [MIT License](LICENSE).
