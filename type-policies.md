```ts
const cache = new InMemoryCache({
  typePolicies: {
    StudyActivity: {
      fields: {
        selected: {
          read(cachedValue, fieldObj) {
            const { readField } = fieldObj;
            // https://www.apollographql.com/docs/react/caching/cache-field-behavior/#fieldpolicy-api-reference
            // Helper function for reading other fields within the current object.
            // If a foreign object or reference is provided, the field will be read
            // from that object instead of the current object, so this function can
            // be used (together with isReference) to examine the cache outside the
            // current object. If a FieldNode is passed instead of a string, and
            // that FieldNode has arguments, the same options.variables will be used
            // to compute the argument values. Note that this function will invoke
            // custom read functions for other fields, if defined. Always returns
            // immutable data (enforced with Object.freeze in development).
            const id = readField('id'); // <--- read field within the 'current' object, no other params are required
            return cachedValue ? cachedValue : false;
          },
        },
      },
    },
  },
});
```
