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

##### Observable:

In service, observable that emits a single value, array of HEROES

```ts
import { Observable } from 'rxjs/Observable';
import { of } from 'rxjs/observable/of';

getHeroes(): Observable<Hero[]> {
  return of(HEROES);
}
```

To use in another component, notice the callback
```ts
this.heroService.getHeroes()
        .subscribe(heroes => this.heroes = heroes)
```

If you neglect to subscribe(), the service will not send the delete request to the server! As a rule, an Observable does nothing until something subscribes!
