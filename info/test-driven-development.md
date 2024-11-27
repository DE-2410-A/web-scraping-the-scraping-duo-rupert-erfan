# ![Digital Futures](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Test-Driven Development

### Overview

There are many different practices and techniques used to develop code.  All have their own merits, advantages and disadvantages. Test-Driven Development is one such technique that comes from the set of Extreme Programming practices developed by Agile pioneer, Kent Beck.  This document will introduce Test-Driven Development and a technique to execute it in a pair-programming environment.

---

## Test-Driven Development - Concepts

### What is TDD?

- Core practice of XP
- Can be adopted within other methodologies

> "Test-first programming is the least controversial and most widely adopted part of Extreme Programming (XP). By now the majority of professional Java™ programmers have probably caught the testing bug" – Elliotte Rusty Harold [Who is Elliotte Rusty Harold?](https://en.wikipedia.org/wiki/Elliotte_Rusty_Harold)

- Test written before implementation
- Tools and techniques make TDD very rigorous process
- aka Test Driven Design
- Tests drive design of API
- Developers become "Test infected" (Erich Gamma - [Who is Erich Gamma?](https://en.wikipedia.org/wiki/Erich_Gamma))
  - Cannot program without test first

---

### Uncle Bob's Three Rules of TDD

**1. You are not allowed to write any production code unless it is to make a failing unit test pass.**
**2. You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.**
**3. You are not allowed to write any more production code than is sufficient to pass the one failing unit test.**

**This is according to Uncle Bob!** [Who is Uncle Bob?](https://en.wikipedia.org/wiki/Robert_C._Martin)

---

### Test – Code – Refactor

Kent Beck's [Who is Kent Beck?](https://en.wikipedia.org/wiki/Kent_Beck) summary of TDD:

1. Write new code only if you first have a failing automated test
2. Eliminate duplication

#### Red - Green - Refactor

![Red-Green-Refactor-1](../images/rgrf1.png)

The image above illustrates that the famous green bar is indeed a progress bar. The image below shows the final outcome of running this series of tests: there are 3 failures.

![Red-Green-Refactor2](../images/rgrf2.png)

#### Red-Green-Refactor Workflow

![Red-Green-Refactor Workflow](../images/rgrf3.png)

---

### More on TDD

#### TDD Benefits

- Build up library of small tests that protect against regression bugs
- Extensive code coverage
- No code without a test
- No code that is not required
- Almost completely eliminates debugging
- More than offsets time spent developing tests
- Tests as developer documentation
- Confidence not fear
- Confidence in quality of the code; confidence to refactor
- A regression bug is a defect which stops some bit of functionality working, after an event such as a code release, or refactoring.

#### TDD Strategies

More from Kent Beck:

- Fake it:
  - Return a *constant*; gradually replace *constants* with *variables*
- Obvious implementation:
  - If a quick, clean solution is obvious, type it in
- Triangulation:
  - Locating a transmitter by taking bearings from 2 or more receiving stations
  - Only generalise code when you have 2 or more different tests

The point is to get developers to work in very small steps, continually re-running the tests.

```sh
                   <=> A
                  /  \
                 /    \
                /      \
               /        \
              /          \
             /            \
            ¶              []
            B               C
```

**Triangulation:** someone on the boat at A can determine their position on a chart by taking compass bearings to the lighthouse at B and the tower at C. Or conversely, observers at B and C can work out the location of the boat by taking bearings to it from their known points on the shore and sharing their readings. In fact, sailors are taught to take a three-point fix, with charted landmarks that are as widely separated as possible, for better accuracy.

#### Testing Heuristics

**Test List:**

- Start by writing a list of all tests you know you have to write

**Starter Test:**

- Start with case where output should be same as input

**One Step Test:**

- Start with test that will teach you something and you are confident you can implement

**Explanation Test:**

- Ask for and give explanations in terms of tests

**Learning Tests:**

- Check your understanding of a new API by writing tests

These mainly come from Kent Beck's book **Test Driven Development**, *Chapter 26 – "Red Bar Patterns"*. They're primarily suggestions for breaking down a seemingly mountainous task of developing some new functionality in a test-driven way, into very small, tractable steps.

For example:

> "a poster on the Extreme Programming newsgroup asked about how to write a polygon reducer test-first.
>
> The input is a mesh of polygons and the output is a mesh of polygons that describes precisely the same surface, but with the fewest possible polygons.
>
> How can I test-drive this problem since getting a test to work requires reading Ph.D. theses?”
>
> **Starter Test** provides an answer:
>
> The output should be the same as the input.
>
> Some configurations of polygons are already normalized, incapable of further reduction. The input should be as small as possible, like a single polygon, or even an empty list of polygons."
>
> **Explanation Test** is primarily for communicating within the development group, clarifying the requirements for some item of functionality by expressing them precisely in terms of tests.

---

## Test-Driven Development - Strategies

A good pair programming technique to use is ***Ping Pong***:

Like a game of Table Tennis:

- One writes a test and bats it over the the other
  - This can be done remotely using a shared screen or a shared code editor
  - The code should be shared using a version control system like Git - push and pull
  - It's important that only one of the pair works on the code at a time
- The other writes the code for the test and then writes a new test that is batted back to the partner
- Ad infinitum until all of the code has been written and all of the identified test cases pass
  - We test for the expected behaviour of the code, including handling expected 'bad' responses
  - We also test for the unexpected behaviour of the code, including handling unexpected 'bad' responses
  - We test edge and corner cases to ensure that the code is robust and resilient

Other Pair Programming techniques exist:

- Strong-Style Pairing (aka Driver-Navigator):
  - The person at the keyboard (the "Driver") only types what the "Navigator" tells them to type.
  - The Navigator thinks about the direction and strategy of the code.
  - This technique emphasizes communication and collaboration.

- Remote Pairing:
  - Pair programming done remotely using tools like screen sharing, video calls, and collaborative coding platforms.
  - Requires good communication tools and practices to be effective.

- Tour Guide:
  - One partner (the "Guide") explains the codebase and the task at hand to the other (the "Tourist").
  - The Tourist asks questions and provides fresh perspectives, which can lead to new insights and improvements.

- Mob Programming:
  - An extension of pair programming where the entire team works on the same code at the same time.
  - One person types (the Driver) while the rest of the team (the Navigators) discuss and guide the implementation.
  - Promotes knowledge sharing and team cohesion.

---

|---> Back to [Activity 2 - Making a Request](../activities/02-making-a-request.md)
