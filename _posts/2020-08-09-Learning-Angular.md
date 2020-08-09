---
layout: post
title: "Learning Angular"
date: 2020-08-09 18:00:00
tags: Development
image: 2020-08-09-Learning-Angular/Angular.png

---

Angular is a framework designed for creating single page apps. It uses TypeScript, a strongly typed superset of JavaScript, and it is meant for building complete solutions instead of just the UI, making it more complex than React and Vue. Essentially, Angular organizes code into components and solves many common scenarios with powerful syntax and features.

This article is essentially a barebones outline of [Angular's Tour of Heroes tutorial](https://angular.io/tutorial), mostly covering keywords.

## Getting Started

With npm, you can get started with Angular in four command prompt lines.

```
> npm install -g @angular/cli
> ng new app-name
> cd app-name
> ng serve
```

This will install the Angular CLI, build and serve your app, and rebuild whenever files are changed.

In the case that you are using an existing project, you must run `npm install` to install all of its dependencies.

## Components 

> Components are the fundamental building blocks of Angular applications. They display data on the screen, listen for user input, and take action based on that input
>
> https://angular.io/tutorial/toh-pt0#angular-components

They have three main files:

1. component-name.component.ts: the Typescript class 
2. component-name.component.html: the template
3. component-name.component.css: component specific styles

The way I'm thinking of it is that the structure is essentially just the classic HTML, CSS, JS trio but extremely modularized, with you being able to create a component for essentially any part of an application. For example, your header could be a component, but the links in that header could be a component, and the entire layout could be a component containing the rest of the components. To create these components and set them up execute `ng generate component component-name` with the CLI.

### component.ts

Has three parts:

- Imports: to use interfaces, other components, parts of Angular, or whatever else.
- @component: specifies the metadata for the component, like the element selector and the location of the component's files.
- export class: so it can be imported and used elsewhere. This class contains the logic and data for the component, which can be used in the template. For example, in the component we can declare a variable: `name = 'Justin'`. Then in the HTML, we can call and display that variable with `{ {name} }` (I had to put spaces between the brackets because Liquid does something similar). This is called one way data binding, or interpolation.

Then, to actually use the component, simply call its element selector in the parent component's HTML: `<component-name></component-name>`.

In the export class there should also be a constructor and `ngOnInit()`. `ngOnInit()` is called after the component is created and performs initialization logic, while the constructor generally just handles dependency injection, which is covered later.

## Two-Way Data Binding

Inputting and altering data in forms is very streamlined under the two-way data binding. In our component HTML we can have something like `<input [(ngModel)]="person.name" placeholder="name"/>`. This binds person.name to the input so that data flows both from person.name in the TypeScript to the input and the other way.

However, we need to make sure that Angular has ngModel to work with, so in `app.module.ts`, we must `import { FormsModule } from '@angular/forms';` 

## Structural Directives

These add and remove DOM elements by putting directives within the related tags, cutting down on HTML and on logic used to hide UI elements.

### ngIf

`<div *ngIf="aBoolean"> Hi </div>`

Here, if the aBoolean is true, then the div will appear in the DOM and 'Hi' will be displayed. If aBoolean is false, then the div is excluded from the DOM.

`<div *ngIf="name"> Hello </div>`

In this case, if name is undefined, then the div is removed from the DOM, but if name has a value, then the div will display the name by way of one way binding. Finally, we can even handle an else statement like so: 

```
<div *ngIf="something; else #elseBlock">
    If
</div>
<ng-template #elseBlock> 
    Else 
<ng-template>
```

### ngFor

This is a for loop that directly creates DOM objects, making it particularly handy for lists of data.

``` 
<li *ngFor="let element of list">
    element.property
</li>
```

This will create a list item for every element in the list. Note that this is a for each loop, similar to Python, which abstracts the loop a bit by providing the data directly instead of direct control of the index. However, you can access it with `<div *ngFor="let element of list; index as i>`.

## Click Events 

To add a click event to an element, simply add `(click)="function(param)"` to it, then define that function in the component's typescript file like:

```
function(param: type): returnType {
    doSomething;
}
```

## Property Binding

If we want control over a child component from a parent component, we use property binding. In the HTML tag for the component we can add a new property and assign to it like so `<child-component [property]="value"></child-component>`. Then in the child component, we define the property: `@Input() property: type;`, which can then be used in the template or wherever else.

## Services

> Components shouldn't fetch or save data directly... They should focus on presenting data and delegate data access to a service.
>
> https://angular.io/tutorial/toh-pt4#why-services

Therefore, services are meant to share information among components.

Use the CLI to make a service: `ng generate service service-name`.

You'll notice that the file generated is similar to that of a component, but instead of @Component, it has @Injectable, meaning it participates in dependency injection.

We will add a getter to the service:

```
getter(): type {
    return something;	
}
```

Now, inject the service into the component it's needed in and add the service to the constructor: `contructor(private serviceName: ServiceName)`. This sets serviceName to a singleton instance of ServiceName. Then, we use the service by using `this.serviceName.getter();`. The best practice is to create a getter method in the component, and then call it within `ngOnInit()`.

This usage creates an issue in that the getter is synchronous. If we were fetching data from a server, this would block the browser while it waits for the server to respond, not ideal. Therefore, the tutorial opts to use Observables from RxJS. To do that, in the service, `import {Observable, of} from 'rxjs';`, alter the getter return type to `Observable<type>`, and `return of(variable)`. Then, in the component, we must subscribe to the getter, allowing for an asynchronous wait on the Observable.

One useful way of managing services is importing one service into another, then injecting just one service into a component.

## Routing

Angular is meant to create single-page apps, so routing is done by showing and hiding components rather than fetching a new HTML file. However, the URL still changes, making the site look like it has multiple pages, and necessitating extra management of routing.

> In Angular, the best practice is to load and configure the router in a separate, top-level module that is dedicated to routing and imported by the root `AppModule`.
>
> https://angular.io/tutorial/toh-pt5#add-the-approutingmodule

Generate this with `ng generate module app-routing --flat --module=app`.

Another possibility is to create the app with routing set up in the first place: `ng new app-name --routing`.

In this routing module, a routes list is used to define URL paths and their corresponding components: `const routes: [Routes] = [{ path: 'path', component: Component }]` . You can also do redirects in here, like from the root: `{path: '', redirectTo: '/path', pathMatch: 'full'}`.  Now in the HTML, you can route like `<a routerLink="/path">link</a>`. 

For routes that hold information for the specific page, like an id, a path can be generalized like `{path: 'path/:id', component: idComponent}`. Then, to use that information in the related component, import `ActivatedRoute` and inject it in the constructor: `private route: ActivatedRoute`. Finally, use the route with something like `const id = +this.route.snapshot.paramMap.get('id')`.

There are some more specific changes that need to be made to create a router that can be found at [https://angular.io/api/router/Routes](https://angular.io/api/router/Routes).

## HTTP

Angular provides its own mechanism for communicating with servers via HTTP. After a [number of steps to enable HTTP services](https://angular.io/guide/http#setup-for-server-communication), we can begin using the HTTP client. Since this is manipulation of data, all this functionality should be handled by a service. The related component only gets the action from the user, relays it to the service, then back to the user. In that relay, the call from the component must be subscribed to in a way like: 

```
this.service.httpFunction().subscribe(callback action)
```

 The service would then likely have some of the following functions.

### Get

``` 
getter(): Observable<Type> {
    return this.http.get<Type>(apiUrl)
}
```

The tutorial further suggests to handle errors by adding `.pipe(catchError(this.handleError<type>('getter', [])));` to the return. You then create a `handleError()`.

### Put 

Update data like so:

``` 
update(data: type): Observable<any> {
    return this.http.put(apiUrl, data, httpOptions)
}
```

We can of course add a catch error here as well. The same is true for the following functions.

### Post

```
add(data: type): Observable<Type> {
    return this.http.post(apiUrl, data, httpOptions)
}
```

### Delete

```javascript
delete(data: type): Observable<Type> {
    return this.http.delete(apiUrl, httpOptions)
}
```

### Search

This is essentially just a series of gets. However, we need to make sure that we don't make unnecessary requests. There is a decent amount of code [here](https://angular.io/tutorial/toh-pt6#search-by-name), so I won't restate it, but essentially you make a search component with an input box and search results with `*ngFor`. Then, that component calls a service which performs the get. There are a couple other key considerations though. Firstly, in the service, we ensure that a get is never executed if the search is empty, then in the component, we actually wait a small period of time between keystrokes and only search if the term is different that the last. These methods reduce the amount of gets that are executed and lower unnecessary bandwidth consumption.

## Conclusion

This only covers the tutorial from the Angular docs, and concepts go much deeper than this. Angular is meant to be a fully fledged solution for an application so there are a lot of features to get familiar with. However, with this tutorial, I felt I was able to at least look at an Angular project and have an idea of how things are working.

At its most basic, Angular uses components to organize the project, cut down on repeating code, and ease the use of data moving through the application. Then, TypeScript serves to communicate with an api, calculate its own logic, perform routing, and pass and receive data with the HTML.

## Future Considerations

Angular is one of the three most popular web frameworks/libraries, with the other two being React and Vue. React is the most popular of them, while Angular tends to be more popular with enterprises. Knowing these frameworks is essential in web development as plain JavaScript is not enough anymore. Some of their concepts, such as components, overlap, making learning the others much more simple once you've used one. 

I'm curious about learning React and its static site generator Gatsby next, as they are a very popular pairing and a likely candidate for my future projects.