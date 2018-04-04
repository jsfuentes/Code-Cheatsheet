## HTML:
##### Interpolation

```html
<div> {{title}} </div>
<div> {{title | uppercase }} </div>
```

`| uppercase` = a pipe

##### Two way binding

In app.module.ts and added to import list:
```ts
import { FormsModule } from '@angular/forms';  
```

In html:
```html
<label>name:
  <input [(ngModel)]="hero.name" placeholder="name">
</label>
```


##### Loops
```html
<ul class="heroes">
  <li *ngFor="let hero of heroes">
	  	{{hero.id}}
  </li>
</ul>
```

##### Event Binding
OnSelect defined in ts for this component
```html
<div (click)="onSelect(hero)">  
<button (click)="add(heroName.value); heroName.value=''">
  add
</button>
```


##### If

if selectedHero exists/defined
```html
<div *ngIf="selectedHero">
```


##### Conditional Classes
```html
[class.some-css-class]="some-condition"
<li [class.selected]="hero === selectedHero"> hi </li>
```

##### Property Binding(used with [@Input](#input) )
```html
<component [hero]="selectedHero"> </component>
```
