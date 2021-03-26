# Summary of Go

## Basic
- **Commentary**
  - C-style `/* */` block comments : package
  - C++-style `//` line comments : simple package

- **Names**
  - Package names : lower case, single-word, short, concise, evocative
  - Getters / Setter : Owner / SetOwner
  - Interface names : Reader, Writer, Formatter, CloseNotifier etc
  - Multiword names : MixedCaps or mixedCaps

- **Semicolons**

  Idiomatic Go programs have semicolons only in places such as for loop clauses, to     
  separate the initializer, condition, and continuation elements.
  
- **Control structures**
  - if
    ```go
    if x > 0 {
        return y
    }
    ```
  - for
    ```go
    // Like a C for
    for init; condition; post { }

    // Like a C while
    for condition { }

    // Like a C for(;;)
    for { }
    ```
