# Agility Techniques

# Code-Size Reduction Tactics

1. **DRY (Don’t Repeat Yourself)**:
   - Allow up to two repetitions before creating abstractions.
   - DRY applies across all levels, from low-level code to high-level concepts.
1. **Consistency**:
   - Uniform naming conventions (e.g., `lowerCamelCase` for functions, `UpperCamelCase` for classes).
   - Align file and directory structures with module structures to maximize modularity.

## Standardized Everything

### Standard Data Shapes

Anti-pattern: different set of fields from the same record returned for each different API endpoint. GraphQL is a productivity disaster for this reason.

Instead, use one data shape, one data structure for the same record type everywhere. Generally, if you are creating an API, then I recommend JSON as the standard: over the wire, in-memory server-side, in-memory client-side. This standardization maximizes code-reuse and minimizes code-size.

But how do you solve the problem of sending a lot of unused fields over the wire? Simple - keep each record as simple as possible. If you need a complex record, break it out into separate, 1:1 linked tables. That way the client can request the extra records as needed without breaking the data-shape consistency.

#### Side-Channel instead of Inline Linked Data

I prefer, unlike most all ORMs, to **not** inline linked records. Linked records also breaks data-shape consistency since the linked record may or may-not be present depending on the query. My strong preference is to return linked record data on a side-channel. If done right it still all comes over the wire in a single JSON response, and the client-side code can immediately access the linked record data simply if the client-side ORM is "good." (Ahem, Art-ery is how I solved this problem.)

Side-channel data over the wire might look like this:

```json
{
  "data": [
    {
      "id": "abc",
      // the main record data - either a single record or a list of records
      "user": "123",
      "order": "456"
    },
    {
      "id": "def",
      "user": "123", // note, the user is the same as above, but only one copy of the user is sent over the wire
      "order": "789"
    }
  ],
  "linked": {
    // the linked record data - either a single record or a list of records
    "users": { "123": { "name": "John Doe", "email": "john.doe@example.com" } },
    "orders": {
      "456": { "name": "Order 456", "amount": 100, "status": "pending" },
      "789": { "name": "Order 789", "amount": 200, "status": "pending" }
    }
  }
}
```

Side-channel data also has some other benefits:

- it allows for circular references
- it only sends one copy of each record
- it makes data-shape 100% consistent across the entire stack

### Simplified, Standardized Data Types

Most data structures are actually pretty simple. For the DB in particular, standardize on a minimal set of data types you are going to use and be reluctant to add more. E.g. numbers (choose just one number type if you can), strings, one date type, boolean. I also generally recommend your DB conform to JSON as much as possible to make the rest of your stack simpler.

# Modular Design Tactics
