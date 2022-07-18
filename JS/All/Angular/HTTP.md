## Http

```ts
import { HttpClient, HttpHeaders } from '@angular/common/http';
```
Inject in constructor `private http: HttpClient`

 An Observable from HttpClient always emits a single value and then completes.
 HttpClient.get returns the body of the response as an untyped JSON object by default. Applying the optional type specifier, <Hero[]> , gives you a typed result object.
All HttpClient methods return an RxJS Observable of something
```ts
return this.http.get<Hero[]>('api/heroes');
```
To make parameterized urls `${this.heroesUrl}/${id}`

Update
```ts
const httpOptions = {
  headers: new HttpHeaders({ 'Content-Type': 'application/json' })
};

this.http.put(this.heroesUrl, hero, this.httpOptions)
```
##### Error Handling

catchError passes an error handler
```ts
import { catchError, map, tap } from 'rxjs/operators';

return this.http.get<Hero[]>(this.heroesUrl)
  .pipe(
    catchError(this.handleError('getHeroes', []))
  );
```

* Handle Http operation that failed.
* Let the app continue.
* @param operation - name of the operation that failed
* @param result - optional value to return as the observable result

```ts
private handleError<T> (operation = 'operation', result?: T) {
  return (error: any): Observable<T> => {
    console.error(error); // log to console instead
    this.log(`${operation} failed: ${error.message}`);
    return of(result as T);
  };
}
```
