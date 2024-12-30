# Agility Techniques

1. **DRY (Don’t Repeat Yourself)**:
   - Allow up to two repetitions before creating abstractions.
   - DRY applies across all levels, from low-level code to high-level concepts.
1. **Consistency**:
   - Uniform naming conventions (e.g., `lowerCamelCase` for functions, `UpperCamelCase` for classes).
   - Align file and directory structures with module structures to maximize modularity.
1. **Database Design**:
   - Keep individual records reasonable in size; split larger fields into associated tables.
1. **JSON as the Standard**:
   - Maintain a consistent JSON structure across database, server, wire, and client.

# Verifiability Techniques

1. **Test from the Outside**:
   - Start at the highest module level and verify the product requirements are met.
   - Drill down only when necessary. If the highest-level requirement validation becomes difficult, then drill down one tier to the next level of modules and write tests for one or more of them.
2. **Pure Functions**:
   - Separate functional logic from integrations for easier testing and modular design.
   - Apply this principle to testing user interfaces by isolating logic from direct interactions.
