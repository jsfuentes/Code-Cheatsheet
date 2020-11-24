# Migration

Use https://github.com/airbnb/ts-migrate

```
npx ts-migrate init . 
npx ts-migrate rename .
npx ts-migrate migrate .
npx ts-migrate reignore .
```



1) Create tsconfig

2) Rename files to .js => .ts

3) Run ts-migrate plugins

4) Add to [webpack](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html#webpack)

5) Reignore? all errors or fix