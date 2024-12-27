# IDs

Which ids to use in a DB?

Recommended: 

- CUID2, if being hardcore smarts
- if you don't need cross-host unique ids or security, use whatever is easiest in your language/framework not autoincrementing
- try to add Stripe 1-2 letters underscore for readability

## Options

- Autoincrementing Ids
  - easy to guess ids
  - cant generate the id before you write the data, ie distributed systems or clientside generated ids need full round trip to update local id
- UUID
  - 36 chars, 32 hexadecimal and 4 hyphens
  - don't use uuidv1-v5, uuidv8 is for custom uuids, v6 has MAC address privacy concerns but useable
  - **UUIDv7**
    - Starts with timestamp, so timesortable and good for db indexing,
- CUID2 (Security focus)
  - 25 chars, consisting of a mix of timestamp, counter, client fingerprint, and random values
    - contains only lowercase letters and the numbers
  - Shorter, more collision resistant, and more secure/leaks less info then uuid, infeasible to guess next id
- Nanoid (small focus)
  - 21 chars, use more letters than uuid
  - url safe, 2x as fast as uuid generation, not time ordered, as collision resistant as uuid
- ULID (Universally Unique Lexicographically Sortable Identifie)
  - Lexicographically sortable.
  - 26 characters
