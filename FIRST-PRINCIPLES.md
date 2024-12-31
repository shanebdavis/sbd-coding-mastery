# Grand Summary

## Glossary

- "Tier X principle" - we are building a hierarchy of principles based on first principles.
- "Mastery" - mastery never means you are done learning. It means you know enough about a topic to be self-directed in your infinite pursuit of improvement in that topic. When I say "master" a topic I mean a boundless path of improvement.

## _The_ Tier-1 Principle

> Solve real world problems with software with maximum impact.

## The Tier-2 Principles

To solve the Tier-1 Principle, there are only two tier-2 principles that matter for software engineering.
Forget "code quality" and "correctness", they do not provide an objective measure of success. Instead, we need to focus on the following two principles:

1. **Good Product Requirements**: TBD, but if we don't have good requirements, nothing else matters.
2. **Verifiability**: Ensure our software meets our "good requirements"
3. **Agility**: Requirements constantly change. The longer it takes to ship, the less impact we have. It's essential to be able to ship quickly with each new requirement.

## T2: Agility

> **Agility definition**: minimize the time to ship the **next** requirement and then the **next** requirement after that, etc.

### T3: Surface Area of Change

> **Surface Area of a Change Definition**: All code-tokens that must be understood, changed, and verified to meet each new requirement including, significantly, all upstream and downstream dependencies of the change - while simultaneously maximizing verifiability.

**O(n^2)**: The complexity/difficulty of the change is proportional to the number of code-tokens (n) in the "surface area of the change" _squared_.

### Surface Area of Change's Tier 4 Principles

N, the size of the surface-area, dominates the complexity of the change as complexity is proportional to the square of the surface-area. Therefor there are two key principles for maximizing agility:

1. **Master Minimizing Code Size**:
   - Simply mastering the language to minimize the number of tokens required to solve any specific problem maters immensely.
   - When in doubt selecting between two solutions, select the one that requires fewer tokens.
   - **Every token counts.**
1. **Master Modular Design**:

   - When token-count reduction hits its limits, modular design can transform dependency graphs from n² scaling to log(n) scaling.
   - A well-designed module walls off a larger implementation behind a simple interface.
   - 10x better: If the ratio of interface to implementation is 1:10, then the surface area of the change is reduced by a factor of 10.
   - O(log(n)) scaling: The winning doesn't stop there. Modular design can be applied hierarchically, nearly flat-lining complexity scaling no matter how big the system gets.
   - But, you have to master modular design.

## T2: Verifiability

> **Verifiability definition**: Ensure our software meets our "good requirements" - while simultaneously maximizing agility.

1. Test from the Outside: start at the highest module level and verify the product requirements are met.
2. Drill down only when necessary. If the highest-level requirement validation becomes difficult, then drill down one tier to the next level of modules and write tests for one or more of them.

**Automated Testing**

- Always test modules from the outside, focusing on interfaces.
- Start at the highest module level and drill down only when necessary.
- Modular testing replaces unit testing by treating modules as the unit.

## Testing Benefits

- Provides documentation for requirements.
- Drives better modular design and cleaner code.
- Enables confident, fast changes and supports semantic versioning.
- Maintains agility while ensuring verifiability with minimal overhead (~30% effort).
