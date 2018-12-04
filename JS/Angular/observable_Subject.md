## Observables

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

```html
<li *ngFor="let hero of heroes$ | async" >
```
The $ is a convention that indicates heroes$ is an Observable, not an array.

The \*ngFor can't do anything with an Observable. But there's also a pipe character (|) followed by async, which identifies Angular's AsyncPipe.

The AsyncPipe subscribes to an Observable automatically so you won't have to do so in the component class.

## Subject vs Observable?
Unique features of a subject are:
- observer & observable so you can also send values to a subject in addition to subscribing to it.

BehaviorSubject is a type of subject, a subject is a special type of observable so you can subscribe to messages like any other observable. The unique features of BehaviorSubject are:
- needs initial value
- returns the last value of the subject upon subscription
- `getValue()` retrieve the last value of the subject


##### Tap Observables
The RxJS tap operator, which looks at the observable values, does something with those values, and passes them along. The tap call back doesn't touch the values themselves.
```ts
[Observable].pipe(
  tap(heroes => this.log(`fetched heroes`)),
  catchError(this.handleError('getHeroes', []))
)
```

##### Search
```html
<input #searchBox id="search-box" (keyup)="search(searchBox.value)" />
```

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
