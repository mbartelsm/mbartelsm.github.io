---
layout: page
title: Dynasties (1)
author: Miguel Bartelsman
---

Dynasties is meant to be a royal family tree generator for worldbuilding and alt-history enthusiasts. I will be building this project using [Rust](https://www.rust-lang.org/), primarily because I want to learn the language and this project is as good an opportunity as any to get some practice. Design goals for the project include generating a realistic and clear family tree, emulating the lives of each person and the environmental factos at play to produce a believable timeline and the possibility to add custom individuals to the timeline.

One thing at a time, though. The first thing that needs to be asked is "what makes a person?" or, rather, "what is the minimal representation of a person in such a project?"

## A person

The life of every person can be condensed into two lists, a list of relatives--spouses, parents, children, friends-- and a list of events--birth, death, illnesses, marriages, promotions--. For the first one, there's only really two relations that are mandatory for a person to exist: a father and a mother. For the second one, assuming we are viewing the world from outside the flow of time, a person is at least born and will at some point die.

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
    relatives: vec![
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
    Valiant,  // +10% chance of battles or duels, +10% public support
    Craven,  // -10% chance of battles or duels, -10% public support
    /* ... */
}

```
