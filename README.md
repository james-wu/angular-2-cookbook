# angular-2-cookbook
* Source code for Angular 2 Cookbook
* markdown cheat sheet https://guides.github.com/features/mastering-markdown/
# Chapter 2 
* 1315 Configuring Mutual Parent-Child Awareness with ViewChild and forwardRef
* 2048 Utilizing Component Lifecycle Hooks
* 3211 Using ngFor and ngIf Structural Directives for Model-based DOM Control ngForOf
* 3292 Attaching Behavior to DOM Elements with Directives
* 4437 Registering Handlers on Native Browser Events
* 4907 Referencing a Parent Component from a Child Component
* 5094 Referencing Elements with Template Variables
* 6172 Projecting Nested Content Using ngContent 
* 6543	Passing Members From a Parent Component Into a Child Component
* 6577	Using Decorators to Build and Style a Simple Component
* 7386	Configuring Mutual Parent-Child Awareness with ContentChild and forwardRef
* 8313	Binding to Native Element Attributes
* 8565	Binding to Native Element Attributes
* 8611 Generating and Capturing Custom Events Using EventEmitter

# Chapter 3
* 0771 Implementing simple two-way data binding with ngModel
* 2816 Bundling FormControls with a FormArray
* 3052 Bundling Controls with a FormGroup
* 4076 Implementing basic field validation with formControl
* 5116 Implementing basic forms with NgForm
* 7811 Creating and using a custom asynchronous validator with Promises
* 8574 Creating and using a custom validator
* 9302 Implementing basic forms with FormBuilder and formControlName

# Chapter 4
* 0905 Converting an Http Service Observable into a ZoneAwarePromise

* 4362 Cancelling Asynchronous Actions with Promise.race()
* 5195 Understanding and Implementing Basic Promises
* 5244 Converting a Promise into an Observable
* 6828 Chaining Promises and Promise Handlers
* 8496 Implementing Promise Barriers with Promise.all()
* 9315 Creating Promise Wrappers with Promise.resolve() and Promise.reject()

# Chapter 5
* 2417 Building a Generalized Publish-Subscribe Service to Replace $broadcast, $emit, and $on
* 4112 Using QueryLists and Observables to Follow Changes in ViewChildren
  
```javascript
constructor(private changeDetectorRef_:ChangeDetectorRef) {}
ngAfterViewInit() {
    this.innerComponents.changes
      .subscribe(innerComponents => {
        this.lastVal = (innerComponents.last || {}).val;
        this.changeDetectorRef_.detectChanges();
      });
  }

```
* 4121 Basic Utilization of Observables with Http
* 4839 Implementing a Publish-Subscribe Model using Subjects
* 6957 Creating an Observable Authentication Service using BehaviorSubjects
* 8629 Building a Full-Featured AutoComplete with Observables
```javascript
constructor(private apiService_:APIService) {
    this.queryField.valueChanges
      .debounceTime(200)
      .distinctUntilChanged()
      .switchMap(query => this.apiService_.search(query))
      .subscribe(result => this.results.push(result));
  }

@Injectable()
export class APIService {
  constructor(private http_:Http) {}
  
  search(query:string):Observable<string> {
    return this.http_
      .get('static/response.json')
      .map(r => r.json()['prefix'] + query)
      .concatMap(
        x => Observable.of(x).delay(Math.random()*1000));
  }
}
```

# Chapter 6
* 1355 Selecting a LocationStrategy for Path Construction
```javascript
import {LocationStrategy, HashLocationStrategy} 
providers: [
    {provide: LocationStrategy, useClass: HashLocationStrategy}
  ],

```

* 3308 Building Stateful Route Behavior with RouterLinkActive
```javascript
@Component({
  selector: 'root',
  template: `
    <h1>Root component</h1>
    <a [routerLink]="['']"
       [routerLinkActive]="'active-navlink'"
       [routerLinkActiveOptions]="{exact:true}">Default</a>
    <a [routerLink]="['article']"
       [routerLinkActive]="'active-navlink'"
       [routerLinkActiveOptions]="{exact:true}">Article</a>
    <router-outlet></router-outlet>
  `,
  styles: [`
    .active-navlink {
      color: red; 
      text-transform: uppercase;
    }
  `]
})
export class RootComponent {}



import {Component, Input, ngOnInit, ChangeDetectionStrategy, ChangeDetectorRef} from '@angular/core';
import {Observable} from 'rxjs/Observable';

@Component({
  selector: 'article',
  template: `
    <h1>{{title}}</h1>
    <p>Shares: {{count}}</p>
  `,
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class ArticleComponent implements OnInit {
  @Input() shares:Observable<Event>;
  count:number = 0;
  title:string = 
    'Insurance Fraud Grows In Wake of Apple Pie Hubbub';
    
  constructor(private changeDetectorRef_: ChangeDetectorRef) {}
    
  ngOnInit() {
    this.shares.subscribe((e:Event) => {
      ++this.count;
      this.changeDetectorRef_.markForCheck();  
    });
  }
}

```
* 4553 Working with Matrix URL Parameters and Routing Arrays

