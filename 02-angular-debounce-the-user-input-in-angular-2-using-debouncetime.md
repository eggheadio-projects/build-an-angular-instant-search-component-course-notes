# [02 - Debounce the user input in Angular 2 using debounceTime](https://egghead.io/lessons/angular-debounce-the-user-input-in-angular-2-using-debouncetime)

## Dealing with Deprecation

debounceTime() is an RxJS operator, and RxJS operators are handled differently in RxJS 6.

We can import debounceTime in the same line as we imported map:
```javascript
import { map, debounceTime } from "rxjs/operators";
```
Another change to RxJS operators is that they are applied through the .pipe() method. To learn more about .pipe(), take a look at [Using Operators in RxJS 6](https://academind.com/learn/javascript/rxjs-6-what-changed/#using-operators-in-rxjs-6). The code we write to apply .debounceTime() to our program is as follows:
```javascript
this.term$.pipe(debounceTime(400)).subscribe(term => this.search(term));
```
## Notes
- Through debounceTime(), we can create gaps of time when our program will not update and effectively decreasing network usage.
- RxJS operators are very effective. It's all about finding the right one for the job. The official list and documentation of RxJS operators can be found [here](https://rxjs-dev.firebaseapp.com/guide/operators).
## Resources
- [Parker's Updated Angular 9 Code (Lesson 2)](https://github.com/ParkerGits/build-an-angular-instant-search-component/tree/02-angular-debounce-the-user-input-in-angular-2-using-debouncetime)
- [Using Operators in RxJS 6](https://academind.com/learn/javascript/rxjs-6-what-changed/#using-operators-in-rxjs-6)
- [RxJS Operators Documentation](https://rxjs-dev.firebaseapp.com/guide/operators)
