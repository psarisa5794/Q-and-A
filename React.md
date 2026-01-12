## Q1. Introduce yourself from a React frontend developer perspective
Hi, my name is [you name]. I have over three years of experience building dynamic and scalable web applications using React and Angular.

In React, I’ve worked on multiple real-world projects. One key project was an internal ticketing system where employees could raise IT or HR-related tickets. I focused on building reusable components, implementing role-based access control, and protecting routes using authentication guards.

I used Redux for state management, lazy loading for performance optimization, and Firebase Cloud Messaging to notify users about ticket updates. For security, I implemented JWT-based authentication with HTTP-only cookies.

I always focus on writing clean, secure, and maintainable React code while delivering a responsive and smooth user experience.
## Q2. What problem does React solve? Why React over plain JavaScript or jQuery?
When applications are built using plain JavaScript or jQuery, managing UI updates and maintaining large codebases becomes difficult as the application grows.

React solves this problem using a component-based architecture, where the UI is broken into small, reusable components. This improves readability, reusability, and maintainability.

React also uses a Virtual DOM, which updates only the necessary parts of the UI instead of re-rendering the entire page, improving performance.

Because of its declarative approach and scalability, React is a better choice for modern, large-scale applications.

## Q3. What is JSX? Why does React use JSX?
JSX stands for JavaScript XML. It is a syntax extension that allows us to write HTML-like code inside JavaScript.

JSX makes UI code more readable and helps keep UI structure and logic in one place. We can embed JavaScript expressions inside JSX using curly braces.

Although JSX looks like HTML, it is compiled into JavaScript by Babel, which React uses to efficiently update the Virtual DOM.

## Q4. What is a React component? Functional vs Class components
A React component is a reusable and independent building block of the UI.

There are two types of components: class components and functional components. Earlier, class components were used to manage state and lifecycle methods, but today functional components are preferred.

Functional components are simpler, easier to test, and use hooks like useState and useEffect to manage state and side effects.

Components promote reusability—for example, a Button component can be reused across multiple pages by passing different props.

## Q5. What are props? What is prop drilling?
Props are inputs passed from a parent component to a child component. They are read-only and follow a one-way data flow.

Prop drilling occurs when data has to be passed through multiple intermediate components just to reach a deeply nested child.

To avoid prop drilling, I’ve used the Context API. For larger applications, I prefer Redux, which provides centralized state management and acts as a single source of truth.

## Q6. What is state? Difference between state and props
State represents data that belongs to a component and can change over time. When state changes, React re-renders the component.

Props are passed from parent to child and are read-only.
The key difference is that state is managed internally by the component, while props are external inputs.

## Q7. Explain useState with an example
In React, updating a normal JavaScript variable does not trigger a re-render.
The useState hook allows us to create state variables and update them using a setter function. When state updates, React re-renders the component.
For example, in a counter component, clicking a button updates the count using the setter function, and the UI updates automatically.

## Q8. What is useEffect? Dependency array? Common mistake

useEffect is used to handle side effects such as API calls, subscriptions, or timers in functional components.

The dependency array controls when the effect runs:

- Empty array → runs once
- With dependencies → runs when dependencies change
  
A common mistake is missing or incorrect dependencies, which can cause infinite re-renders.

useEffect can also return a cleanup function to clear subscriptions or timers.

## Q9. How did you handle API calls in React?

I used Axios for making API calls.

For simpler components, I handled API calls inside useEffect and managed loading and error states using useState.

In complex applications, I used Redux-Saga to centralize API logic, manage loading and error states, and improve scalability using generator functions.

## Q10. What is conditional rendering?

Conditional rendering means displaying different UI elements based on a condition.

In React, we use operators like && and the ternary operator.

For example, I used conditional rendering to show different dashboards based on user roles or to show loaders while data is loading.

## Q11. Controlled vs Uncontrolled components (Forms)

In controlled components, form inputs are managed using React state and updated via onChange handlers.

Uncontrolled components rely on the DOM and use useRef to access values.

I prefer controlled components because they provide better control, validation, and dynamic behavior.

## Q12. What is the key prop?

The key prop uniquely identifies list items in React.
It helps React efficiently update the UI during reconciliation.
Using incorrect or missing keys can cause performance issues and unexpected UI behavior.
Stable unique IDs are preferred over array indexes.

## Q13. React performance issues you faced

I faced issues like UI flickering and slow list rendering.
The main cause was incorrect useEffect dependency usage, which caused continuous re-renders.
I fixed this by optimizing dependency arrays and restructuring state updates to avoid infinite loops.

## Q14. Difference between useMemo and useCallback

useMemo is used to memoize computed values, while useCallback is used to memoize **functions`.

I use useMemo when a calculation is expensive and should not re-run on every render.

I use useCallback when passing functions as props to child components to avoid unnecessary re-renders.

For example, in a dashboard with filters, I used useMemo to cache filtered data and useCallback for event handlers passed to child components.

## Q15. Context API vs Redux – When to use which?

I use Context API for small to medium-sized applications where the state is simple, such as theme, language, or user session.

I avoid Context when the application has complex state logic or frequent updates because it can cause unnecessary re-renders.

For large-scale applications, I prefer Redux because it provides centralized state management, better debugging, and predictable state updates.

## Q16. How Redux works internally (Actions, Reducers, Store)

Redux works on a unidirectional data flow.
1. Actions describe what happened.
2. Reducers describe how the state changes.
3. The store holds the global state of the application.

 When an action is dispatched, it goes to the reducer, which returns a new state, and the store updates the UI accordingly.
## Q17. Redux-Saga vs Redux-Thunk
Redux-Thunk is good for simple async logic, but it becomes hard to manage when the application grows.

I chose Redux-Saga because it separates side effects from components and reducers. It uses generator functions, which makes async flows easier to test and manage.

Saga is especially useful when handling complex workflows like retries, parallel API calls, or background tasks.

## Q18. Authentication & Authorization flow in React
I handle authentication by storing the token securely, usually in HTTP-only cookies.
On app load, I validate the user session and store user details in global state.
Authorization is handled using role-based access control, where UI components and routes are rendered based on user roles.
## Q19. How do you protect routes in React?

I use protected routes by wrapping routes with an authentication check.
If the user is not authenticated, they are redirected to the login page.
For role-based access, I check user roles before rendering the route and show an unauthorized page if access is denied.
## Q20. What are Higher-Order Components (HOC)? Do you still use them?
A Higher-Order Component is a function that takes a component and returns an enhanced component.

Earlier, HOCs were used for code reuse, but today hooks have replaced most use cases.

I rarely use HOCs now and prefer custom hooks instead because they are simpler and more readable.
## Q21. Controlled re-renders & preventing unnecessary re-renders
Controlled re-renders mean ensuring components re-render only when necessary.

I prevent unnecessary re-renders by using React.memo, useMemo, useCallback, and proper state placement.

I also avoid passing new object or function references unnecessarily.
## Q22. What is React.memo? When to use it?
React.memo is used to memoize a component so it only re-renders when its props change.

I use it for pure components that receive the same props frequently.

I avoid using it everywhere because overusing memoization can add unnecessary complexity.
## Q23. Lifting state up – with example
Lifting state up means moving shared state to the nearest common parent component.

For example, if two child components need to share form data, I store the state in the parent and pass it down via props.

This keeps the data flow predictable and consistent.
## Q24. Client-side vs Server-side pagination
Client-side pagination loads all data at once and paginates on the frontend. It works well for small datasets.

Server-side pagination fetches only required data per page and is more scalable.

I prefer server-side pagination for large datasets to improve performance.
## Q25. Handling large lists efficiently in React
I handle large lists by using pagination, virtualization, and proper keys.

I avoid rendering all items at once and only render what is visible to the user.

This significantly improves performance.
## Q26. Issues while integrating REST APIs & solutions
Common issues include inconsistent API responses, error handling, and loading states.

I solved these by creating centralized API services, handling errors globally, and standardizing response handling.
## Q27.  Global error handling in React
I handle global errors using centralized API interceptors and error boundaries.

This ensures consistent error messages and prevents the application from crashing.
## Q28. Real performance optimization you did

I optimized performance by fixing incorrect useEffect dependencies, memoizing expensive calculations, and reducing unnecessary re-renders.

This removed UI flickering and improved load time.
## Q29. Debugging a slow React app in production
I start by analyzing performance using browser dev tools and React DevTools.

I identify unnecessary re-renders, large API payloads, and inefficient state updates.

Then I optimize rendering, API usage, and state management step by step. 
## Q30. How do you structure a large React application?
In large React applications, I follow a modular and feature-based folder structure.

I separate concerns by organizing code into folders like components, pages, hooks, services, store, and utilities.

I also ensure reusable components are isolated, API logic is centralized, and business logic is not mixed with UI code.
This structure improves scalability, readability, and team collaboration.
## Q31. How do you decide what should be local state vs global state?
I keep state local if it is used only within a single component, such as form inputs or UI toggles.

I move state to global state management when it needs to be shared across multiple components, persisted across routes, or used by background processes.

This approach avoids unnecessary complexity while keeping the application predictable.
## Q32. How do you handle API failures gracefully in UI?
I always handle API failures by showing meaningful error messages to users instead of breaking the UI.

I manage loading, success, and error states explicitly and provide retry options when possible.

I also log errors centrally for debugging and monitoring purposes.
## Q33. Explain a complex bug you faced in React and how you fixed it.
I once faced a continuous re-render issue caused by incorrect useEffect dependencies.

I debugged it by identifying which state updates were triggering re-renders and restructuring the logic to avoid updating state inside dependent effects.

Fixing the dependency array resolved UI flickering and performance issues.
## Q34. How do you ensure code quality in React projects?
I ensure code quality by following clean code principles, writing reusable components, and maintaining consistent naming conventions.

I also use linting, code reviews, and unit tests to prevent regressions and improve maintainability.
## Q35. How do you handle security concerns in a React frontend?
I avoid storing sensitive data in local storage and prefer HTTP-only cookies for authentication.

I implement role-based UI rendering, input validation, and follow secure API communication practices.

I also ensure the frontend handles authorization properly and does not rely only on UI checks.
## Q36. How do you collaborate with backend teams effectively?
I collaborate closely with backend teams by clearly understanding API contracts, request/response formats, and error handling strategies.

I proactively communicate frontend requirements and suggest improvements to APIs when needed.

This helps avoid integration issues and improves development speed.
## Q37. How do you handle breaking changes in APIs?
I handle breaking API changes by versioning APIs and updating frontend logic incrementally.

I also ensure backward compatibility when possible and coordinate releases with backend teams to avoid production issues.
## Q38. What do you do if a junior developer writes poor React code?
I review the code constructively, explain why certain approaches are problematic, and suggest better patterns.

I focus on mentoring rather than criticizing, ensuring the developer learns best practices and improves over time.

## Q39. How do you optimize React application load time?
I optimize load time using lazy loading, code splitting, and reducing bundle size.

I also optimize API calls, avoid unnecessary renders, and ensure assets are efficiently loaded.

## Q40. How do you approach feature estimation and delivery?
I break features into smaller tasks, identify dependencies, and estimate based on complexity and risks.

I communicate clearly if timelines need adjustment and ensure quality is not compromised.
## Q41. How do you handle production issues?
I first identify the impact and prioritize user experience.

I analyze logs, reproduce the issue locally, apply a fix, and ensure proper testing before deployment.

I also make sure to add safeguards to prevent similar issues in the future.
## Q42. What makes a React application scalable?
A scalable React application has modular architecture, predictable state management, optimized rendering, and clean separation of concerns.

Scalability also depends on team practices like code reviews and documentation.
## Q43. How do you handle UI consistency across large applications?
I use shared component libraries, design systems, and common styling guidelines.

This ensures consistency, reduces duplication, and improves development speed.
## Q44. How do you stay updated with React ecosystem changes?
I stay updated by reading official React documentation, following community discussions, and experimenting with new features in side projects.

I focus on understanding concepts deeply rather than blindly adopting trends.
## Q45. Why should we hire you as a React frontend developer?
I bring strong hands-on experience in building scalable and secure React applications.

I focus not just on writing code, but on performance, maintainability, and user experience.

I adapt quickly, collaborate well with teams, and take ownership of features from development to production.
