# Software Design Principles

## Interface Segregation Principle

[Codeburst.io Article](https://codeburst.io/understanding-solid-principles-interface-segregation-principle-b2d57026cf6c)

Keep interfaces small. Don't put methods into an interface that the interface's callers won't need.

Instead, separate them into smaller interfaces.

Instead of -

```
type Person interface {
    // syntax is wrong
    func talk()
    func smell()
    func eat()
    func kill()
}
```

Write -

```
type Eater interface {
    func eat()
}

type Killer interface {
    func kill()
}
```

And then you can compose small interfaces:

```
type Snake interface {
    Eater
    Killer
}
```

In Python, you'd just inherit from multiple interfaces:

```
class Snake(Eater, Killer):
    # Code here
```

Throwing `NotSupportedException` or `NotImplementedError` errors is a warning sign your interface is too big.

## Liskov Substitution Principle

[Nice explanation on Stack Overflow](https://stackoverflow.com/questions/56860/what-is-an-example-of-the-liskov-substitution-principle)

### The Problem

- Take a Board class that has methods `height`, `width`, `add_piece`, `add_tile`
- Now say you want to write a 3DBoard

- Idea - just inherit from Board! After all, a 3DBoard is a board
- So you subclass Board, but you have to re-write AddTile, AddUnit, etc methods, because they only take in x and y coordinates but not a z coordinate

### The Solution

- Don't inherit from Board
- You can find other ways to reuse Board's code without subclassing it
- A 3DBoard may be an array of Boards, for example
- If you find yourself checking the type of an instance, you may be violating the Liskov Substitution Principle

```
if typeof(board) is 3DBoard:
	# Code here
elif typeof(board) is Board:
	# Code here
else:
	# Throw error
```
