# Routing

Routing refers to the process of determining how incoming HTTP requests should be handled and which controller action should be invoked to generate a response.

Routing is a fundamental part of web application frameworks that follow the MVC pattern, and it plays a crucial role in handling client requests and directing them to the appropriate controller for processing.

A **router** is a component responsible for handling URL routing and directing incoming HTTP requests to the appropriate controller and action method in an MVC-based web application.

Mapping URLs directly to scripts, also known as a "script-centric" or "file-centric" approach is generally considered a bad idea for several reasons:

- **Poor Separation of Concerns**

Directly mapping URLs to scripts often leads to mixing business logic and presentation logic within the same script or file. This can make the codebase less maintainable and harder to understand because it lacks a clear separation of concerns.  

- **Limited Reusability**

When URLs are tightly coupled to specific scripts, it becomes challenging to reuse code components across different parts of the application. This can result in code duplication and increased development time.  

**Scalability Issues**

As an application grows, maintaining a direct mapping of URLs to scripts becomes unwieldy. It can lead to many individual script files, making it difficult to manage and organize the codebase. 

**Security Risks** 

In a script-centric approach, the scripts are directly accessible via URLs. This can expose sensitive code and data to potential attackers who may attempt to exploit vulnerabilities in your application.

Instead, **configure your web server to redirect all URLs to the same index.php** file that uses the router as a frontend to MVC. Instead of mapping URLs to individual scripts, URLs will map to controller's actions.

**.htaccess** files are frequently used to implement URL rewriting rules. This can be used to create user-friendly URLs, remove file extensions, and control how URLs map to server resources.

- **Consistency and Conventions**

Adopting consistent naming conventions and URL structures can make the application more intuitive and easier to navigate.

- **Security Measures**

Implement additional security measures in routing to prevent unauthorized access and potential attacks.

- **Performance Optimization**

Efficient routing can also contribute to better performance, as it ensures quick and accurate request handling.
