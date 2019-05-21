# rajnish
rajnish
For run application 
Ng serve
For create components
Ng g c components/recipe-summer
Ng service services/service

For testing using karma 
Ng test
You can define our own test case 

 it('should create', () => {
   expect(component).toBeTruthy();
 });


it('should have the message "hello there" by default', () => {
expect(component.message).toEqual('hi,mom');});

Using Fixture queryselector

it('should display the text "Hello there"in a<p> by default', () => {
expect(fixture.nativeElement.querySelector('p').innerText).toEqual('hello There..'); 
});

// by will come from angular browser
import('by') form '@angular/platform-browser'
it('should have 5 divs for each of the letters', () => {
expect(fixture.debugElement.queryAll(By.css('div')).length).toBe(5);
});
});












Basics of Angular js

String interpolation syntax  = {{ string or number }} --- Auto convert into string

Property Binding
<button class=”btn btn-default” disable></button> ---- Disable attribute in Html

<button class=”btn btn-default” [disable] = “disable”></button> -- Disable  should be in boolean form 
 [disable] is binding properties in DOM.

Other Property is like [input] 

You should not use any string interpolation syntax  [disable]=”{{}}” ----Wrong

Event Binding

(click) = “function()”;
(input) = “function($event)” --- It pass event to the components 

(<HTMLInputElement>event.target).value --- Angular read the value using type of the htmlinputElement.

Two Way Binding

[(ngModel)] =”name” ------ name value will bind.
<input type=”text” [(ngModel)]=”name”>
{{name}} ---- Two way binding the name property.
To enable ngMode you have to declare into app-module file 
With formsModule need to added into import[] array

Directives
Directives are instructions in the DOM
Components are directive with the @ notations.

ngIF or else:  Structural Dirctive

<p *ngIf=”name”>Ng if is the structural directive and the * is required and it is changing the dom</p> ------ Name is true or false

Else
<p *ngIf=”name; else elsepart ”> else part with the # notation placing a local reference in else part</p> ------ Name is true or false

<ng-template #elsepart></ng-template>
 
Styling with ngStyle Directive attribute directive

Unlike structural Directive , attribute directive don’t add and remove.
[ngStyle] = {callStyleMethod()}
 
We want to bind some property with this directive 

Binding To a property of a directive

ngClass to add or remove dynamic class

[ngClass]= “{classname}”
 Or you can pass object for condition checking

[ngClass]= “{classname: condition === true}”

ngFor directive

*ngFor = “name in names” 

*ngFor = “name of names; let i = index ”

Where index=0 and it keep incrementing each time.


@Input() Directive 
<app-Input-copmponent *ngFor=”let server of serves” [server]= “server”></app-Input-copmponent >

So on top we are sending data to other component app-Input-copmponent using server property

For access the server 
app-Input-copmponent

Import INPUT Drective
@Input() server: type ------ {type: string, name:string} ---------server is a property that bind data from the parent component 

This can be pass as a parameter

<app-Input-copmponent *ngFor=”let server of serves” [ChangeServer]= “server”></app-Input-copmponent >

@Input(ChangeServer)  server;


Event Emmeter using output Directive

<app-cockpit (addSerevr)="addnewServer($event)" (addBluePrint)="addnewBluePrint($event)"></app-cockpit>

Events bind and send data from child to parent

@Output propertname = new Eventemmeter<data,object>();()---constructor

For emit

propertyname.emit({obje});


EventEmmiter<typeof data pass> is a generic type

Change Encapsulation css behavior

Using encapsulation: viewEncapsulation.none----angular/core   
The above code remove all the encapsulated css property from the source code.
.Native -- sudo dom property



Local Reference in angular
Using # key 
<input type=”text” #valueofinput>

(click)= “passlocalreferance(valueofinput)”---local reference to a component 

Local reference can’t directly pass to component it can only using the events 

And into component ts file get the value using

Function localReference(reference: HtmlInputElement) {
	Var retrunvalue = reference.value;
}

@ViewChild Directive(Decorator)

Property decorator that configures a view query. The change detector looks for the first element or the directive matching the selector in the view DOM. If the view DOM changes, and a new child matches the selector, the property is updated.
 
Using ElementRef native element property 

@viewChild(‘localreference’) localreference : ElementRef -----console.log(localrefrence);

To get value from reference

Var local= this.localreference.nativeElement.value

If anything change in DOM it catch details for all change into  using viewChild Decoretor






Life Cycle For angular

constructor() {
   console.log('Constructor Called');
 }
 deleteServer(i) {
   this.deleteEle.emit(i);
 }
 ngOnChanges(changes: SimpleChanges) {
   console.log('ngOnChanges called');
   console.log(changes);
 }
  ngOnInit() {
   console.log('ng on init called');
 }
 // Every change detection will run
 ngDoCheck() {
   console.log('Ng Do Check called');
 }
 // Content will be ng-content
 ngAfterContentInit() {
   console.log('Ng After content call');
 }
 ngAfterContentChecked() {
   console.log('Ng After content Checked');
 }
 ngAfterViewChecked() {
   console.log('Ng After View Checked');
 }
 ngAfterViewInit() {
   console.log('Ng After View Init');
 }
 ngOnDestroy() {
   console.log('Destory first');
 }
 passvalue() {
   console.log(this.childValue.nativeElement.value);
 }


Local Reference ContentChild
In other component just add local ref

<p #content>
@ContentChild('Content') paragraph: ElementRef;
this.paragraph.nativeElement.textContent
TO ACCESS FORM outside of the components.
@viewChild is for inside of the component. 
*The children element which are located inside of its template of a component are called view children **
**elements which are used between the opening and closing tags of the host element of a given component are called content children **


Decorator and directive
@ is called as a decoretor @components @dirctive()
We Can't have more then one structural directive in one element.
ex->
*ngIf and *ngFor both are structural directive and that can change the DOM after occurence.

Attribute Directive
[ngClass]="{odd: number % 2 !== 0}
We can write class write like that way and bind css property

    2)    Basic Attribute Drective
	[ngStyle]="{backgroundColor: number % 2 !== 0 ? 'yellow' : 'transparent'}"

ng g d attribute-directive -- to create directive file

 constructor(private eleRef: ElementRef) {
 }
ngOnInit() {
this.eleRef.nativeElement.style.background = 'green';
}
  3)Renderer Attribute Directive
	Renderer2 is to bind the dom element.
So rederer is the better approach to using attribute directive
If has different arguments
 this.renderer.setStyle(this.eleRef.nativeElement, 'background-color', 'blue');
Extend this base class to implement custom rendering. By default, Angular renders a template into DOM. You can use custom rendering to intercept rendering calls, or to render to something other than DOM.

Host Listener Attribute directive
Using this listener we can call any event object  and bind to the property on event 
Mouse enter , mouse leave , click
// argument with string and that will have all the event and this will listen to custom event
 @HostListener('mouseenter') mouseover(eventData: Event) {
   console.log(eventData);
   this.renderer.setStyle(this.eleRef.nativeElement, 'background-color', 'blue');
 }
 @HostListener('mouseleave') mouseleave(eventData: Event) {
   console.log(eventData);
   this.renderer.setStyle(this.eleRef.nativeElement, 'background-color', 'transparent');
 }
HostBinding to bind to host
Working with an element inside in a directive
// this will access style property and sub property background color
@HostBinding('style.backgroundColor') backgroundColor: string;
this.backgroundColor = 'blue';
Host binding we can attach class 
 @HostBinding('class.open') isOpen = false
Binding TO Directive Property
Using property binding we can bind the element
Using @Input() color

And get the value using 
<p [color]= "'yellow'"></p> // Sending the data to directive
Directive itself close into square bracket
So we can take input from the appBetterDirective.
Like below code
<li class="list-group-item" [appBetterDirective]="'green'" [defaultColor]="'yellow'">
 @Input('appBetterDirective') hoverColor = 'red';

Demo code
{code}
import { Directive, ElementRef, Renderer2, OnInit, HostListener, HostBinding, Input } from '@angular/core';

@Directive({
 selector: '[appBetterDirective]'
})
export class BetterDirectiveDirective implements OnInit {
Museclick = 0;
 @Input() defaultColor = 'transparent';
 @Input('appBetterDirective') hoverColor = 'red';
// this will acces style property and sub property background color
@HostBinding('style.backgroundColor') backgroundColor: string = this.defaultColor;
 constructor(private eleRef: ElementRef, private renderer: Renderer2 ) {
   this.backgroundColor = this.defaultColor;
 }
 ngOnInit() {
   // this.renderer.setStyle(this.eleRef.nativeElement, 'background-color', 'blue');
   this.backgroundColor = this.defaultColor;
 }
 // argument with string and that will have all the event and this will listen to custom event
 @HostListener('mouseenter') mouseover(eventData: Event) {
   this.backgroundColor = this.hoverColor;
 }
 @HostListener('mouseleave') mouseleave(eventData: Event) {
   this.backgroundColor = this.defaultColor;
 }
 @HostListener('click') onclick(eventData: Event) {
   console.log(this.Museclick++, 'jbfxv');
 }
}


{code}
  


Structural Directive

What happened behind the scenes
* Indicate it is a structural directive
*ng-> * is use to nicer way to declare
So when we place * then angular change dom or structure of a dom.
We can use as a property binding inside ng-template.
 
<ng-template [ngIf] =! something >  // ng-form-template due to transform from * to property binding
<div>
</div>
</ng-template>


Building Structural directive

For building a structure directive 

We have to use few injector
Templateref: TemplateRef --> Template reference which template to refere. What should it render
vcRef: ViewContainerRef -->  What you want to do inside the container.Where should it render it.

We are taking value from the Input()
 // set is the method this still a property , whenever changes the property.
Input parameter changes with the set method, It execute whenever property changes. 
 @Input() set appUnless(condition: boolean) {
 if (!condition) {
   this.vcRef.createEmbeddedView(this.templateRef);
 } else {
   this.vcRef.clear();
 }
}
  
 constructor(private templateRef: TemplateRef<any>, private vcRef: ViewContainerRef) {

 }


Services And Dependency Injection

Services can be created multiple way.
Create services using
Ng g s services/services
After that we need to register it into Component Director

Using provide: [providerName];

Services worked in hierarchical way top to child component.
But if you want to change made to all the component then you need to register it into app Module page
Provider:[array of the provider],  
If you want to emit something using services.

Just create event emitter in services

eventEmitter = new EventEmitter<string>();

And from the component just emit the event 
Using 
this.service.seventEmitter.emit(string);

And in other component just subscribe into it using

this.service.seventEmitter.subscribe(
(status: string) => alert(status);
)


Router Angular
 RouterModule.forRoot(




routerConfig,


   )
routerConfig = [{
Path:'',
redirectTo:'Home',
pathMatch:'full'
},
{
Path:'home',
component:HomeComponent,
data: {title:'MyHome'}
}
]
 
 And just add directive to root folder
<router-outlet></router-outlet>
To get the routed link

This all is imported from the angular/router
import { RouterModule, Routes } from '@angular/router';

And to call the route just add in html file
routerLink = “/” orr any path
TO make this active link
Just add 
routerLinkActive = “active”
But in case of blank path this will not work
For that just add
[routerLinkActiveOptions] = “{exact:true}”
[routerLink] = “‘name’” using property binding 




Programmatically we can add routing 
// ROuter is imported from angular/router
Just inject route into the constructor
constructor(private router: Router) {} // INjecting route to use it into method

onLoad() {
this.router.navigate(['/server']); // absolute path
} 

Using Relative path in router
Route is imported from angular/router
constructor(private route: ActivatedRoute)

onReload()
 {
this.router.navigate(['servers'], {relativeTo: this.route});
}
Above code refers
Navigate -> servers to the relative path -> TO the reference of route



Passing parameter to Route

We will pass the parameter to the route 
{path: 'user/:id/:name', component: UserComponent}

Here Id is parameter that can be anything.

localhost/user/1 or  localhost/user/someName → this will load the UserComponent page after the parameter passed to the user 


Fetching Route Parameter
This.user = {id,name}
Route should be imported from angular/router
controller(private route: ActivatedRoute)
this.user = {
Id: this.route.snapshot.params['id'],
name: this.route.snapshot.params['name'],
}
In html file
[routerLink] = "['/user',10,'Anna']" 
This should create
/user/10/anna path

 Fetch Route Parameters Reactively
Params is observable
Observable is the easy way to subscribe the event when it occurs  
Prams is the object that contains url properties.
this.route.params.subscribe((params: Params) => {
This.user.id = params['id'];
})


Route.snapshot.params


When it is static no need to create subscriber and observer to lesson  

this.route.params.subscribe((params: Params))

When your component changes the value dynamically
What happen when you are subscribing it in backend
It store the route in back and it won't destroy even if component destroyed.
   


So for the above solution we need to destroy event
Implement OnDestroy
Import {subscription} from 'rxjs/subscription'

And then define the type of the property 
paramsSubscription: Subscription;
this.paramsSubscription=this.route.params.subscribe((params: Params) => {
This.user.id = params['id'];
})
ngOnDestory() {
this.paramsSubscription.unsubscribe();
}


Query Parameter Access 
{path: 'servers/:id/edit', component: EditServersComponent}

Hookup Links
[routerLink] = "['/servers',5,'edit']"
Add new bindable property 
[queryParams]="{allowEdit=1}" /server/5/edit/?allowEdit=1
fragment = "loading"/server/5/edit/?allowEdit=1#loading


In typeScript file

this.router.navigate(['/servers',id,'edit'],{queryParams: {allowEdit: '1'},fragment:'loading'});
Retrieve query parameter
We need route:ActivatedRoute import from router

ngONinit() {
console.log(this.route.snapshot.fragment);
this.route.params.subscribe()
this.route.queryParams.subscribe()
this.route.fragment.subscribe()
}
Query parameter pass to the other component
this.router.navigate(['edit'], {relativeTo: this.route, queryParamsHandling: 'preserve'});// will take current query parameter.
// merge will merge with the current to old


Wild Card route

If component not present just add wildcard to catch and redirect to 404

{path:’**’, redirectTo:’path to component 404’}
Make sure wild card into the last of array object

Angular Guards


Guards
It is use to guards the route like login and logout


To Use guard we need to create service file
And in that just implements CanActivated interface.
And that contains 
canActivate(route)

Above method contains two parameter
canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot)
-----------------------------------------------------------------------

This method contains return type

Observable<boolean> | Promise<boolean> | boolean

This can run sync and async mode 

------------------------------------------------------------------------

To use this service we need to use it in route method.
Like which url you want to auth 
------------------------------------------------------------------------
 
Just add canActivate in array 
canActivate: [Auth ]
Demo Code 
Auth.services

export class AuthService {
   isLoggedin: boolean;
   constructor() {
       this.isLoggedin = false;
   }
   isActivated() {
       const promise = new Promise<boolean>(
           (resolve, reject) => {
               setTimeout(() => {
                   resolve(this.isLoggedin);
               }
               , 4000);
           }
       );
       return promise;
   }
   login() {
       return this.isLoggedin = true;
   }
   logout() {
       return this.isLoggedin = false;
   }
}



Auth Guard

import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';
import { Observable } from 'rxjs';
import { Injectable } from '@angular/core';
import { AuthService } from './auth.service';
@Injectable()
export class AuthGard implements CanActivate {
   constructor(private authService: AuthService, private router: Router) {}
canActivate(route: ActivatedRouteSnapshot,
   state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
   return this.authService.isActivated()
   .then(
       (authenticated: boolean) => {
           if (authenticated) {
               return true;
           } else {
               this.router.navigate(['/']);
           }
       }
   );
}
}


At last just add canActivated in route for menu
canActivate: [AuthGard]
  {path: 'servers', canActivate: [AuthGard], component: ServersComponent}



For child route or Child Component Authenticate 

Just like canActivate 
canActivateChild() → This contains similar parameter and return type.

Demo Code
 canActivateChild(route: ActivatedRouteSnapshot,
       state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
       return this.canActivate(route, state);
       }
And in Router 
canActivateChild: [AuthGard]


CanDeactivate Route
In the page if any changes occured and its not saved then we can catch and notify the user like do you want to quit or stay on the pages
Demo Code
import { Observable } from 'rxjs';
import { CanDeactivate, ActivatedRouteSnapshot, RouterStateSnapshot } from '@angular/router';

export interface CanComponentDeactivate {
   canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean;
}

export class CanDeactivateGard implements CanDeactivate<CanComponentDeactivate> {
canDeactivate(component: CanComponentDeactivate,
currentRoute: ActivatedRouteSnapshot,
currentStatus: RouterStateSnapshot,
    nextState?: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
        return component.canDeactivate();
    }
}



Above code will call by another method inside component.
Using implement interface and its method
 canDeactivate(): Observable<boolean> | Promise<boolean> | boolean {
   if (!this.allowAdded) {
     return true;
   }
   if (this.serverName !== this.server.serverName || this.serverStatus !== this.server.status && !this.changesSaved) {
     return confirm('Do you want to Descard the changes?');
   } else {
     return true;
   }
 }
 Above code will check the changes occured at any property or not.
If not return true 
Or return the confirm box to the users 
Above we studies all the router activation 
CanActivate -> this contains one method canActivate(route, state) and return type is obsrvable<boolean> | Promises<boolean> | boolean
CanActivateChild -> It will call to above method with the same parameter 
CanDeactivate -> canDeactivate method		







Passing Static data to route

Just add data object in router module and fetch using 
{ path: 'not-found', component: ErrorPageComponent, data: {'message': 'Page not availabe'} }

ActivatedRoute

this.route.data.subscribe(
     (data: Data) => {
       console.log(data);
       this.errorMessage = data['message'];
     }
   );


Passing Dynamic Data

Using Resolver
Demo Code

import { Resolve, ActivatedRouteSnapshot, RouterStateSnapshot, ActivatedRoute } from '@angular/router';
import { Observable } from 'rxjs';
import { ServerServiceService } from '../server-service.service';
import { Injectable } from '@angular/core';
interface Server {
   id: number;
   serverName: string;
   status: string;
}
@Injectable()
export class ServerResolver implements Resolve<Server> {
   constructor(private serverService: ServerServiceService, private route: ActivatedRoute) {}
resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<Server> | Promise<Server> | Server {
   return this.serverService.getServer(+route.params['id']);
}
}

And we need to pass it into router module
{ path: ':id', component: ServerComponent, resolve: { server: ServerResolver }}

In the component just get the data from resolver
this.route.data.subscribe(
     (data: Data) => {
      this.server  = data.server;
       console.log(data);
     this.serverName = this.server.serverName;
     this.serverStatus = this.server.status;
     }
  );
Above an example of passing data from the route
Understanding Observable 


Observable is a part of a data source(user input, Http Request, Triggered in code). It is in package of RXJS.

1)Observable (data Package)

2) Observel -> It is subscribe code or my code need a logic in it and receive from the Observable. Like we deed for router.subscriber

Three ways to handling data packages that we receive from the observable
Handel Data
Handel Error
Handel Completion 



Using Observable 
Code Demo

import { Component, OnInit } from '@angular/core';
import { interval } from 'rxjs';

@Component({
 selector: 'app-observer-learning',
 templateUrl: './observer-learning.component.html',
 styleUrls: ['./observer-learning.component.css']
})
export class ObserverLearningComponent implements OnInit {
 constructor() { }

 ngOnInit() {
   const mynuber = interval(3000); // Observable
   mynumber.subscribe( // observer 
     (numb) => {
       console.log(numb);
     }
   );
 }

}



Own Observable Create 
Demo Code

import { Component, OnInit } from '@angular/core';
import { interval, Observable, Observer } from 'rxjs';

@Component({
 selector: 'app-observer-learning',
 templateUrl: './observer-learning.component.html',
 styleUrls: ['./observer-learning.component.css']
})
export class ObserverLearningComponent implements OnInit {
 constructor() { }

 ngOnInit() {
   // const mynuber = interval(3000);
   // mynuber.subscribe(
   //   (numb) => {
   //     console.log(numb);
   //   }
   // );
   const myObservable = Observable.create( // This is normal brize between observable and observal
     (observel: Observer<string>) => {
       setTimeout(() => {
         observel.next('First Observable'); // pass the next datapackage to observable
       }, 2000);
       setTimeout(() => {
         observel.next('Second Observable');
       }, 4000);
       setTimeout(() => {
        // observel.error('Error Observable');
        observel.complete();
       }, 6000);
       setTimeout(() => {
         observel.next('after Error Observable');
       }, 7000);
     }
   );
   myObservable.subscribe(
     // Total 3 function argument can accept
     (data: string) => { // Data package that recive from the observable
       console.log(data);
     },
     (error: string) => { // Second para is error message
       console.log(error);
     },
     () => {
       console.log('Completed the call');
     }
   );
 }

}



Unsubscribe Observerval 
It always run in background hence we need to unsubscribe when we kill the page or component. If we don’t than it cause the memory leak and memory outbound exception

Demo code 
numberSubscription: Subscription // imported from rxjs

this.numberSubscription = mynuber.subscribe(
   //   (numb) => {
   //     console.log(numb);
   //   }
   // );


ngOnDestroy() {
 this.numberSubscription.unsubscribe();
}
Above code kill the background process when it kills the page. 







Use Of Observer instead of eventemitter
Cross component Emitter or own Event Emitter.
Create service and just declare 
export class ObservarUser {
 userActivated = new Subject();
}

The above code will observe and subscribe both at the same end 

For using observer data package 
this.obserService.userActivated.next(this.id);

And for subscribe 

 this.userService.userActivated.subscribe(
       (id: number) => { // this value get from the observable 
         console.log(id);
       }
     );




Angular Forms


Angular have the two approach for form 
Template Driven
Reactive Approach	
		
Template Driven Form Approach

Angular have the pre build method to get object of the form data

-> It is very simple by using ngForm in the form local reference.

Code example 
For submitting the form use 
(ngSubmit)="onsubmit()" -> on click submit the method will call

Above code work same like form action 
Passing the form data

Use local Reference 
<form (ngSubmit)="onSubmit(f)" #f="ngForm">

 onSubmit(form: NgForm){ // Importing the NgForm from forms
   console.log(form); // THis will return all the form object
 }

 
Understanding Form State
In tag email is a directive
<input type="email" id="email" class="form-control" ngModel name="email" email>
NgForm give all the state changes information to the user
Like form is valid or not 
Ng-touch ng-valid etc.






Using state change just show the message to the user

<input type="email" id="email" class="form-control" ngModel name="email" required email #email="ngModel">

email.hasError=”requird” // access the error
<span *ngIf="!email.valid && email.touched">Email is not valid</span>


Explanation

#email contains the from events as a local reference

Local ref contains all the value that ngModel will have.


Property binding using form 
[ngModel]="valuefromts"
In js file 
Just add the property value
Using the key 
Valuefromts = "rajnish"
NgModel two way binding

<div class="form-group">
         <textarea name="questionAnswer" id="" rows="3" [(ngModel)]="answer" class="form-control"></textarea>
       </div>
       <p>Your Reply {{answer}}</p>




In js file declare property
Answer and then bind the data to and from using ngmodel
Grouping form control

<div id="user-data" ngModelGroup="usergroup">
</div>
Local also we can access the value using property binding

<input type="text" #grouing="ngModelGroup">
Just wrap all input fields inside the userdata.

In the ngForm we will get the details of user object with grouping name user group as object



This line will give the access to the grouping object 


Set Value and Patch value 

Code for set value it should pass all the data value
this.formValue.setValue({
     usergroup: {
       username: 'rajnish',
       email: 'rajnishmca20@gmail.com'
     },
     secret: 'pet',
     questionAnswer: '',
     gender: 'male'
   });

Patch Value

this.formValue.form.patchValue(
     { usergroup: { username: 'rajnish'}}
   );



Set value is use for set the whole form.

Patch value is use for the part of the form.
















It's always better to use patch value. Because it will always have full control of the form data.   
Reset form after submit
this.signupForm.reset()

Reactive Form


Form is created programmatically and synchronized with the DOM


Using FormGroup to implement Reactive form validation 
It is imported from angular/forms

One global import 
ReactiveFormModule from forms
To use Form control

This.formname = new FormGroup({
  'username': new FormControl('', Validators.required),
     'email': new FormControl('', [Validators.required, Validators.email]),
     'secret': new FormControl('', Validators.required),
     'gender': new FormControl('male')
   });


Log out formName to see the all object
Form name should declare in the form tag

Adding [formGroup] directive -> take this form group and binding via property binding


<form [formGroup]="signupForm" (ngSubmit)="onSubmit()">

To implement inside form use 
formControlName="email"
<input type="email" id="email" class="form-control" name="email" formControlName="email">


We don't need ngModel
Adding validation to a form
Using Validators object
'email': new FormControl('', [Validators.required, Validators.email])


Displaying error message to the user if the form field is invalid.
<span class="help-block" *ngIf="!signupForm.get('username').valid && signupForm.get('username').touched">Please Enter a Valid username</span>

Above code will provide you the access of form object using formname.get() method with the field name.
Reactive Grouping Concept

Using formGroupName="userData"
We can bind the form in group 


For displaying Error message to user

<span class="help-block" *ngIf="!signupForm.get('userData.username').valid && signupForm.get('userData.username').touched">Please Enter a Valid username</span>


In js just add the 
Nest formGroup 

 'userData' : new FormGroup({
       'username': new FormControl('', Validators.required),
       'email': new FormControl('', [Validators.required, Validators.email]),
     }),
Full code
 this.signupForm = new FormGroup({
     'userData' : new FormGroup({
       'username': new FormControl('', Validators.required),
       'email': new FormControl('', [Validators.required, Validators.email]),
     }),
     'secret': new FormControl('', Validators.required),
     'gender': new FormControl('male')
   });



Reactive Array of forms Controls


Need to do a lot of things here 

Adding formArray in form group object

Example
'getHobbies': new FormArray([])



Onclick event

addHobbies(){
   const control = new FormControl('null', Validators.required);
   (<FormArray>this.signupForm.get('getHobbies')).push(control);
   // casting the value using formarray that is his type
} 


In Html file call this formArray

{{Sample Code}} 

<div formArrayName="getHobbies">
         <h4>Your Hobies</h4>
         <button (click)="addHobbies()" class="btn btn-primary">Add Hobbies</button>
         <div class="form-group" *ngFor="let hobbbie of signupForm.get('getHobbies').controls; let i = index;">
           <input type="text" class="form-control" [formControlName]="i">
         </div>
       </div>




Adding Our own Validators


For adding validators we will write method 
Ex 
Global create Array

forbiddenName = ['Test'];


 forBiddenNames(control: FormControl): {[s: string]: boolean} {
   if (this.forbiddenName.indexOf(control.value) !== -1) {
     return {'nameIsForbidden': true};
   }
   return null;
 }


The above method will call by angular 

And in formGroup inside form control pass the method name

SOmething like this

'username': new FormControl('', [Validators.required, this.forBiddenNames.bind(this)]),





Reactive: Using Error Code


We are getting value from the form control object and display according to that signupForm.get('userData.username'). 

signupForm is forGroup  property

<span
           class="help-block"
           *ngIf="!signupForm.get('userData.username').valid && signupForm.get('userData.username').touched"
           class="help-block">
           <span *ngIf="signupForm.get('userData.username').errors['nameIsForbidden']">
             This name is not allowed
           </span>
             <span *ngIf="signupForm.get('userData.username').errors['required']">
               This field is required
             </span>
         </span>




Reactive Creating a custom Async Validator

If we want to check the error from the services and the response is not coming at the same time so we need the async call

 forbiddenEmails(control: FormControl): Promise<any> | Observable<any> {
   const promise = new Promise<any>(
     (resolve, reject) => {
       setTimeout(() => {
         if (control.value === 'test@test.com') {
           resolve({'email is forbidden': true});
         } else {
           resolve(null);
         }
       }, 10000);
     });
   return promise;
 }

Above code work when we pass parameter in the formControl 
'email': new FormControl('', [Validators.required, Validators.email], this.forbiddenEmails)

After running in background it always check the status 
For some time it is in pending and after that it return the correct class to it.


Reactive: Reacting to status or Value Changes 

this.signupForm.valueChanges.subscribe(
     (value) => console.log(value)
   );
   this.signupForm.statusChanges.subscribe(
     (status) => console.log(status)
   );


 
Set value and patch value work same as template driven form

Reset the form using reset method

this.signupForm.reset(); // will reset the form


Binding to a string using property binding in form

pattern=”^[-+]?[1-9]\d*\.?[0]*$” // To check number is +ve

Or 

[pattern]=”’^[-+]?[1-9]\d*\.?[0]*$’” // Same thing but using single quotes  



Pipes

What are pipes?
It transform some output. It also use for sync and async.

One of the pipe symbol is 

Uppercase

{{name| uppercase}} 

Or some date pipeline
{{date | date }}
If you have the parameter 

{{date | date:"full" }} -> TO add parameter just add : and the value

To learn more about pipe
https://angular.io/api

Create custom Pipe

Creating custom pipe we need to declare decorator

@Pipe({name: 'shorten'})

export class Shoretn implements PipeTransform {
   transform(value: any) {
       return value.substr(0, 10);
   }
}

Use name of the pipe to filter as shorten

Custom Pipe Parameter

export class Shoretn implements PipeTransform {
   transform(value: any, limit: number) {
       return value.substr(0, limit);
   }
}

From the pipe filter we need to pass the parameter

{{name | shorten: 5}}-> Here 5 is the limit as a parameter

More depth
{{name | shorten: 5: 10}}


Pipe Shortcut command

Ng g p pipe name

Demo Code
import { PipeTransform, Pipe } from '@angular/core';
@Pipe({
   name: 'filter'
})
export class Filter implements PipeTransform {
   transform(value: any, filterString: string, propName: string): any {
       if (value.length === 0 || filterString === '') {
           console.log(value);
           return value;
       }
       const resultArray = [];
       value.forEach(item => {
           if (item[propName] === filterString) {
               resultArray.push(item);
           }
       });
       console.log(resultArray);
       return resultArray;
   }
}








@Pipe({
   name: 'filter',
   Pure: false // this will take changes on run time
})

Little about promises 

 serverStatus = new Promise((resolve, reject) => {
   setTimeout(() => {
     resolve('test');
   }, 5000);
 });

In Html file we need pipes to display its value 

{{serverStatus|async}} -> Using async pipes to print the object 

Without async it return object value







Making Http Request

To make Http service we need to import few module

In service file 
import { Http } from '@angular/http';
constructor(private http: Http, private firebase: AngularFireDatabase) { }
 storeServers(server) {return this.http.post('https://test-7b6af.firebaseio.com/data.json', server); }

In module file 
We need to add and import httpModule file

import { HttpModule } from '@angular/http';


Using firebase database to make application more dynamic

https://console.firebase.google.com/project/test-7b6af/database/test-7b6af/data/


For implementing this concept we need to import few files

Add the config file in environment folder                                        
ex-> /Users/rajnish.kumar/mypro/project/src/environments/environment.ts

Test code 

export const environment = {
 production: false,
 firebaseConfig: {
   apiKey: 'AIzaSyCzoIwkd-V_-AdPJWtmhpnFP_Ni1AV_8rE',
   authDomain: 'test-7b6af.firebaseapp.com',
   databaseURL: 'https://test-7b6af.firebaseio.com',
   projectId: 'test-7b6af',
   storageBucket: 'test-7b6af.appspot.com',
   messagingSenderId: '809632247980'
 }
};


 
App module we need to import few module and install few module. TO installing module we need to run command in terminal
Npm -i firebase angularfire2
THis will generate all the plugins

We need to import 3 file to make it work
import { AngularFireModule } from 'angularfire2';
import { AngularFireDatabaseModule } from 'angularfire2/database';
import { environment } from '../environments/environment';

In import in array 
Imports: [AngularFireModule.initializeApp(environment.firebaseConfig),
   AngularFireDatabaseModule
]
In app module this is enough   
 To implement this in template we need to add service
Dummy code for implementing the CURD operations

import { Injectable } from '@angular/core';
import { HttpModule } from '@angular/http';
import { Http } from '@angular/http';
import { AngularFireDatabase, AngularFireList } from 'angularfire2/database';
@Injectable()
export class ServiceService {

 constructor(private http: Http, private firebase: AngularFireDatabase) { }
 customerList: AngularFireList<any>;
 storeServers(server) {
   console.log(server);
   this.customerList = this.firebase.list('/data');
   this.customerList.push(server);
   // return this.http.post('https://test-7b6af.firebaseio.com/data.json', server);
 }
 getCustomers() {
   this.customerList = this.firebase.list('data');
   return this.customerList.snapshotChanges();
 }
 insertCustomer(server) {
   this.customerList.push(server);
 }
}



  


Passing Header in the service

Const header = new Header({'content-type': 'text/Json'})

return this.http.post('https://test-7b6af.firebaseio.com/data.json', server, {headers: headers})  


Get Server to get Back data

Angular offer you get response back from the server

Import Response from http.

This will return all the json format data by applying 

ex-> 

this.recipeService.getServer().subscribe(
(response: Response) => {
Const data = response.json();
console.log(data);
}
);

Put Request

Append the existing data or append to new one

Same as post request

Ex
this.http.put('serverurl');


Getting back data from server
Catching error for http request

Important import
import 'rxjs/add/operator/catch';
import 'rxjs/add/observable/throw';

getServer() {
   return this.http.get('https://test-7b6af.firebaseio.com/data')
     .pipe(map(
     (response: Response) => {
       const data = response.json();
      // console.log(data);
       const test = Object.keys(data).map(i => {
         return data[i];
       }
       );
       // console.log(test);
       return(test);
     }
   )).pipe(catchError((err: Response) => {
     console.log(err);
     return Observable.throw(err);
   }
 ));
 }
      
Get response from the error code

(error) => console.log(error)



Using the async pipe with HTTP Requests

Using async pipes need to subscribe the observar 
 Example code

appName = this.recipeService.getAppName();

In Server http request
 getAppName() {
   console.log('here');
  return this.http.get('https://recipe-4fc9a.firebaseio.com/data.json')
   .pipe(map((response: Response) => {
     console.log(response.json());
     return response.json();
   }));
 }

Finally use pipes to print the value from the db

<li *ngIf="(appName | async) as appName">{{appName.appName}}</li>
Using async pipe filter this pipe will do the rest job for the subscriber 






Authentication & Route Protection in Angular

To send authentication related list using firebase

First we need to install firebase.

After that just use the service in root folder

Such as app.component

import * as firebase from 'firebase';
Inside class

 ngOnInit() {
   firebase.initializeApp({
     apiKey: 'AIzaSyCwQuy8Vb-b5j8t74n_SJP_MCGbfatibbI',
     authDomain: 'recipe-4fc9a.firebaseapp.com'
   });
 }


Adding key to app load.

TO work with the token 
Create Service file
import * as firebase from 'firebase';
import { Injectable } from '@angular/core';
@Injectable()
export class AuthServices {
signupUser(email: string, password: string) {
firebase.auth().createUserWithEmailAndPassword(email, password).then(
   responce => console.log(responce)
)
.catch(
   error => console.log(error)
);
}

signinUser(email: string, password: string) {
   firebase.auth().signInWithEmailAndPassword(email, password).then(
       (response => {
           console.log(response);
       }
   ));
}
}
 
And call into the method inside the other component


 onSignin(form: NgForm) {
   const email = form.value.email;
   const password = form.value.password;
   this.authService.signinUser(email, password);
 }

Get token from the login form

Using Angular Module & Optimizing Apps

CommonModule imports -> Common module will provide the feature to add attribute and directive.

Example if we create any extra module then we need to imports Common MOdule form @angular/common
Code Example for adding common module
Why we need to create extra module?

We are importing everything in app.module file. SO we are creating complex file that is hard to edit in future. 

For overcome this situation we create extra module for component and extra module for routing.   

Module file
@NgModule({
   declarations: [ShoppingListComponent, ShoppingEditComponent],
   imports: [
       CommonModule,
       FormsModule,
       RouterModule.forChild([{path: '', component: ShoppingListComponent}])
   ],
   exports: [RouterModule]
})
export class ShoppingListModule {}




Forchild is use to make child route for the parent module.

After all setup done then we remove import component from the app module file. 



Difference between Browser Module and common Module

BrowserModule provides services that are essential to launch and run a browser app.
BrowserModule also re-exports CommonModule from @angular/common, which means that components in the AppModule module also have access to the Angular directives every app needs, such as NgIf and NgFor.


Common Module

CommonModule (all the basics of Angular templating: bindings, *ngIf, *ngFor…), except in the first app module, because it’s already part of the BrowserModule


RouterModule.forRoot(ROUTES) vs RouterModule.forChild(ROUTES)


Lazy Loading 
User usually not load every module while browsing but angular download every package in one shot. That will make site little slow . To Overcome this situation we need to load the component when it needed  i.e. called lazy loading.

{ path: 'recipes', loadChildren: './recipes/recipes.module#RecipeModule'}

loadChildren file will be in main routing folder 

After that we need to add static path for the component  module ./recipes/recipes.module And in the module class name followed by #RecipeModule.




AOT reduce the size of code in prod environment

 
Preloading all lazy loading after module load 
// Angular route import preloadAllModule
RouterModule.forChild(appRoute, {preLoadingstrategy: PreLoadAllModule })


Using HTTPCLIENT in Angular app

TO use this client we need to import form 
import { HttpClientModule } from '@angular/common/http';
In app.module to use in service.

In services page import HttpClient 
import { HttpClient } from '@angular/common/http';

HttpClient is very strong and it don’t require Response to convert json data

Just give the generic type in get or put request
this.http.get<generic type>(url,{if any parameter like type:”text or json”,observe{headeror body})

Working with response events 

Http CLient will pass the response to the client and get it back 

To get the response we have different options 
this.httpclient.get<>(url+token+getdata(), {Observe: “Events or body”})

Events will have Object type and we will get it back by doing under process

saveData(callMethod(
(response: HttpEvents<Object>) {
console.log(response)
}
) );

Import httpEvent from @angular/common/http

saveData() {
   // call service
   this.dataService.saveRecipe().subscribe(
     (response: HttpEvent<Object>) => console.log(response.type)
   );
 }


Working with Header TO send Headerdata to cline authentication 
Import HttpHeaders from @angular/common/http
Header =  new HttpHeaders().set(‘application’: ‘aksndfk’).append(‘new’:’append ne data’)

saveRecipe() {
   const token = this.authToken.getAuthToken();
   return this.http.put('https://recipe-4fc9a.firebaseio.com/recipe.json?auth=' + token, this.recipeService.getRecipe(), {observe: 'body', headers: Header});
}


Working with httpParams
Import httpParams from @angular/common/http
Same like header 
I am removing ?auth=' + token
saveRecipe() {
   const token = this.authToken.getAuthToken();
   return this.http.put('https://recipe-4fc9a.firebaseio.com/recipe.json, this.recipeService.getRecipe(), {observe: 'body', headers: Header, params: HttpParams().set(‘auth’,token)});
}

So here reducing the complexity of code. 


Using Progress HttpRequest we can get the progress state

Example 
 // return this.http.put('https://recipe-4fc9a.firebaseio.com/recipe.json', this.recipeService.getRecipe(), {
       //     observe: 'body',
       //     params});
       const requests = new HttpRequest('PUT', 'https://recipe-4fc9a.firebaseio.com/recipe.json', this.recipeService.getRecipe(), {reportProgress: true, params});
       return this.http.request(requests);
Using HttpRequest pass the request type and the data to store in to server

reportProgress to get download and upload status

Below is the upload status
{type: 1, loaded: 452, total: 452}loaded: 452total: 452type: 1__proto__: Object
header.component.ts:23 

HttpHeaderResponse {headers: HttpHeaders, status: 200, statusText: "OK", url: "https://recipe-4fc9a.firebaseio.com/recipe.json?au…zv9PfC_Pysg8iKENfWDpwT6nhHWh5TO3Nbf7rZRGIDPqkcoSw", ok: true, …}
header.component.ts:23 
Below is the Download status
{type: 3, loaded: 452, total: 452}
header.component.ts:23 HttpResponse {headers: HttpHeaders, status: 200, statusText: "OK", url: "https://recipe-4fc9a.firebaseio.com/recipe.json?au…zv9PfC_Pysg8iKENfWDpwT6nhHWh5TO3Nbf7rZRGIDPqkcoSw", ok: true, …}

Interceptors
Export class implements HttpInterceptors

The Intercepts methods get two arguments
intercept(req: HttpRequest<any>, next: HttpHandler )
HttpRequest is type generic and it will get any type of request
Next:HttpHandler -> It will handle a special request it will call back every time.

Intercept Method will return Observable<HttpEvent<any>> Because angular need Observable to wrap the request it is a generic type i.e
HttpEvent is also a generic type because it could return any events
Such as sent event upload progress and simply a event that the response is there  
}
export class AuthInterceptors implements HttpInterceptor {
   intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
      console.log('INtercept', req);
       return next.handle(req);
   }
}

So here We are  handling the request using httpHandler and getting the request type

So using this HTTP_INTERCEPTORS

import { HTTP_INTERCEPTORS } from '@angular/common/http';

{provide: HTTP_INTERCEPTORS, useClass: AuthInterceptors, multi: true}

All Outgoing request come through this
Angular Tells that HTTP_INTERCEPTOR use inside AuthInterceptors and multi tells angular to use multiple   HTTP_INTERCEPTOR  by duplicating, 
Ex 
{provide: HTTP_INTERCEPTORS, useClass: AuthInterceptors, multi: true}
{provide: HTTP_INTERCEPTORS, useClass: AuthInterceptors1, multi: true}


Setting Up Own Parameter
By default request are immutable.But we can do it using observable using retry request. It keep running in back and some time it break the code so it is not advisable. Using Retry() Observable 
Using clone method that will give exact copy of request
req.clone() and then we can only read the request header but can’t edit it.
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
      console.log('Intercept', req);
  const clone = req.clone({params: req.params.set('auth', this.authService.getAuthToken())});
       return next.handle(clone);
   }

const clone = req.clone({params: req.params.set('auth', this.authService.getAuthToken())});

We will pass the Auth token using params.

Using NgRx in angular to state management

npm install --save @ngrx/store -- Import packge ngrx

Working with reducers 
In This file we need to import import {Action} from '@ngrx/store';

This class have no class having only function with state management 

  
import * as ShoppingListAction from './shoping-list.actions';
import { Ingredient } from '../../shared/ingredient.model';


const initialState = {
   ingredients: [
       new Ingredient('apple', 5),
       new Ingredient('Tomatoes', 10),
   ]
};
export function shoppingListReducers(state = initialState, action: ShoppingListAction.ShoppingListAction) {
   switch (action.type) {
       case ShoppingListAction.ADD_INGREDIENT:
       return {
           ...state,
           ingredients: [...state.ingredients, action.payload]
       };
       default:
        return state;
   }
}



 
In Action file we can create our type


import { Action } from '@ngrx/store';
import { Ingredient } from '../../shared/ingredient.model';
export const ADD_INGREDIENT = 'ADD_INGREDIENT';

export class AddIngredient implements Action {
   readonly type = ADD_INGREDIENT;
   payload: Ingredient;
}

export type ShoppingListAction = AddIngredient;




For getting the state add the reducer function in app.module file

Imports: [
 StoreModule.forRoot({shoppingList: shoppingListReducers})
]













Angular Animations
@component decorator add animation property

import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

import { trigger, state, transition, animate, style } from '@angular/animations';

animations: [
   trigger('divState', [
     state('normal', style({
       'background-color': 'red',
       transform: 'translateX(0px)'
     })),
     state('highlighted', style({
       'background-color': 'green',
       transform: 'translateX(10px)'
     }))
   ])
 ]

Animations dela with state
Store in one state to another state

Switching state to state 
onAnimate() {
   this.state === 'normal' ? this.state = 'highlighted' : this.state = 'normal';
   console.log(this.state);
 }

Implement the transition
 animations: [
   trigger('divState', [
     state('normal', style({
       'background-color': 'red',
       transform: 'translateX(0px)'
     })),
     state('highlighted', style({
       'background-color': 'green',
       transform: 'translateX(100px)'
     })),
     transition('normal => highlighted', animate(30)),
     transition('highlighted => normal', animate(800)),
   ])
 ]
Using transition method we will change the transition state 

In html use the property binding using state
<div [@divState]="state" style="width: 10px; height: 20px;"></div>

If you want to add more state


import { Component, ViewChild, ElementRef } from '@angular/core';
import { trigger, state, transition, animate, style } from '@angular/animations';
@Component({
 selector: 'app-root',
 templateUrl: './app.component.html',
 styleUrls: ['./app.component.css'],
 animations: [
   trigger('divState', [
     state('normal', style({
       'background-color': 'red',
       transform: 'translateX(0px)'
     })),
     state('highlighted', style({
       'background-color': 'green',
       transform: 'translateX(100px)'
     })),
     transition('normal <=> highlighted', animate(300)),
     // transition('highlighted => normal', animate(800)),
   ]),
   trigger('wildCard', [
     state('normal', style({
       'background-color': 'red',
       transform: 'translateX(0px) scale(1)'
     })),
     state('highlighted', style({
       'background-color': 'green',
       transform: 'translateX(100px) scale(1)'
     })),
     state('shrink', style({
       'background-color': 'blue',
       transform: 'translateX(200px) scale(0.5)'
     })),
     transition('normal => highlighted', animate(300)),
     transition('highlighted => normal', animate(800)),
      transition('shrink <=> *', animate(800)),
   ])
 ]
})
export class AppComponent {
 state = 'normal';
 wildCard = 'normal';
 @ViewChild('update') update: ElementRef;
 fruits = ['mango', 'banana', 'Apple'];
 title = 'angular-animation';
 onAdd() {
   console.log(this.update.nativeElement.value);
   this.fruits.push(this.update.nativeElement.value);
 }
 onDelete(item) {
   this.fruits.splice(this.fruits.indexOf(item), 1);
 }
 onAnimate() {
   this.state === 'normal' ? this.state = 'highlighted' : this.state = 'normal';
   this.wildCard === 'normal' ? this.wildCard = 'highlighted' : this.wildCard = 'normal';
   console.log(this.state);
 }
 onShrink() {
   this.wildCard = 'shrink';
   console.log(this.wildCard );
 }
}






<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <meta http-equiv="X-UA-Compatible" content="ie=edge">
 <title>Document</title>
</head>
<body>
 <div class="container">
   <div class="row">
     <div class="col-12 mb-2">
       <h3>Animations</h3>
       <button class="btn btn-primary mr-2" (click)="onAnimate()">Animate</button>
       <button class="btn btn-primary" (click)="onShrink()">Shrink</button>
     <hr>
     <div [@divState]="state" style="width: 10px; height: 20px;"></div>
     <br>
     <div [@wildCard]="wildCard" style="width: 100px; height: 50px;"></div>
     </div>
     <div class="col-12">
       <input type="text" name="update" id="" #update>
       <button class="btn btn-primary ml-2 mb-2"(click)="onAdd(update)">Add Item</button>
       <ul class="list-group" *ngFor="let fruit of fruits">
         <li class="list-group-item" (click)="onDelete(fruit)">{{fruit}}</li>
       </ul>
     </div>
   </div>
 </div>
</body>
</html>

<router-outlet></router-outlet>





We can pass array inside animation

transition('shrink <=> *', [style({'background-color': 'orange'}),
     animate(1000, style({
       borderRadius: '50px'
     })), animate(5000)
   ]

Using void without binding the property


trigger('list1', [
     state('in', style({
       opacity: 0,
       transform: 'translateX(0)'
     })),
     transition('void => *', [style({
       opacity: 0,
       transform: 'translateX(-100px)'
     }),
   animate(300)
   ]),
     transition('* => void', [
       animate(300, style({
         opacity: 0,
         transform: 'translateX(100px)'
       }))
     ])
   ])



Using Key frame we use to which frame you want to use animation

trigger('list2', [
     state('in', style({
       opacity: 0,
       transform: 'translateX(0)'
     })),
     transition('void => *', [
       animate(1000, keyframes([
         style({
           opacity: 0,
           transform: 'translateX(100px)',
         }),
         style({
           opacity: 0.5,
           transform: 'translateX(-50px)',
         }),
         style({
           opacity: 1,
           transform: 'translateX(-20px)',
         })
       ]))
     ]),
     transition('* => void', [
       animate(300, style({
         opacity: 0,
         transform: 'translateX(100px)'
       }))
     ])
   ])

Here goes full code

import { Component, ViewChild, ElementRef } from '@angular/core';
import { trigger, state, transition, animate, style, keyframes } from '@angular/animations';
@Component({
 selector: 'app-root',
 templateUrl: './app.component.html',
 styleUrls: ['./app.component.css'],
 animations: [
   trigger('divState', [
     state('normal', style({
       'background-color': 'red',
       transform: 'translateX(0px)'
     })),
     state('highlighted', style({
       'background-color': 'green',
       transform: 'translateX(100px)'
     })),
     transition('normal <=> highlighted', animate(300)),
     // transition('highlighted => normal', animate(800)),
   ]),
   trigger('wildCard', [
     state('normal', style({
       'background-color': 'red',
       transform: 'translateX(0px) scale(1)'
     })),
     state('highlighted', style({
       'background-color': 'green',
       transform: 'translateX(100px) scale(1)'
     })),
     state('shrink', style({
       'background-color': 'blue',
       transform: 'translateX(200px) scale(0.5)'
     })),
     transition('normal => highlighted', animate(300)),
     transition('highlighted => normal', animate(800)),
     transition('shrink <=> *', [style({'background-color': 'orange'}),
     animate(1000, style({
       borderRadius: '50px'
     })), animate(5000)
   ]
   ),
   ]),
   trigger('list1', [
     state('in', style({
       opacity: 0,
       transform: 'translateX(0)'
     })),
     transition('void => *', [style({
       opacity: 0,
       transform: 'translateX(-100px)'
     }),
   animate(300)
   ]),
     transition('* => void', [
       animate(300, style({
         opacity: 0,
         transform: 'translateX(100px)'
       }))
     ])
   ]),
   trigger('list2', [
     state('in', style({
       opacity: 0,
       transform: 'translateX(0)'
     })),
     transition('void => *', [
       animate(1000, keyframes([
         style({
           opacity: 0,
           transform: 'translateX(100px)',
         }),
         style({
           opacity: 0.5,
           transform: 'translateX(-50px)',
         }),
         style({
           opacity: 1,
           transform: 'translateX(-20px)',
         })
       ]))
     ]),
     transition('* => void', [
       animate(300, style({
         opacity: 0,
         transform: 'translateX(100px)'
       }))
     ])
   ])
 ]
})
export class AppComponent {
 state = 'normal';
 wildCard = 'normal';
 @ViewChild('update') update: ElementRef;
 fruits = ['mango', 'banana', 'Apple'];
 title = 'angular-animation';
 onAdd() {
   console.log(this.update.nativeElement.value);
   this.fruits.push(this.update.nativeElement.value);
 }
 onDelete(item) {
   this.fruits.splice(this.fruits.indexOf(item), 1);
 }
 onAnimate() {
   this.state === 'normal' ? this.state = 'highlighted' : this.state = 'normal';
   this.wildCard === 'normal' ? this.wildCard = 'highlighted' : this.wildCard = 'normal';
   console.log(this.state);
 }
 onShrink() {
   this.wildCard = 'shrink';
   console.log(this.wildCard );
 }
}




In Html just add 
[@list1] to use the animation and bind the property

Animate buy using group

Just add the grouping into the animations 

group([
         animate(300, style({
           color: 'red'
         })),
         animate(300, style({
           opacity: 0,
           transform: 'translateX(100px)'
         }))
       ]
       )

We can call back the animation using
Built in start and done property
  <div [@divState]="state" (@divState.start)="eventStart($event)"
      (@divState.done)="eventDone($event)"













NGRX State Management

State< -> reducer<-> action<-> component

Npm install ngrx/store

To create action and reducers

We need to create reducers function i.e immutable
Example


export interface State {
   isLoading: boolean;
}

const initialState: State = {
  isLoading: false
};
// action will take from dispachers
export function appReducer(state = initialState , action ) {
   console.log(action.type);
   switch (action.type) {
       case 'START_LOADING':
        return {
           isLoading: true
        };
        case 'STOP_LOADING':
        return {
           isLoading: false
        };
        default:
        return state;
   }
}


In App.module we need to import the store file
StoreModule.forRoot({ui: appReducer}),

After that we need to dispatch the action using stroe 

this.store.dispatch({type: 'START_LOADING'});
this.store.dispatch({type: 'STOP_LOADING'});

Then we need to observe the action

this.loadingBar = this.action.pipe(map(data => data.ui.isLoading ));
  this.loadingBar.subscribe(
   (data) => console.log(data)
  );



















