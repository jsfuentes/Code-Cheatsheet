## Observables
```html
<li *ngFor="let hero of heroes$ | async" >
```
The $ is a convention that indicates heroes$ is an Observable, not an array.

The \*ngFor can't do anything with an Observable. But there's also a pipe character (|) followed by async, which identifies Angular's AsyncPipe.

The AsyncPipe subscribes to an Observable automatically so you won't have to do so in the component class.

##### Search
```ts
<input #searchBox id="search-box" (keyup)="search(searchBox.value)" />
```

##### Tap Observables
The RxJS tap operator, which looks at the observable values, does something with those values, and passes them along. The tap call back doesn't touch the values themselves.
```ts
[Observable].pipe(
  tap(heroes => this.log(`fetched heroes`)),
  catchError(this.handleError('getHeroes', []))
)
```

##### Search
```ts
import {
   debounceTime, distinctUntilChanged, switchMap
 } from 'rxjs/operators';


private searchTerms = new Subject<string>();

// Push a search term into the observable stream.
search(term: string): void {
  this.searchTerms.next(term);
}

ngOnInit(): void {
  this.heroes$ = this.searchTerms.pipe(
    // wait 300ms after each keystroke before considering the term
    debounceTime(300),

    // ignore new term if same as previous term
    distinctUntilChanged(),

    // switch to new search observable each time the term changes
    switchMap((term: string) => this.heroService.searchHeroes(term)),
  );
}
```
A Subject is both a source of observable values and an Observable itself. You can subscribe to a Subject as you would any Observable.

You can also push values into that Observable by calling its next(value) method as the search() method does.

switchMap() calls the search service for each search term that makes it through debounce and distinctUntilChanged. It cancels and discards previous search observables, returning only the latest search service observable.
