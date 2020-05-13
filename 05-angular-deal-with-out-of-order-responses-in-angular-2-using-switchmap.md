# [05 - Deal with out of order responses in Angular 2 using switchMap](https://egghead.io/lessons/angular-deal-with-out-of-order-responses-in-angular-2-using-switchmap)

## Dealing with Deprecation
Surprise, surprise! Another operator! To import, simply replace mergeMap with switchMap in your import:
```javascript
import { map, debounceTime, distinctUntilChanged, switchMap } from "rxjs/operators";
```
and in the .pipe method():
```javascript
constructor(private service: WikipediaSearchService) {
this.term$.pipe(
  debounceTime(400),
  distinctUntilChanged(),
  switchMap(term => this.service.search(term)),
).subscribe(results => this.items = results);
```
Simple!
## Notes
- The instructor demonstrates the bug that a response for one search can potentially override the response for another.
- switchMap() allows us to get rid of this bug by automatically unsubscribing from the Observable that was previously mapped to.
## Resources
- [Parker's Updated Angular 9 Code (Lesson 5)](https://github.com/ParkerGits/build-an-angular-instant-search-component/tree/05-angular-deal-with-out-of-order-responses-in-angular-2-using-switchmap)
- [Using Operators in RxJS 6](https://academind.com/learn/javascript/rxjs-6-what-changed/#using-operators-in-rxjs-6)
