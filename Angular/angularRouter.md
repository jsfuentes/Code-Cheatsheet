## Routes

The RouterOutlet is one of the router directives that became available to the AppComponent because AppModule imports AppRoutingModule which exported RouterModule. It tells the html where to display the routed html.
```html
<router-outlet></router-outlet>
```

##### Create a link
```html
<nav>
  <a routerLink="/heroes">Heroes</a>
</nav>
```

##### Create a parameterized link
```html
<routerLink="/detail/{{hero.id}}">
```

##### Routes
```ts
import {RouterModule, Routes } from '@angular/router';
import { HeroesComponent } from './heroes/heroes.component';
```

```ts
const routes: Routes = [
  { path: 'heroes', component: HeroesComponent },
  { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
  { path: 'detail/:id', component: HeroDetailComponent },
];
```

- regular
- default route
- parameterized

```ts
@NgModule({
imports: [ RouterModule.forRoot(routes) ],
	  exports: [ RouterModule ]
})
export class AppRoutingModule {}
```

Detect parameters in component
```ts
import { ActivatedRoute } from '@angular/router';
import { Location } from '@angular/common';
```
Inject ActivatedRoute which hold info about route and location interacts with the browser. The `+` turn the string into an integer
```ts
constructor(
  private route: ActivatedRoute,
  private location: Location
)

ngOnInit() {
  const id = +this.route.snapshot.paramMap.get('id');
}
```

##### Going Back
```html
goBack(): void {
  this.location.back();
}
```
