# [04 - Combine Observables in Angular 2 with flatMap](https://egghead.io/lessons/angular-combine-observables-in-angular-2-with-flatmap)

## Dealing with Deprecation

Another operator has been introduced, and so it can be imported accordingly:
```javascript
import { map, debounceTime, distinctUntilChanged, mergeMap } from "rxjs/operators";
```
In the lesson, he calls the method flatMap(). The operator is now only called mergeMap(), just like it is called on import. mergeMap is added to our .pipe() method like so:
```javascript
this.term$.pipe(
  debounceTime(400),
  distinctUntilChanged(),
  mergeMap(term => this.service.search(term)),
).subscribe(results => this.items = results);
```
You can now remove the original search() function!
## Notes
- Using mergeMap() allows us to clean up our code by removing the needs for two .subscribe() methods. Read more on mergeMap [here](https://rxjs-dev.firebaseapp.com/api/operators/mergeMap).
## Resources
- [Parker's Updated Angular 9 Code (Lesson 4)](https://github.com/ParkerGits/build-an-angular-instant-search-component/tree/04-angular-combine-observables-in-angular-2-with-flatmap)
- [RxJS mergeMap operator](https://rxjs-dev.firebaseapp.com/api/operators/mergeMap)
- [Using Operators in RxJS 6](https://academind.com/learn/javascript/rxjs-6-what-changed/#using-operators-in-rxjs-6)
