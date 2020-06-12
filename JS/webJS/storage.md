# Storage

### Web Storage

- **sessionStorage** maintains a separate storage area for each given origin that's available for the duration of the page session (as long as the browser is open, including page reloads and restores)
  - Stores data only for a session, meaning that the data is stored until the browser (or tab) is closed.
  - Data is never transferred to the server.
  - Storage limit is larger than a cookie (at most 5MB).
- **localStorage** does the same thing, but persists even when the browser is closed and reopened.
  - Stores data with no expiration date, and gets cleared only through JavaScript, or clearing the Browser cache / Locally Stored Data.
  - Storage limit is the maximum amongst the three.

```javascript
localStorage.setItem('myCat', 'Tom');

const cat = localStorage.getItem('myCat');
const cat = localStorager.myCat;
const cat = localStorager["myCat"];

localStorage.removeItem('myCat');

localStorage.clear();
```

### Index DB

New web tech to store large files

[Storage limits](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Browser_storage_limits_and_eviction_criteria), global limit is 50% of free disk space and group/domain limit is 20% of that with a minium of 10MB and 2GB

