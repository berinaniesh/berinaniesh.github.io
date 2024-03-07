+++
title = "Universal Code Formatter"
date = 2023-01-25
draft = false
+++

Git Repo: [Link](https://github.com/berinaniesh/ucf)

Crates.io: [Link](https://crates.io/crates/ucf)

Universal Code Formatter (UCF) is a command line application that formats most programming language files. 

## Why ucf

Each programming / markup language has a different formatting tool with different command line flags and different behaviours. The burden of selecting a tool and calling it with the right parameters lies on the IDE or the end user. UCF takes that on to itself. So, without UCF

```
black code1.py
gofmt -w code2.go
rustfmt code3.rs
prettier -w code4.html
clang-format -i code5.cpp
```

With UCF

```
ucf code1.py
ucf code2.go
ucf code3.rs
ucf code4.html
ucf code5.cpp
```

## Installation

### With cargo

```
cargo install ucf
```

### AUR
```
yay -S ucf
```

## Working

Under the hood, `ucf` is a simple program. It determines the file extension of the file and calls the appropriate code formatter with appropriate arguments. The called code formatter should be present in the system's `$PATH`.
