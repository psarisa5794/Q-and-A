# Level 1 Interview Questions
## Q1. What is Node.js and How does it works?
Node.js is a runtime environment that executes JavaScript code outside the web browser using **Chrome V8 Engine**.

**This is how Node.js Actually works**
- **V8 Engine:** Node.js uses Google's open-source V8 JavaScript engine to compile JavaScript code directly into native machine code, providing fast execution speeds.
- **Singel Thread:** Node.js run on a single main thread. This avoids the overhead of managing multiple threads and prevents the potential deadlocks which are common in other server models.
- **Asynchronous Operations** : When a request involves input/output(I/O) operatinos (like reading a file, accessing a database, or making a network call), Node.js does not wait for that operation to complete. Instead it offloads the task and continoues processiong other requests.
- **Libuv Library** : Under the hood, Node.js uses a powerful c++ library called libuv. This library handles the complex, cross-platform asynchronous I/O operations and uses an underlying thread pool for certain blocking tasks, seamlessly managing the operations and notifying the main thread when they are finished.
  
## Q1. What is Node.js? How is it different from traditional backend languages like Java or PHP?

Node.js is a JavaScript runtime environment, not a framework.
It allows JavaScript to run outside the browser using Google’s V8 engine.

In browsers, JavaScript is sandboxed and cannot access system resources like files or networks directly.
Node.js provides built-in modules such as fs, http, and path, which allow JavaScript to interact with the file system, network, and operating system.

Compared to traditional backend languages like Java or PHP, Node.js follows a non-blocking, event-driven architecture.
Even though Node.js runs on a single thread, it can handle thousands of concurrent requests efficiently using the event loop instead of creating a new thread per request.

This makes Node.js highly suitable for I/O-intensive and scalable applications, such as APIs, real-time systems, and microservices.

## Q2. Is Node.js single-threaded or multi-threaded? Explain clearly.

Node.js is single-threaded at the JavaScript execution level, meaning it executes JavaScript code using a single call stack.

However, Node.js is not limited by this single thread because it uses an event-driven, non-blocking architecture powered by the event loop.

When an asynchronous operation like a database query, file read, or API call is initiated, it is offloaded to the system or worker threads.
Node.js does not wait for that operation to complete. Instead, it continues executing other requests.

Once the asynchronous task is completed, its callback (or promise resolution) is placed into the appropriate event loop queue and executed when the call stack is free.

This is how Node.js efficiently handles multiple concurrent requests while still being single-threaded.

## Q3. What is the Event Loop in Node.js? Why is it important?

The event loop is a core mechanism in Node.js that allows it to perform non-blocking asynchronous operations using a single JavaScript thread.

When Node.js encounters an asynchronous task such as a file read, database call, or network request, the task is delegated to the system or worker threads.
Node.js does not wait for the task to complete. Instead, it continues executing other code.

Once the asynchronous operation finishes, its callback or promise resolution is placed into a queue.
The event loop continuously checks whether the call stack is empty and then pushes queued callbacks to the stack for execution.

This mechanism is the main reason Node.js can handle many concurrent I/O operations efficiently without blocking the main thread.

## Q4. What do you mean by non-blocking I/O? Give a real example.

Non-blocking I/O means that Node.js does not wait for an I/O operation to finish before moving on to execute other code.

For example, when a request comes in to fetch data from a database, the database operation may take time to complete.
In Node.js, this database call is executed asynchronously and handed over to the system.

While the database query is running, Node.js continues handling other incoming requests instead of blocking the main thread.

Once the database operation completes, its callback or promise result is queued and executed when the call stack is free.

This non-blocking behavior allows Node.js to handle multiple requests efficiently using a single thread.

## Q5. What are callbacks? What problems do callbacks create?

A callback is a function that is passed as an argument to another function and is executed after an asynchronous operation completes.

In Node.js, callbacks are commonly used to handle results of operations like file reading, database queries, or API calls.

The main problem with callbacks is callback hell, which happens when multiple asynchronous operations are nested inside each other.
This makes the code difficult to read, hard to maintain, and challenging to handle errors properly.

Because of these problems, Promises and later async/await were introduced to make asynchronous code more readable and manageable.

## Q6. What is the difference between synchronous and asynchronous code in Node.js?

Synchronous code executes line by line and blocks the execution until the current operation completes.
For example, a heavy calculation or a blocking function will prevent the next line of code from running.

Asynchronous code, on the other hand, allows long-running operations such as database calls, file reads, or API requests to execute in the background.
Node.js does not wait for these operations to finish and continues executing other code.

Once the asynchronous operation is completed, its result is handled using callbacks, promises, or async/await.

This is why Node.js relies heavily on asynchronous code to achieve high performance and scalability.

## Q7. What is npm? What is the role of package.json?

npm stands for Node Package Manager.
It is used to install, manage, and share JavaScript packages and also provides access to a global package registry containing thousands of open-source Node.js modules.

The `package.json` file is the core configuration file of a Node.js project.
It contains metadata such as the project name, version, scripts, and a list of dependencies required for the application.

It also defines scripts, which are used to run commands like starting the application, running tests, or building the project.

Dependencies are categorized into:
- dependencies – packages required at runtime for the application to function
- devDependencies – packages used only during development, such as testing tools, linters, or build utilities

## Q8. What is package-lock.json and why is it important?

`package-lock.json`  is an automatically generated file that records the exact versions of all installed dependencies, including nested dependencies.

While `package.json` defines the dependency version ranges, `package-lock.json` locks the exact dependency tree that was installed.

This ensures that the same versions of packages are installed across different environments such as development, testing, and production.

It improves consistency, prevents unexpected bugs caused by version changes, and also speeds up the installation process.

## Q9. What are global objects in Node.js? Name a few.

Global objects are objects that are available everywhere in a Node.js application

👉 You do NOT need to import or require them.

They are similar to:
- `window` object in the browser (but Node.js does NOT have window)

- ## Common Global Objects in Node.js (Very Important)

Here are the most commonly expected ones in interviews:

Global Object	Purpose
- global	-- The global namespace object
- process	-- Provides information about the current Node.js process
- console	-- Used for logging
- setTimeout()	-- Executes code after a delay
- setInterval()	-- Executes code repeatedly
- __dirname	-- Current directory path
- __filename	-- Current file path

  - ## Simple Interview-Ready Answer (USE THIS)

Global objects in Node.js are objects that are available throughout the application without importing them.

Some commonly used global objects are process, console, setTimeout, __dirname, and __filename.

They provide access to system-level information, timing functions, and execution context.

## Q10. How does Node.js handle multiple requests at the same time?

Node.js handles multiple requests concurrently using its event-driven, non-blocking I/O model.

When a request involves an I/O operation such as a database call, file read, or network request, Node.js delegates the task to the system or libuv thread pool.

The main JavaScript thread does not wait for the operation to complete. Instead, it continues handling other incoming requests.

Once the asynchronous operation finishes, its callback or promise resolution is placed into the event loop queue and executed when the call stack is free.

This allows Node.js to efficiently handle thousands of concurrent requests using a single thread.
