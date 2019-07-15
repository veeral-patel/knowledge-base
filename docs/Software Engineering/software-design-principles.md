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

## Domain driven design

From ["DDD Quickly"](http://carfield.com.hk/document/software%2Bdesign/dddquickly.pdf)

- DDD helps establish a shared vocabulary between developers and domain experts
- In DDD, there's two kinds of objects, entities and value objects

### Entities

- an object not defined by its attributes
- an entity's attributes aren't sufficient to describe it
- each entity has its own unique identifier (eg, an ID, UUID, combination of attributes, etc)
- example - a human

### Value objects

- we only care about the attributes
- for example, a point & its coordinates

### Distinguishing entities and value objects

- If you changed a person's name, hair color, and age, would be the same person? YES => Entity
- If you changed an address's street name and city, would it be the same address? NO => Value object

### Services and bounded contexts

- Services are helper functions that don't belong in entity nor value objects
- Bounded contexts - a customer to Sales is not the same as a customer to Customer Support. Sales and Customer Support are bounded contexts.
