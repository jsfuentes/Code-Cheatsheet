## TypeScript:

##### Classes
In a hero.ts file, then import it everywhere you use it
```ts
export class Hero {
  id: number;
  name: string;
}
```

##### Services:

`providers: [HeroService]` in app.module.ts

```ts
constructor(private heroService: HeroService) {
}

ngOnInit() {
  this.heroes = this.heroService.getHeroes();
}
```

- In a class, public if you use it in the html or something
- Define getHeroes in the service
