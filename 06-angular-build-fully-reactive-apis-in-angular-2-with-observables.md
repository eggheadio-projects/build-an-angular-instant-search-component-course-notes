# [06 - Build fully reactive APIs in Angular 2 with Observables](https://egghead.io/lessons/angular-build-fully-reactive-apis-in-angular-2-with-observables)

## Dealing with Deprecations (and other problems)
Last lesson! The operators copied from **app.component.js** need to be inserted in a .pipe method in the search function, like so:
```javascript
search(terms: Observable<string>, debounceMs = 400) {
    return terms.pipe(
    debounceTime(debounceMs),
    distinctUntilChanged(),
    switchMap(term => this.rawSearch(term))
  )
}
```
If you noticed, I passed debounceMs into debounceTime() instead of 400. I think this is what the instructor meant to do, anyway. Also, I wrote the function rawsearch() as rawSearch() - it just felt more natural!

Next, your Observable import should look like:
```javascript
import { Observable } from 'rxjs';
```
Instead of:
```javascript
import { Observable } from 'rxjs/Observable';
```
Finally, my imports in **app.component.ts** were not being shared application-wide, so I simply moved
```javascript
import { map, debounceTime, distinctUntilChanged, switchMap } from "rxjs/operators";
```
to **wikipedia-search.service.ts**. If you know why this is the case, please contribute!
## Notes
- The ability to pass in Observables as arguments allows us to hide a lot of code behind a service!
## Resources
- [Parker's Updated Angular 9 Code (Lesson 6)](https://github.com/ParkerGits/build-an-angular-instant-search-component/tree/06-angular-build-fully-reactive-apis-in-angular-2-with-observables)
- [Importing Observable RxJS](https://stackoverflow.com/a/56431681)
- [Using Operators in RxJS 6](https://academind.com/learn/javascript/rxjs-6-what-changed/#using-operators-in-rxjs-6)
