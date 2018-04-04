#### Cool Counters
Note counter has to be after it incremented
```css
body {counter-reset: invalidCount; }
:invalid { counter-increment: invalidCount; }
p:before { content: "you have " counter(invalidCount) " invalid entries"; }
```
