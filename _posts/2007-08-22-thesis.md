---
title: "<i>Analyzing Security Advice in Functional Aspect-oriented Programming Languages</i> presented as Ph.D thesis at Princeton Computer Science"
description: "This thesis extends functional programming languages with aspect-oriented features, primarily to explore aspect-oriented enforcement of security policies."
author: Daniel Dantas
# redirect: https://www.cs.princeton.edu/research/techreps/TR-795-07"
---

## [🔗Princeton CS](https://www.cs.princeton.edu/research/techreps/488) | [📄pdf](https://www.cs.princeton.edu/techreports/2007/795.pdf)

> This thesis extends [functional programming languages](https://en.wikipedia.org/wiki/Functional_programming) with [aspect-oriented features](https://en.wikipedia.org/wiki/Aspect-oriented_programming), primarily to explore aspect-oriented enforcement of [security policies](https://en.wikipedia.org/wiki/Computer_security_policy).

> First, this thesis examines an aspect-oriented implementation of the [Java security mechanism](https://en.wikipedia.org/wiki/Security_of_the_Java_software_platform), which requires the security advice to be triggered by functions with diverse types. I present a new language, AspectML, that allows type-safe [polymorphic](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)) advice using pointcuts constructed from a collection of polymorphic join points. I then compare my AspectML implementation of the Java security mechanism against the existing Java implementation. 

> Second, in ordinary aspect-oriented programming, security and other advice added after-the-fact to an existing codebase can disrupt important [data invariants](https://en.wikipedia.org/wiki/Invariant_(mathematics)#Invariants_in_computer_science) and prevent local reasoning. Instead, this thesis shows that many common aspects, including security advice, can be implemented as harmless advice. Harmless advice uses a novel [type and effect system](https://en.wikipedia.org/wiki/Effect_system) related to [information-flow type systems](https://en.wikipedia.org/wiki/Information_flow_(information_theory)#Security_type_system) to ensure that harmless advice cannot modify the behavior of mainline code. To demonstrate the usefulness of harmless advice for security, I implement many of the security examples used by the Naccio execution monitoring system as harmless advice.

> Finally, this thesis expands the harmless advice specification to allow programmers to create interference policies to define how system libraries can be used by aspects. These policies use a combination of compile-time type checking and run-time monitoring to enforce the desired degree of harmlessness on the aspect-oriented program. My thesis formalizes an idealized file I/O library and proves that an interference policy specified by our policy language can continue to enforce our original view of harmlessness for advice that uses file I/O.
