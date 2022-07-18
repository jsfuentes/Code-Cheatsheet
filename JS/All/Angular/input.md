##### input
```html
<div>
  <label>Hero name:
    <input #heroName />
  </label>
  <!-- (click) passes input value to add() and then clears the input -->
  <button (click)="add(heroName.value); heroName.value=''">
    add
  </button>
</div>
```

#####  @Input <a name="input"></a>

Getting input into component
```ts
@Input() hero: Hero;
```
