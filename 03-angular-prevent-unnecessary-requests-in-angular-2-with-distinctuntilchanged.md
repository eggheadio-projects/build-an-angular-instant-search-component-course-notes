# [03 - Prevent unnecessary requests in Angular 2 with distinctUntilChanged](https://egghead.io/lessons/angular-prevent-unnecessary-requests-in-angular-2-with-distinctuntilchanged)

## Dealing with Deprecation

Like with debounceTime(), distinctUntilChanged() is an operator and will need to be handled differently in RxJS 6.

First, add distinctUntilChanged to your operator imports:
```javascript
import { map, debounceTime, distinctUntilChanged } from "rxjs/operators";
```
Now, in the pipe method, add distinctUntilChanged() after debounceTime():
```javascript
this.term$.pipe(
  debounceTime(400),
  distinctUntilChanged(),
).subscribe(term => this.search(term));
```
## Notes
- The RxJS distinctUntilChanged() operator filters out duplicate inputs and further decreases network usage.
- The RxJS .pipe() method allows us to list the operators that we will be "piping" to the Observable.
## Resources
- [Parker's Updated Angular 9 Code (Lesson 3)](https://github.com/ParkerGits/build-an-angular-instant-search-component/tree/03-angular-prevent-unnecessary-requests-in-angular-2-with-distinctuntilchanged)
- [Using Operators in RxJS 6](https://academind.com/learn/javascript/rxjs-6-what-changed/#using-operators-in-rxjs-6)
