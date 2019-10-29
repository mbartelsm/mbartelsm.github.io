---
layout: page
title: Dynasties - making of
author: Miguel Bartelsman
---

# Dynasties

Fantasy royal family generator

## Plan

### A person

The life of every person can be condensed into two lists, a list of relations, and a list of events. For the first one, there's only really two relations that are mandatory for a person to exists: a father and a mother. For the second one, assuming a detached state from the time of the world, these two mandatory events are a person's birth and death.

```rust
struct Person {
    name: String,
    relations: Vector<Relative>,
    events: Vector<Event>,
}

enum Relative {
    Father(Person),
    Mother(Person),
    /* ... */
    Other(String, Person),
}

enum Event {
    Birth(Date),
    Death(Date),
    /* ... */
    Other(String, Date),
}
```
```rust
let guy: Person = {
    name: String::from("John Doe"),
    relations: vec![
        Relative::Father(some_other_guy),
        Relative::Mother(some_gal)
    ],
    events: vec![
        Event::Birth(1900),
        Event::Death(1980),
    ]
}
```

Other features for the family tree can be added as methods (ideally) or as extra fields in the structure (if necessary). For example, if one needs to know if the person has ever held the royal crown, then a method scanning for a crowning event should do it. For extremely common searches, private flags and variables might be defined.

A more thorough implementation may also include a list of traits, these traits may be innate (from birth) or acquired (from other events) and may have an impact on the life of the person.

```rust
struct Person {
    /* ... */
    traits: HashSet<Trait>,
    /* ... */
}

enum Trait {
    Valiant,  // +10% chance of battles or duels, -10% chance of coups
    Craven,  // -10% chance of battles or duels, +10% chance of coups
    /* ... */
}

```
