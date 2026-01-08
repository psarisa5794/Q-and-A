  # Level 1 Interview Questions 
## Q1. Explain Angular architecture
Angular is a component-based and modular frontend framework.
The core building block is a component, which consists of a TypeScript class, an HTML template, and CSS styles.
Components handle UI logic and rendering.
Related components, services, and pipes are grouped into modules, which help organize the application.
Services are used to handle business logic and data access and are injected into components using Angular’s dependency injection system.
Templates define how data is displayed using bindings and directives, while Angular handles change detection to keep the UI in sync with data.

## Q2. What is data binding? Explain types
Data binding is the mechanism that allows communication between the component class (TypeScript) and the template (HTML).
Angular supports four types of data binding:
- **Interpolation ({{ }})** – Used to display component data in the template.
- **Property binding ([property])** – Used to bind data from the component to HTML element properties.
- **Event binding ((event))** – Used to handle user events like clicks or input changes.
- **Two-way binding ([(ngModel)])** – Combines property and event binding to keep data in sync between the view and component.
I’ve used two-way binding mostly in forms and event/property binding for dynamic UI interactions.

## Q3. Difference between constructor and ngOnInit()
The constructor is used mainly for dependency injection, such as injecting services into the component.
It should not contain heavy logic.
Historically it was the primary place to perform dependency injection like injecting services like **Router**, **HTTPClient**.
However modern Angular 14 & above we can also use the `inject()` function to handle dependency injection.

Regardless of which injectino style we use, the constructor should remain lightweight. We generally avoid writing business logic there,
prefering **ngOnInit()** for initialization logic because input bindings (`@Input()`) are not yet available inside constructor.

**ngOnInit()** is a lifecycle hook that runs after Angular initializes the component and its input properties.
It is the ideal place to perform initialization logic, such as API calls or setting up data for the view.
In real projects, I inject services in the constructor and place business or API logic inside ngOnInit().

Example: 
```typescript
constructor(private userService: UserService) {}

ngOnInit() {
  // We write initialization logic here
  this.userService.fetchUsers().subscribe(users => this.users = users);
}
```

## Q4. What is Dependency Injection?
Dependency Injection is a design pattern where Angular provides required dependencies, such as services, to a class.
This improves reusability, testability, and maintainability.
Angular implements DI using its built-in `injector` and the `@Injectable()` decorator.
In real projects, I use DI to inject services like API services, authentication services, and shared utility services into components.

## Q5. What are directives?
Directives are used to manipulate the DOM or change the behavior of elements.
Angular has three types of directives:
- **Structural directives** – Modify the DOM structure, such as `*ngIf`, `*ngFor`, and `*ngSwitch`.
- **Attribute directives** – Modify the appearance or behavior of elements, such as `ngClass` and `ngStyle`.
- **Custom directives** – Used to create reusable DOM behavior like auto-focus or permission-based rendering.
  
I frequently use structural and attribute directives in real applications.

Examples: 

**TypeScript(.ts)**
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-example',
  templateUrl: './example.component.html'
})
export class IfExampleComponent {
  isLoggedIn: boolean = true;

  status = 'pending'; // can be 'active', 'pending', or 'inactive'

  // list of users
  users = [
    { id: 1, name: 'Alice' },
    { id: 2, name: 'Bob' },
    { id: 3, name: 'Charlie' }
  ]
}

```

**template (.HTML)**
```html
<!-- Simple condition -->
<div *ngIf="isLoggedIn">
  Welcome, user!
</div>

<!-- With else block using <ng-template> -->
<div *ngIf="!isLoggedIn; else loginTemplate">
  Please log in.
</div>
```

## Q6. ngIf vs hidden
`*ngIf` adds or removes elements from the DOM, whereas hidden only hides the element using CSS while keeping it in the DOM.
I prefer ngIf when:
- The element is not required at all
- Performance or security is a concern

I use `hidden` when:
- The element needs to stay in the DOM
- Toggling visibility frequently without recreating the element

## Q7. Change Detection & OnPush
Change Detection is the mechanism Angular uses to update the view when data changes.
Default strategy checks all components whenever any event occurs.
OnPush strategy checks a component only when:
- An `@Input()` reference changes
- An **observable** emits a new value
- An event occurs inside the component
I use OnPush in performance-critical components like dashboards or large lists to reduce unnecessary checks.

## Q8. RxJS & Observable vs Promise
**RxJS** is a reactive programming library used extensively in Angular to handle **asynchronous data streams**.
#### Observable vs Promise:
A **Promise** is an object that represents a value that you don't have yet, but will have in future.
- It is a placeholder of a result of an asynchronous operation.
- Promises handle a single value.

An **Observable** is a part of Angular's reactive programming.
- Observables can handle multiple values over time, can be cancelled, and support powerful operators.

Angular’s HttpClient returns observables, which makes it easy to combine API calls, manage streams, and unsubscribe using async pipe or takeUntil.

## Q9. What is a Service ?
- An angular service is used to encapsulate business logic, data access and reusable functionality.
- Components focus of UI logic while services handle API communications, state management, shared logic.
  
This Separation improves code maintainability, resusability, and testability.
```typescript
@Injectable({ providedIn: 'root' })
export class UserService {}
```

## Q10. What is Lazy Loadind ?
**Lazy loading** is a technique where feature modules are loaded only when required instead of loading the entire application upfront.
In improves initial load time, Application performance.

I have implemented lazy loading using loadChildren in angular routing. especially for large modules (or) components.
```typescript
{
  path: 'admin',
  loadChildren: () =>
    import('./admin/admin.module').then(m => m.AdminModule)
}
```

# Level-2 Interview Questions.

## Q11. Why does Angular HttpClient return Observables instead of Promises ?
Angulr's HttpClient returns **Observables** instead of Promises because Observables are more powerfull for handling asynchronous data streams.

Observables Supports: 
- Multiple emitted values over time.
- Cancellation using unsubscription.
- Provides powerfull operations like **map, filter, switchMap** and **retry**.

In real applications, this allows us to cancel unnecessary HTTP requests, chain dependent API calls, and manage complex async workflows.

Promises on the other hand, emit only a single value and cannot be cancelled once executed.

## Q12. Explain Angular lifecycle hooks in order. Which ones have you used ?
Angular lifecycle hooks allow us to tap into different stages of a component’s life.

The commonly used hooks are:
- `constructor()` – Used for dependency injection only
- `ngOnInit()` – Used for initialization logic and API calls
- `ngOnChanges()` – Triggered when input properties change
- `ngAfterViewInit()` – Used when accessing child components or DOM elements
- `ngOnDestroy()` – Used to clean up subscriptions and avoid memory leaks

In real projects, I mostly use ngOnInit for API calls and ngOnDestroy to unsubscribe from observables.

## Q13. Template-Driven Forms vs Reactive Forms
Template-Driven Forms are simple and rely heavily on the template using `ngModel`. They are suitable for small forms with minimal validation.

Reactive Forms are model-driven and created in the component class using `FormGroup`, `FormControl`, and `FormBuilder`.
They provide better control, scalability, and testability.

In enterprise applications, I prefer Reactive Forms because they support complex validations, dynamic form controls, and better state management.

## Q14. How do you handle validation in Reactive Forms?
Reactive Forms support three types of validators:

- Built-in validators like `Validators.required`, `Validators.email`, and `Validators.minLength`
- Custom validators, where we write a function that receives a `FormControl` and returns validation errors
- Async validators, which are used when validation depends on an API call, such as checking username availability

In the template, I access validation state using `formControl.touched` and `formControl.invalid` to show error messages dynamically.

## Q15. What are route guards?
Route guards are used to control access to routes based on certain conditions.

Common types of guards include:
- `CanActivate` – Controls access to a route
- `CanLoad` – Prevents lazy-loaded modules from loading
- `CanDeactivate` – Prevents navigation away from a route
  
I have used `CanActivate` extensively for authentication and role-based authorization to restrict access to protected pages.

## Q16. What is the async pipe and why is it preferred?
The **async pipe** allows us to subscribe to observables directly in the template.

It automatically:

- Subscribes to the observable
- Updates the UI when new data arrives
- Unsubscribes when the component is destroyed

This prevents  subscription logic in the component class.
```html
<div *ngIf="users$ | async as users">
  {{ users.length }}
</div>
```

## Q17. Subject vs BehaviorSubject vs ReplaySubject
A **Subject** does not store any value, subscribers only receive values emitted after subscription.

A **BehaviorSubject** stores the latest value and immediately emits it to new subscribers. This is useful for shared state like logged-in user data.

A **ReplaySubject** replays a specified number of previous values to new subscribers.

In Angular, I mostly use BehaviorSubject for state sharing across components.

## Q18. How do you unsubscribe from Observables?
To avoid memory leaks, Angular provides multiple ways to unsubscribe:

- Manually unsubscribing in ngOnDestroy
- Using takeUntil with a destroy subject
- Using the async pipe

In complex components with multiple subscriptions, I prefer takeUntil as it provides cleaner and scalable cleanup logic.

## Q19. What is takeUntil and when do you use it?

`takeUntil` is an RxJS operator that automatically completes an observable when another observable emits a value.

I commonly use it with a `destroy$` subject to automatically unsubscribe from all streams when a component is destroyed.

This is especially useful in components with multiple subscriptions and long-lived observables.

## Q20. Difference between mergeMap, switchMap, concatMap
- `mergeMap` runs multiple inner observables in parallel
- `concatMap` runs inner observables sequentially
- `switchMap` cancels the previous observable and switches to the latest one

In Angular HTTP calls, I most commonly use `switchMap`, especially for search or dependent API calls, because it prevents outdated requests from completing.

# Level 3 Interview Questions
## Q21. Performance bottlenecks in large Angular applications & how to fix them
In large Angular applications, common performance bottlenecks include excessive change detection cycles, rendering large DOM lists, unoptimized API calls, and large bundle sizes.

I usually identify these issues using Angular DevTools, browser performance profiling, and by observing UI freezes or slow dashboard loads.

To fix them:
- I use ChangeDetectionStrategy.OnPush to limit unnecessary change detection
- Use `trackBy` with `*ngFor` to avoid re-rendering entire lists
- Apply virtual scrolling (`cdk-virtual-scroll-viewport`) for large datasets
- Implement server-side pagination and filtering
- Optimize API calls using RxJS operators like switchMap and caching

These changes significantly improve rendering speed and overall user experience.

## Q22. Explain ChangeDetectionStrategy.OnPush
ChangeDetectionStrategy.OnPush tells Angular to run change detection for a component only when specific conditions are met.

Change detection is triggered when:
- An `@Input()` reference changes
- An observable emits a new value (commonly via async pipe)
- A DOM event occurs inside the component
- Change detection is triggered manually

A common mistake developers make is mutating objects instead of creating new references, which prevents OnPush components from updating.

When used correctly, OnPush significantly improves performance in complex UIs.

## Q23. What is trackBy and why is it important?
By default, Angular re-renders all DOM elements in an `*ngFor` loop whenever the data changes.

`trackBy` allows Angular to uniquely identify each item using a key, such as an ID.
This helps Angular update only the modified items instead of recreating the entire list.

In large tables or dashboards, using trackBy greatly improves rendering performance and reduces DOM operations.

## Q24. What are Angular Signals?
Angular Signals are a new reactive primitive introduced to simplify state management.

Signals provide fine-grained reactivity without relying on RxJS or zone-based change detection.

Signals are synchronous, simple, and ideal for managing local UI state.

RxJS is still preferred for asynchronous workflows like HTTP calls.

Signals improve performance, reduce boilerplate code, and make state changes more predictable.

Example : 
```typescript
count = signal(0);
increment() {
  this.count.update(v => v + 1);
}
```

## Q25. Optimizing large dashboards or tables
For large dashboards, I focus on both frontend and backend optimization.

On the backend:
- Implement server-side pagination, filtering, and sorting

On the frontend:
- Use virtual scrolling
- Use trackBy in lists
- Apply OnPush change detection
- Lazy load heavy components

This approach minimizes DOM rendering and improves responsiveness.

## Q26. State management approaches in Angular
Angular state management depends on application size.
- For small apps, component state is sufficient
- For medium apps, services with BehaviorSubject work well
- For large enterprise apps, NgRx is useful for predictable state, debugging, and scalability

I usually start simple and introduce NgRx only when state complexity grows.

## Q27. What is an Angular interceptor?
Angular HTTP interceptors allow us to intercept and modify HTTP requests and responses globally.

Common use cases include:
- Attaching authentication tokens
- Handling global API errors
- Logging requests
- Modifying headers

Interceptors help keep components clean and centralize cross-cutting concerns.

## Q28. What are standalone components?
Standalone components allow Angular components to exist without being declared in an NgModule.

Dependencies like pipes, directives, and modules are imported directly into the component.

This simplifies architecture, improves tree-shaking, and reduces boilerplate.

Standalone components are ideal for modern Angular applications and micro-frontends.

## Q29. Designing scalable Angular architecture
- I design Angular applications using a feature-based folder structure.
- Each feature contains its own components, services, and routing.
- Shared utilities and UI components go into shared folders.
- Business logic is kept in services, while components focus on UI.
- This approach improves maintainability and team collaboration.

## Q30. Securing Angular frontend applications
Frontend security includes:

- Route guards for authentication and authorization
- Role-based access control (RBAC)
- HTTP interceptors for token handling
- Avoiding sensitive data storage in the frontend
- Preventing XSS using Angular’s built-in sanitization

Angular handles CSRF and XSS protections by default, but correct usage is critical.

## Q31. AOT vs JIT compilation
- JIT compiles templates in the browser, which is slower and used mainly during development.
- AOT compiles templates at build time, resulting in faster startup, smaller bundles, and early error detection.

AOT is preferred in production builds for performance and reliability.

## Q32. Angular Universal (SSR)
Angular Universal enables server-side rendering.

It improves SEO, first contentful paint, and performance on low-end devices.

SSR is ideal for public-facing applications but usually unnecessary for internal dashboards.

## Q33. Error handling in Angular
I handle errors at multiple levels:

- Use HTTP interceptors for API error handling
- Use global error handlers for unexpected errors
- Show user-friendly messages using toasts or alerts

Centralized error handling keeps components clean and improves UX.

## Q34. Handling a poorly written Angular codebase
I first focus on understanding the application architecture and identifying critical issues.

My priorities are:

- Security vulnerabilities
- Application stability
- Performance bottlenecks

Then I refactor gradually:
- Improve folder structure
- Introduce reusable components
- Fix performance issues
- I avoid risky large rewrites and focus on incremental improvements.
