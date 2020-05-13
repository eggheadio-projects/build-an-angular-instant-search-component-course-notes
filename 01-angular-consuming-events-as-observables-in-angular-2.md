# [01 - Consuming events as Observables in Angular 2](https://egghead.io/lessons/angular-consuming-events-as-observables-in-angular-2)

## Creating a new Angular project

In order to create a new Angular project, first install [Angular CLI](https://cli.angular.io/) through npm in the terminal.
```
npm install -g @angular/cli
```
Then navigate to a folder of choice in the terminal and run
```
ng new build-an-angular-instant-search-component
```
Routing is not needed for this project. Next, navigate to this project folder via
```
cd build-an-angular-instant-search-component
```
and run
```
ng serve
```

You can also clone [Parker's Angular Version 9 Respository](https://github.com/ParkerGits/build-an-angular-instant-search-component) for a project that works using the latest version of Angular (as of 5/8/2020). The code for each lesson resides in its respective branch. The following section details the changes made between the [transcript code](https://codesandbox.io/s/54xv161qq4?from-embed) and Parker's code.

## Dealing with Deprecation

Between Angular version 7 in the [transcript code](https://codesandbox.io/s/54xv161qq4?from-embed) and Angular version 9, a lot has deprecated.

The following are the changes that were made to the code above in order to get our search component working. The [resources](#resources) section contains resources detailing changes and updates to dependencies. And yes, the number of changes you need to make before your code compiles is reduced drastically after this lesson.

### app.component.ts

In the imports on line 3, we change
```javascript
import { Subject } from "rxjs/Subject";
```
to
```javascript
import { Subject } from "rxjs";
```

and on line 6:
```javascript
import "rxjs/add/operator/map";
```
to
```javascript
import { map } from "rxjs/operators";
```

On line 9, remove
```javascript
moduleId: module.id,
```

### app.module.ts

Replace line 4
```javascript
import { JsonpModule } from "@angular/http";
```
with
```javascript
import { HttpClientModule, HttpClientJsonpModule } from "@angular/common/http";
```
and line 10
```javascript
imports: [BrowserModule, JsonpModule],
```
with
```javascript
imports: [BrowserModule, HttpClientModule, HttpClientJsonpModule],
```

### wikipedia-search.service.ts
Change line 2 from
```javascript
import { URLSearchParams, Jsonp } from "@angular/http";
```
to
```javascript
import { HttpClient } from "@angular/common/http";
```
and line 3 replace
```javascript
import "rxjs/add/operator/delay";
```
with
```javascript
import { map } from "rxjs/operators";
```
Finally, our injectable, instead of looking like
```javascript
@Injectable()
export class WikipediaSearchService {
  constructor(private jsonp: Jsonp) {}

  search(term: string) {
    let search = new URLSearchParams();
    search.set("action", "opensearch");
    search.set("search", term);
    search.set("format", "json");

    return this.jsonp
      .get("https://en.wikipedia.org/w/api.php?callback=JSONP_CALLBACK", {
        search
      })
      .map(response => response.json()[1]);
  }
}
```
should look like
```javascript
@Injectable()
export class WikipediaSearchService {
  constructor(private http: HttpClient) {}
  search(term: string) {
    let url = "https://en.wikipedia.org/w/api.php?action=opensearch&search=" + term + "&format=json"
    return this.http
      .jsonp(url, 'callback')
      .pipe(map(response => response[1]));
  }
}
```
With these changes, your code will be caught up with the instructor's code at the end of lesson one!

## Notes
- "Some people use a dollar suffix to indicate that a variable is an observable."
- The next lessons will teach us how to improve our application's efficiency and performance!
- When I used [Stackblitz](https://stackblitz.com/) to edit my code, I would get [this error](https://stackoverflow.com/questions/44321326/property-value-does-not-exist-on-type-eventtarget-in-typescript/44321394). Try using a local Angular CLI project if you're having trouble with online code editors, too.

## Resources
- [Parker's Updated Angular 9 Code (Lesson 1)](https://github.com/ParkerGits/build-an-angular-instant-search-component/tree/01-angular-consuming-events-as-observables-in-angular-2)
- [Deprecation of JsonpModule in Angular](https://stackoverflow.com/a/47643846)
- [TypeScript error in Angular2 code: Cannot find name 'module'](https://stackoverflow.com/questions/36700693/typescript-error-in-angular2-code-cannot-find-name-module)
- [RxJS 6 - What Changed?](https://academind.com/learn/javascript/rxjs-6-what-changed/)
- [Angular HttpClient](https://angular.io/api/common/http/HttpClient)
