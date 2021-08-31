# Designing Applications

## Checklist

- [ ] **Choose an architecture wisely**
    - Monoliths (focus on maintainability...)
    - Microservices (focus on distribution, decoupling, fault tolerance...): [Designing scalable backend infrastructures from scratch](https://medium.com/@helloansh/designing-scalable-backend-infrastructures-from-scratch-af80f5767ccc), [.NET Microservices Sample Reference Application](https://github.com/dotnet-architecture/eShopOnContainers)
- [ ] **Choose an approach for development / architecture pattern**
    - Test/Domain/Data/Event Driven Development
    - CQRS / Event Sourcing Patterns
    - [Implementation C# Design Patterns (GoF)](https://www.dofactory.com/net/design-patterns)
- [ ] **Choose an adapted type of services**
    - API, background services, scheduled tasks
- [ ] **Choose an adapted technology**
    - Depends on the environment
    - eg. AWS Lambda for short running tasks, AWS Glue for ETL, ECS Service for continuous service...
    - Learn about the technology: try to implement it yourselves so you may understand what sort of problems a tech try to resolve, trade-off and best way to utilize the tech. 
- [ ] **Choose adequate libraries**
    - Retries (eg. Polly)
- [ ] **Choose a testing strategy**
    - [XUnit Test Patterns](http://xunitpatterns.com/)
- [ ] [Choose a strategy to share code between services](#codeshare)
- [ ] [Define an error handling strategy](#errors)
- [ ] [Define Service Layer](#sl)
- [ ] [Define Data Access Layer](#dal)
- [ ] [Define Performance Plan](#performance)
- [ ] Define Monitoring Strategy
- [ ] [Define Authentication & Authorization Mechanism](#auth)
- [ ] [Determine & Challenge Security Aspects](#sec)
- [ ] Define Auditing Strategy
    - audit changes, security aspect, regulatory considerations..

## Define Performance Plan <a name="performance"/>

1. Identifying what quantifiable metric you care about – be specific:
    - Average/hour, Peak…
    - Eg. Measure memory could be the private working set, .NET heap size... 
2. Identifying the hot path of your application / major operations
    - Do not prematurely optimise.
    - You won't have time to optimise everything.
    - Target inefficient portions with largest benefits
3. Comes up with quantifiable goals adapted to your application
    - Instead of "The user interface should be responsive” say “No operation may block the I/O thread for more than 20ms".
    - Instead of "Memory should be less than 1GB” say “Working set memory usage should never exceed 1GB during peak load of 100 queries/s"
4. Plan Capacity: Workload, CPU Usage, Memory Usage, Bandwidth, Internal Sync
    - Going to depend on the hardware / OS 
5. Challenge the outcomes with your goals
6. Measure: believe only in figures
    - Benchmarking

Mindset:
* Thinking about performance early gives a chance to influence early decisions (such as data representation)
* Better bragging about performance gains when you have data to back you up

Layers of optimisation:
*	Architecture / design
*	Algorithms (O Notations)
*	Way to APIs of Language Framework & Libraries
*	Generate code from Language Runtimes
*	Final Assembly code

Caching Strategy for reads:
* Dramatically improve performance and scalability by eliminating unnecessary requests to external data sources
* In-memory cache is stored in the memory of an individual web server. For apps hosted in server farms or on cloud hosting should use a distributed cache.
* Distributed Cache: Avoid cache consistency problems; Cached data survives instance restarts and deployments

## Define Service Layer <a name="sl"/>

Background services: 
* Do you want a window service, a scheduled task or a different mechanism? Keep the business logic out of the "schedule logic" so if it changes, the "presentation" layer can be adapted to work on any of these without changing the behavior. Note that the strategy of scheduled, error managements… are different depending on the technology too.
* How frequently the task should run? Do we have a risk of concurrent threads? 
    - Will the task run all items without interruption?
    - If no, do you want to get the list of available items and run all of them or do you want to split the number of item managed per run?
    - At what point should we commit the transaction? Do we have a risk of manipulating uncommitted data? Do we have to refresh manually the data before changing it?
* Performance (usage of stored procedures) vs Maintainability (c# coding): find the right balance between C#/T-SQL

## Define Data Access Layer <a name="dal"/>

[Define a data model](https://github.com/JM89/software-engineer-survival-guide/blob/main/book-notes/designing-data-intensive-applications.md#data-models)

* Do we want a database first, model first and code first strategy?
    - Is there an existing database?
    - Can it be changed?
    - Who is responsible for these changes?
* How automated is your deployment process?
* Will the database source controlled?
* Do we choose a data / domain / test driven development approach?
* Do we want to have nice CRUD on a DB or having business related functionality?
* What is the best ORM technology to fulfil the requirements of the previous questions? NHibernate / Entity Framework?
* Consider the access to the database through a stored procedure at the same time than entity access (SqlRepository and mapping SqlResultObject).
    - Long-running process in UI and in background tasks

## Define Authentication & Authorization Mechanism <a name="auth"/>

Authorisation mechanism in a UI:
* If possible, use SSO for authentication (+MFA) and delegate authorisations to a third party dedicated to this (eg. Okta)
* For unavoidable extremely granular permissions: 
    - Think "AWS model": trade off between operational overhead and least priviledge principle
    - Think really soon of the strategy to show and hide functionalities to the user: hiding buttons, showing read-only fields...
    
Authentication:
* Business analysis
    - Who will log in to your system?
    - Which roles?
    - What kind of access?
* Technical analysis
    - What authentication mode is used? Advantages / drawbacks of Windows authentication, Forms, 3rd party… depending on the business context?
    - Ensure the authentication mechanism follow these basic rules? Limited number of attempts, Force a secure password, Hashing and salting passwords, Reset with more than a question, Default password are forced to be reset (sent in an email)
    - Are unauthorized pages accessible via URL (server side check – UI and WS!)?
    - Do you audit security events (login, logout, failed attempts)? (Brute force login)

## Determine & Challenge Security Aspects <a name="sec"/>

Secure applications:
* Business analysis
    - Is the system an intranet / extranet / internet application?
    - Sensitize clients to the importance of HTTPS / Security… (Even for a PoC!)
    - Will the web application be accessible from another machine in another domain?
    - Are clients aware of the risk of a long session?
    - Do client agree to be re-challenge on key features? (such as Massive deletions, eg. MFA on s3 object deletion)
* Technical analysis
    - Have we planned the implementation of HTTPS and its constraints?
    - Have we planned Cross-Origin and Anti forgery configurations? (CSRF)
    - Do we have to allow a specific behaviour for Cross-Origin handling? (CSRF)
    - Have we planned to limit large messages sent to a service? (DoS)
    - Have we planned to secure our cookies?
    - Do we have key features which would need to re-challenge the user? (such as Massive deletions, eg. MFA on s3 object deletion)
    
Sensitive data:
* Business analysis
    - What are the sensitive data in this system? non-prod/prod environment
    - Does your client serves clients himself and do they have other constraints? eg. PCI Standards..
* Technical analysis
    - How sensitive data will be encrypted and stored?
    - Which methods to use if test environments can’t contain sensitive data?
    - Does sensitive data may be accessible via an ID in the URL? (Brute force)

Untrusted data
* Do we have pure SQL Queries? (SQL Injection)
* Does our routing mechanism constraint the type of untrusted data in the URL?
* Do we encode the untrusted data (POST / GET)?

## Choose a strategy to share code between services <a name="codeshare"/>

Service Layer Strategy: Do we need Web Service or a shared library?
* Shared library: Private Nuget package
    - Use of semantic versioning
    - Define Review Strategy for changes (to keep a bit of control: if many developers, it means the package can go into berserk!)
    - Dependency Hell: eg. Your app X has two custom libraries Y and Z. Y and Z has a dependencies to AWSSDK v1. Y was upgraded AWSSDK v2. X needs v2 and if AWSSDK v2 not retro-compatible, Z now needs upgrade. Repeat the cascading effect to all projects.  
    - Private repository and retention/cleaning policies
* Web Service: deployment, security, network latency
* Sharing csproj projects between different solutions (for monolith lovers)

Framework / DLL / 3rd Party:
* Is this framework / third party / DLL secured (known vulnerabilities) and maintained/updated regularly?
* Do we keep track of components and versions?

## Define an error handling strategy <a name="error"/>

Different types of errors:
- misusage of an api: eg. user friendly error message, http status code 
- unexpected contention, throttle limits: eg. SQL Locks,... ==> measure so we can reduce them, recover from them
- race conditions: add locking strategy? rollback
- unknown exceptions
- data inconsistency warning (to avoid interrupting the service for other events)
- ...

Patterns:
* Replay strategy (built on idempotency: design systems so you can allow to replay data at a later date if you discover it was missing
* Retry strategy
* Circuit breaker 
* 2-phase commits, Sagas

REST API / WEB Service:
* Communication with consumers: Provide an email subscription for checking API unavailability
* Make available the list of past incidents for consumers

Error handling flows
* Does your error handling show stack traces in production?
* Does your log files are protected

Believe only on hard technical constraints: 
* Create Hard Constraints when needed (for instance, FK): eg. If an association table has no unique constraint, don't assume your data is unique even if the business says so. 
* Code defensively if no over choices: clear log errors/warning will help debug issues
* Take no assumptions of soft constraints will migrating data.

## Useful Links

Designing C# App:
- [C# Code Decompilation](https://sharplab.io/)

Code Release:
- [Semantic versioning](https://semver.org/)

Code Samples:
- [Advanced Pagination in ASP.NET Core WebApi](https://www.codewithmukesh.com/blog/pagination-in-aspnet-core-webapi/?utm_source=csharpdigest&utm_medium=email&utm_campaign=315)

