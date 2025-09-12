
2025-08-17 17:41

Status:

Tags: [Article](3%20-%20Tags/Article.md)

---
# AHA Programming
https://kentcdodds.com/blog/aha-programming

[DRY (an acronym for "Don't Repeat Yourself")](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

> Every piece of knowledge must have a single, unambiguous, authoritative representation within a system

- The problem with multiple instances of same code is, if you find a bug, add info, or generally better way of doing it, you need to change the code everywhere.

## [WET](https://kentcdodds.com/blog/aha-programming#wet)
"Write Everything Twice."
> You can ask yourself "Haven't I written this before?" two times, but never three.

## [AHA 💡](https://kentcdodds.com/blog/aha-programming#aha-) 
>  Avoid Hasty Abstractions

> Prefer duplication over the wrong abstraction


> Optimize for change first

The rationale behind "Optimize for change first" is that the future of code is uncertain; time spent optimizing for performance or creating the "best API" for an abstraction might be wasted if assumptions prove incorrect or features are no longer needed. ==The only certainty is that things will likely change, and if they don't, the code won't be touched anyway.==

Code duplication is fine if you know the use-cases for the duplicate code. Once commonalities in several instances of duplicated code "scream" for abstraction, one will be in the right mindset to create it.

 The main message of "AHA Programming" is **not to be dogmatic about when to start writing abstractions**. Instead, **write the abstraction when it** **feels** **right, and do not be afraid to duplicate code until that point**
 - Don't start with abstraction, but abstract when it feels right to abstract, you reach a point where you realize you are just repeating the code for same use case.


---
## References