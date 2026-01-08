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
- Interpolation ({{ }}) – Used to display component data in the template.
- Property binding ([property]) – Used to bind data from the component to HTML element properties.
- Event binding ((event)) – Used to handle user events like clicks or input changes.
- Two-way binding ([(ngModel)]) – Combines property and event binding to keep data in sync between the view and component.
I’ve used two-way binding mostly in forms and event/property binding for dynamic UI interactions.

## Q3. Difference between constructor and ngOnInit()
The constructor is used mainly for dependency injection, such as injecting services into the component.
It should not contain heavy logic.
ngOnInit() is a lifecycle hook that runs after Angular initializes the component and its input properties.
It is the ideal place to perform initialization logic, such as API calls or setting up data for the view.
In real projects, I inject services in the constructor and place business or API logic inside ngOnInit().

## Q4. What is Dependency Injection?
Dependency Injection is a design pattern where Angular provides required dependencies, such as services, to a class instead of the class creating them itself.
This improves reusability, testability, and maintainability.
Angular implements DI using its built-in injector and the @Injectable() decorator.
In real projects, I use DI to inject services like API services, authentication services, and shared utility services into components.

## Q5. What are directives?
Directives are used to manipulate the DOM or change the behavior of elements.
Angular has three types of directives:
- Structural directives – Modify the DOM structure, such as *ngIf, *ngFor, and *ngSwitch.
 - Attribute directives – Modify the appearance or behavior of elements, such as ngClass and ngStyle.
- Custom directives – Used to create reusable DOM behavior like auto-focus or permission-based rendering.
I frequently use structural and attribute directives in real applications.

## Q6. ngIf vs hidden
*ngIf adds or removes elements from the DOM, whereas hidden only hides the element using CSS while keeping it in the DOM.
I prefer ngIf when:
- The element is not required at all
- Performance or security is a concern

I use hidden when:
- The element needs to stay in the DOM
- Toggling visibility frequently without recreating the element

## Q7. Change Detection & OnPush
Change Detection is the mechanism Angular uses to update the view when data changes.
Default strategy checks all components whenever any event occurs.
OnPush strategy checks a component only when:
- An @Input() reference changes
- An observable emits a new value
- An event occurs inside the component
I use OnPush in performance-critical components like dashboards or large lists to reduce unnecessary checks.

## Q8. RxJS & Observable vs Promise
RxJS is a reactive programming library used extensively in Angular to handle asynchronous data streams.
#### Observable vs Promise:
- Promises handle a single value.
- Observables can handle multiple values over time, can be cancelled, and support powerful operators.
Angular’s HttpClient returns observables, which makes it easy to combine API calls, manage streams, and unsubscribe using async pipe or takeUntil.
