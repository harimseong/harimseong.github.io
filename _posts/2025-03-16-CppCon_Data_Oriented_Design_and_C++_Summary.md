---
layout: post
title: "Summary of CppCon Data Oriented Design and C++"
date: 2025-03-16 20:33:41 +0900
categories:
---

<!---
### What does game engine programmers do?


### What languages do they use?
- C/C++
- ASM
- shaders

### Similarity with embedded SW
Small embedded system with limited resources.
Game consoles are bigger but share a lot of similarities.
- Exceptions


avoid
- Templates


poor use cases slow things down without pros.
- Iostream
- Multiple inheritance
- Operator overloading
- RTTI
- No STL
- Custom allocators


Pre-allocation, Linear allocation, ...
- Custom debugging tools
-->

### Data-Oriented Design Principles
The purpose of all programs, and all parts of those programs, is to transform data from one form to another.

If you don't understand the data you don't understand the problem.

Conversely, understand the problem by understanding the data.

(There are frameworks that have its own way to deal with DOM in Web frontend and DB in Web backend. Programmer need to know how they works to decide a framework to use.)

Everything is a data problem. Including usability, maintenance, debug-ability.

Solving problems you probably don't have creates more problems you definitely do.

Latency and throughput are only the same in sequential systems.

Rule of thumb: Where there is one, there are many. Try looking on the time axis.
Solve the most common problem first.

Rule of thumb: The more context you have, the better you can make the solution. Don't throw away data you need.

Rule of thumb: NUMA extends to I/O and pre-built data all the way back through time to original source creation.

Software does not run in a magic fairy aether powered by the fevered dreams of CS phDs.
It is real engineering problem.

Reason must prevail.


### Three Big Lies
The only reason about this representation is it had been a response to the broader culture that C++ has endangered.

1. Lie 1: Software is a platform

    Hardware is the platform. Different hardware leads to different solution.

    e.g) Differenct CPU architecture, CPU capacity, ...

2. Lie 2: Code should be designed around model of the world

    It implies some relationship to real data or transforms.
    Real object in the real world is different from the object in OOP.
    How similar are PhysicalChair, BreakableChair, StaticChair?

    World modeling leads to monolithic, unrelated data structures and transforms.
    World modeling tries to idealize the problem.
    Actual reality is you have finite set of hardware and data.

    World modeling is the equivalend of self-help books for programming.
    It solves problems by analogy and storytelling, not engineering and reaility.

3. Lie 3: Code is more important than data.

    Only purpose of code is to transform data.
    Programmer is fundamentally responsible for the data, not the code.
    Code is the tool we use to do the transformation.
    Only write code that has direct, provable value.
    Understand the data to understand the problem.

Which means, There is no ideal, abstract solution to the problem.
"future proof" is impossible.

#### What problems do these lies cause?
poor performance

poor concurrency

poor optimization

poor stability

poor testability

#### Example
Key-value dictionary lookup using array of key-value pair

We associate key and value to make a pair because we have such mental model. 
When searching, values are not used most of the times, but most of the keys are used to compare.
So they are not associated directly.

If we need to search, only keys should be considered because cache size is very small.


Solve for the most common case first, not the most generic.

### "Can't the compiler do it?"
Memory access cost
- Register: free
- L1 Cache: 3 cycles
- L2 Cache: 20+ cycles
- RAM: 200+ cycles


There is one order of magnitude difference.

#### L2 cache misses/frame
- miss


L2 cache miss largely outweighs cost of expensive instruction or routine.

Time spend waiting for L2 : actual work = ~10 : 1

Compiler cannot solve the most significant problems. It is a tool, not a magic wand.
- frame


Don't waste cache line, use cache line to capacity.

#### Some common issues
- bools in structs


It is packed, bool uses one byte, we are wasting 7 bytes at minimum.

- Re-reads


Help the compiler to prevent it from doing unecessary re-reads.

```
// Re-read m_NeedParentUpdate
int
Foo::Bar(int count)
{
    int value = 0;
    for (int i = 0; i < count; ++i)
    {
        if (m_NeedParentUpdate)
        {
            ++value;
        }
    }
    return (value);
}
```

```
// Better version
int
Foo::Bar(int count)
{
    int     value = 0;
    bool    need_update = m_NeedParentUpdate;

    if (m_NeedParentUpdate)
    {
        for (int i = 0; i < count; ++i)
        {
            if (m_NeedParentUpdate)
            {
                ++value;
            }
        }
    }
    return (value);
}
```
Don't re-read member values or re-call functions when you already have the data.

Hoist all loop-invariant reads and branches. Even super-obvious ones that should already be in registers.

- Extremely low information density


Actual work is very small compared to the work done around it. Large overhead.
- Over-generalization


Complex constructors tend to imply that

\- Reads are unmanaged (one at a time)

\- Unnecessary reads/writes in destructors

\- Unmanaged instruction cache(virtuals)

\- Unnecessarily complex state machine. 2^(number of bools) states


Rule of thumb: Store each state separately instead of storing them in a single object.
- Undefined or under-defined constraints


Rule of thumb: The best code is code that doesn't need to be exist. Do it offline and once.
- Over-solving (computing too much)

### Good News
Most problems are easy to see.

Side-effect of solving the 90% well, compiler can solve the 10% better.

Organized data makes debbuging, maintenance and concurrency much easier.

### Bad News
Good programming is hard, bad programming is easy.

### C++
Good: Enough tools to reason about most important part of the problem (memory/data)

Bad: A culture that thinks that ignoring the real problem is a good thing.

### Resource
[CppCon 2014: Mike Acton "Data-Oriented Design and C++"](https://www.youtube.com/watch?v=rX0ItVEVjHc&t=285s)

[Optimizable Code](https://deplinenoise.wordpress.com/2013/12/28/optimizable-code/)

[Design patterns are from hell!](https://realtimecollisiondetection.net/blog/?p=44)

[Design patterns are from hell^2!](https://realtimecollisiondetection.net/blog/?p=81)
