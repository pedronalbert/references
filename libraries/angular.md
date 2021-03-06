# Angular
<!-- TOC -->

- [Angular](#angular)
  - [Modules](#modules)
  - [Components](#components)
    - [LyfeCycle Methods](#lyfecycle-methods)
    - [Event Dispatch](#event-dispatch)
    - [Props](#props)
      - [Validating](#validating)
      - [(Getter/Setter)](#gettersetter)
    - [Two-Way Bind Component](#two-way-bind-component)
    - [@ViewChild](#viewchild)
    - [Dynamic](#dynamic)
    - [Animations](#animations)
      - [Callbacks](#callbacks)
  - [Services](#services)
    - [HttpInterceptor](#httpinterceptor)
  - [Directives](#directives)
    - [Attribute](#attribute)
    - [Structural](#structural)
  - [Template](#template)
    - [Binding](#binding)
      - [Property Binding](#property-binding)
      - [Event Handler](#event-handler)
    - [NgClass](#ngclass)
    - [NgContent](#ngcontent)
    - [Conditional](#conditional)
      - [NgIf](#ngif)
      - [NgSwitch](#ngswitch)
    - [List](#list)
    - [Pipes](#pipes)
    - [Variables](#variables)
  - [Forms](#forms)
    - [Template Form](#template-form)
    - [Reactive Form](#reactive-form)
      - [Methods](#methods)
      - [Watch](#watch)
    - [Field](#field)
      - [Properties](#properties)
      - [State](#state)
    - [CSS Classes](#css-classes)
    - [Custom Validator](#custom-validator)
  - [Routing](#routing)
    - [Definition](#definition)
    - [Link](#link)
    - [ActivatedRoute service](#activatedroute-service)
    - [Router Events](#router-events)
    - [Guard](#guard)
      - [Types](#types)
  - [Test](#test)
    - [Pipes](#pipes-1)
    - [Components](#components-1)

<!-- /TOC -->
## Modules
```js
@NgModule({
  declarations: [], // components, directives, pipes,
  exports: [], // exportable declarations
  imports: [], // modules to import
  providers: [], // services
  entryComponents: [], // dynamic components
})
export class AppModule {
  // ...
}
```

## Components
```js
@Component({
  selector: 'users-list',
  templateUrl: './template.html',
  providers: [], // services
})
class UsersListComponent {
  //  ...
}
```

### LyfeCycle Methods
[Docs](https://angular.io/guide/lifecycle-hooks)
```js
ngOnChanges(SimpleChange)
ngOnInit()
ngDoCheck()
ngAfterContentInit()
ngAfterContentChecked()
ngAfterViewInit()
ngAfterViewChecked()
ngOnDestroy()
```

### Event Dispatch
```js
class MyComponent {
  deleteUser = new EventEmitter<User>();

  delete() {
    this.deleteUser.emit(this.user);
  }
}
```

### Props
```js
class MyComponent {
  @Input() user: User;
  @Input('master') masterName: string; // Receive master in masterName
}

// template
<my-component [user]="currentUser">
```

#### Validating
```js
class MyComponent {
  private _foo: number = 0;

  @Input('foo')
  set foo(foo: number) {
    // validations
    this._foo = foo;
  }

  get foo(): number { return this._foo; }
}
```

#### (Getter/Setter)
[Docs](https://angular.io/guide/component-interaction#intercept-input-property-changes-with-a-setter)
```js
class MyComponent {
  @Input()
  set name(name: string) {
    // ...
  }

  get name(): string {
    // ...
  }
}
```

### Two-Way Bind Component
```js
class MyComponent {
  @Input() size: number;
  @Output() sizeChange = new EventEmitter<number>();

  onChange(newSize: number) {
    this.sizeChange.emit(newSize);
  }
}
```

### @ViewChild
[Docs](https://angular.io/guide/component-interaction#parent-calls-an-viewchild)
ViewChild is a direct reference to child component
```js
import { ChildComponent } from './child-component.component';

class MyComponent {
  @ViewChild(ChildComponent)
  private childComponent: ChildComponent;

  ngAfterViewInit() {
    this.childComponent.clearForms();
  }
}
```

### Dynamic
```js
import { Component, ViewChild, ComponentFactoryResolver, ComponentRef, ViewContainerRef } from '@angular/core';

class MyComponent {
  alertRef: ComponentRef<AlertComponent>;
  @ViewChild('alertBox', {read: ViewContainerRef}) alertBox: ViewContainerRef;

  constructor(private ComponentFactoryResolver: ComponentFactoryResolver) {}

  alert() {
    if (!this.alertRef) {
      const alertComponent = this.ComponentFactoryResolver.resolveComponentFactory(AlertComponent);

      this.alertRef = this.alertBox.createComponent(alertComponent);
    }

    this.alertRef.instance.property = data; // Bind Data
    this.alertRef.changeDetectorRef.detectChanges(); // Detect Changes
  }

  destroyAlert() {
    if (this.alertRef) {
      this.alertRef.destroy();
    }
  }
}
```

```html
<!-- template -->
<ng-template #alertBox></ng-template>
```
### Animations
```js
// component.ts
import { trigger, state, style, animate } from '@angular/animations';

@Component({
  selector: 'animated-box',
  animations: [
    trigger('myAnimation', [
      state('preparing', style({ ...styles })),
      transition('void => state1', animate('100ms ease-in')),
      transition('state1 => state2', animate('0.2s ease-in')),
      transition('* <=> state2', animate('...')),
    ]),
  ],
})

// template.html
div[@myAnimation]="state"
```

#### Callbacks
```js
div(
  (@myAnimation.start)="onAnimationStart($event)"
  (@myAnimation.done)="onAnimationDone($event)"
)
```

## Services
[Docs](https://angular.io/guide/architecture-services)
```js
@Injectable()
export class HeroService { }

// component.ts
class MyComponent {
  constructor(
    private service: HeroService
  )
}
```

### HttpInterceptor
```ts
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs/Observable';
import {
  HttpEvent,
  HttpInterceptor,
  HttpResponse,
  HttpHandler,
  HttpRequest,
} from '@angular/common/http';

@Injectable()
export class MyInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const request = req.clone();

    return next
      .handle(request)
      .do(event => {
        if (event instanceof HttpResponse) {
          // ...
        }
      })
  }
}

// AppModule
import { HTTP_INTERCEPTORS } from '@angular/common/http';

providers: [
  {
    provide: HTTP_INTERCEPTORS,
    useClass: MyInterceptor,
    multi: true,
  },
],
```

## Directives
### Attribute
> You can implement lifecycle hooks and inputs
```sh
ng generate directive <path>
```
```js
@Directive({
  selector: '[myDirective]',
})
export class MyDirective {
  constructor(private el: ElementRef) {
    this.el.nativeElement; // Native DOM
  }

  @HostListener('mouseenter') onMouseEnter() {
    // ...
  }
}
```

### Structural
```js
@Directive({
  selector: '[delay]',
})
export class MyDirective {
  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef
  ) {
    this.viewContainer.createEmbeddedView(this.templateRef);
  }
}
```

## Template
[Docs](https://angular.io/guide/template-syntax)

### Binding
```js
{{ foo }} // Basic Binding
(click)="onSelect(hero)" // Event handler
(key.enter)="onKey($event)" // Event Handler with Filter
[class.selected]="present == true" // Property Binding
[(ngModel)]="hero.name" // Two-Way Data binding
```

#### Property Binding
```html
[disabled]="showDisable"
[class.special]="isSpecial"
[style.color]="color"
[style.font-size.px]="fontSize"
[attr.aria-label]="help"
```

#### Event Handler
[Docs](https://angular.io/guide/template-syntax#event-binding---event-)
```html
(change)="onChange()"
(click)="onClick(user)"
(deleteComment)="handleDeleteComment($event)
```

### NgClass
```html
[ngClass]="['one', 'two']"
[ngClass]="{active: isActive}"
```

### NgContent
> ContentChilde
```html
<div>
  <ng-content></ng-content>
  <ng-content select="my-component"></ng-content>
</div>
```

### Conditional

#### NgIf
[Docs](https://angular.io/guide/template-syntax#ngif)
```html
<div *ngIf="user"></div>
```

#### NgSwitch
```html
<div [ngSwitch]="status">
  <div *ngSwitchCase="'success'">Sucess!</div>
  <div *ngSwitchCase="'fail'">Fail!</div>
  <div *ngSwitchDefault>Waiting!</div>
</div>
```

### List 
[Docs](https://angular.io/guide/template-syntax#ngforof)
```html
<li *ngFor="let user of users"></li>
```

### Pipes
[Docs](https://angular.io/guide/pipes)
```html
{{ username | uppercase:arg1:arg2}}
```
```js
@Pipe({ name: 'uppercase' });
export class CalitalizePipe implements PipeTransform {
  transform(str: string): string {
    return str.toUpperCase();
  }
}

// template.html
{{ name | transform }}
```

### Variables
```html
<input #phone placeholder="phone number">

<button (click)="callPhone(phone.value)">Call</button>k
```

## Forms
### Template Form
```html
<form #userForm="ngForm" (ngSubmit)="onSubmit()">
  <input [(ngModel)]="model.name" />
</form>
```
```js
class FormComponent {
  model = new User('Pepe')
}
```
### Reactive Form
```ts
// component.ts
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

class MyComponent {
  myForm FormGroup;

  constructor(private fb: FormBuilder) {
    this.myForm = this.fb.group({
      name: '',
      email: ['', Validators.required],
    });
  }
}
```
```html
<!-- template.html -->
<form [formGroup]="myForm">
  <input formControlName="name" />
</form>
```

#### Methods
```ts
form.setControl(name, value);
form.setValue({
  [property]: value,
});
```

#### Watch
```ts
this.myForm.get(field)
  .valueChanges
  .subscribe(value => {
    // ...
  });
```

### Field

#### Properties
> To get a field you have to myForm.get(field_name)
```ts
.valid
.invalid
.disabled
.enabled
.errors
  .required
  .minLength
.pristine
.dirty
.touched
.untouched
```


#### State
You can access to field state with a template variable
```html
<input [(ngModel)]="model.name" #name="ngModel">

<!-- usage -->
{{ name.invalid }}
```

### CSS Classes
```txt
ng-touched ng-untouched
ng-dirty ng-pristine
ng-valid ng-invalid
```

### Custom Validator
```js
import { AbstractControl, ValidatorFn } from '@angular/forms';

export function MyValidator(): ValidatorFn {
  return (control: AbstractControl): { [key: string]: any } => {
    const value = control.value;

    return valid ? null : { foo: true };
  };
}

// directive
import { Validator, NG_VALIDATORS } from 'angular/forms';

@Directive({
  selector: '[foo][ngModel]',
  providers: [
    {
      provide: NG_VALIDATORS,
      useExisting: MyValidator,
      multi: true,
    },
  ],
})
class MyValidatorDirective implements Validator {
  private validator = MyValidator();

  validate(control: AbstractControl): { [key: string]: any } {
    return this.validator(control);
  }
}
```

## Routing

### Definition
[Docs](https://angular.io/guide/router#configuration)
```js
import { Routes, RouterModule } from '@angular/router';

const routes: Routes = [
  { path: 'login', component: LoginComponent },
  { path: '', redirectTo: '/forums', pathMatch: 'full' },
  { path: '**', component: NotFoundPage },
  {
    path: '/forums',
    component: ForumsListComponent,
    children: [
      { path: 'slug', component: ForumComponent },
    ],
  },
  // Secondary Router
  { path: 'chats', component: ChatListComponent, outlet: 'chat' },
  { path: 'chats/:userId', component: ChatComponent, outlet: 'chat' },
  // LazyLoadng
  { path: 'blogs', loadChildren: 'app/blogs/blogs.module#BlogsModule' },
];

// AppModule
providers: [
  RouterModule.forRoot(routes),
]

// ChildModule
providers: [
  RouterModule.forChild(routes),
]
```
```html
<!-- template.html -->
<router-outlet></router-outlet>
<router-outlet name="chat"></router-outlet>
```

### Link
[Docs](https://angular.io/guide/router#router-links)
```html
<!-- anchor -->
<a routerLink="/users" [queryParams]="params">

<!-- other -->
<tr routerLink="/users">
```

### ActivatedRoute service
[Docs](https://angular.io/guide/router#activated-route)
```ts
.url
.data
.paramMap
  .has(name)
  .get(name)
  .getAll(name)
  .keys()
.queryPramMap
.fragment
.outlet
.routeConfig
.parent
.firstChild
.children
```

### Router Events
[Docs](https://angular.io/guide/router#router-events)
```ts
NavigationStart
RoutesRecognized
RouteConfigLoadStart
RouteConfigLoadEnd
NavigationEnd
NavigationCancel
NavigationError
```

### Guard
```js
import { CanActivate } from '@angular/router';

@Injectable()
export class MyGuard implements CanActivate {
  canActivate() {
    return true || false;
  }
}

// routes.ts
export [ { path: '/foo', canActivate: [MyGuard] } ];
```

#### Types
```ts
CanActivate
CanActivateChild
CanDeactivate
CanLoad
Resolve
```

## Test

### Pipes
```ts
describe('MyPipe', () => {
  const pipe = new MyPipe();

  it('should transform value', () => {
    expect(pipe.transform(data)).toEqual(data);
  });
});
```

### Components
```ts
import { ComponentFixture, TestBed } from '@angular/core/testing';s

describe('MyComponent', () => {
  let component: MyComponent;
  let fixture: ComponentFixture<MyComponent>;
  let el: HTMLElement;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [
        // ...
      ],
      declarations: [
        MyComponent,
      ],
      providers: [
        { provide: MyService, useClass: MyStubService },
      ],
    });
  });

  beforeEach(() => {
    fixture = TestBed.createComponent(MyComponent);
    component = fixture.componentInstance;
    el = fixture.debugElement.nativeElement;
    fixture.detectChanges();
  });
})
```