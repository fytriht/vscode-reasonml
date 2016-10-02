# vscode-reasonml

Reason support for Visual Studio Code

![screenshot](https://github.com/freebroccolo/vscode-reasonml/raw/master/assets/screenshot.png)

## Theme

Syntax highlighting works with any theme but "Flatland Monokai" is recommended.

## Status

The VS Code [insiders build](https://code.visualstudio.com/insiders) is highly recommended since it
provides improved documentation formatting and scrollable hovers (shown above).

- [x] advanced syntax highlighting
- [x] completion
- [x] linting
- [x] outline view for symbols (⇧⌘O)
- [x] type and documentation on hover
- [x] jump-to-definition (⌃+click or ⌘+hover)
- [x] case splitting (see below for details)
- [ ] formatting integration
- [ ] build tool integration
- [ ] debugger integration
- [ ] toplevel integration

### Case splitting

For the examples below, `<cursor>` represents the position of the current VS Code editor cursor.

#### Introducing a `switch`

In order to introduce a `switch`, execute the following steps:

1. select an identifier or move the cursor anywhere within its word range (as below)
2. open the palette (⇧⌘P) and run `Reason: case split` (typing `case` should pull it up)

##### Before
```
let foo (arg: list 'a) => a<cursor>rg;
```

##### After
```
let foo (arg: list 'a) => switch arg {
  | [] => failwith "<case>"
  | [_, ..._] => failwith "<case>"
};
```

#### Nesting `switch` expressions

The `switch` introduction functionality works with nested `switch` expressions:

##### Before
```
let foo (arg: list 'a) => switch arg {
  | [] => failwith "<case>"
  | [_, ...xs] => x<cursor>s
};
```

##### After
```
let foo (arg: list 'a) => switch arg {
  | [] => failwith "<case>"
  | [_, ...xs] => switch xs {
    | [] => failwith "<case>"
    | [_, ..._] => failwith "<case>"
  }
};
```

#### Splitting a pattern without introducing a `switch`

The case split feature can be used to split an existing pattern further:

##### Before
```
let foo (arg: list 'a) => switch arg {
  | [] => failwith "<case>"
  | [x, ...x<cursor>s] => failwith "<case>"
};
```

##### Before
```
let foo (arg: list 'a) => switch arg {
  | [] => failwith "<case>"
  | [_] | [_, _, ..._] => failwith "<case>"
};
```
