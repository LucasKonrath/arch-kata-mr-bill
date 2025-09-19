# Mr. Bill Architecture - Technical Glossary

This glossary provides definitions for the technical terms used in the Mr. Bill architecture document. Use this as a reference to prepare for presentations and discussions about the system architecture.

## A

### ACID
**Definition:** An acronym for Atomicity, Consistency, Isolation, and Durability. These properties guarantee database transactions are processed reliably.
**Context:** PostgreSQL provides ACID compliance for reliable data transactions in our system.

### ALB (Application Load Balancer)
**Definition:** An AWS service that distributes incoming application traffic across multiple targets, such as EC2 instances, in multiple Availability Zones.
**Context:** Used with API Gateway to manage API traffic and ensure high availability.

### Amazon CloudFront
**Definition:** A content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds.
**Context:** Used for global distribution of static assets with edge caching for improved performance. Integrates with AWS Shield and WAF for DDoS protection and application security.

### Amazon Comprehend
**Definition:** A natural language processing (NLP) service that uses machine learning to find insights and relationships in text.
**Context:** Used for text analysis in the content analysis pipeline.

### Amazon EC2 (Elastic Compute Cloud)
**Definition:** A web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.
**Context:** Hosts our backend services in Auto Scaling Groups for scalability and reliability. We use EC2 rather than serverless solutions to avoid cold starts and have predictable performance.

### Amazon ElastiCache
**Definition:** A fully managed in-memory caching service supporting Redis or Memcached engines.
**Context:** Used for session storage, API response caching, rate limiting implementation, and distributed locking mechanisms. Improves application performance by reducing database load.

### Amazon OpenSearch Service
**Definition:** A managed service that makes it easy to deploy, operate, and scale OpenSearch clusters in the AWS Cloud.
**Context:** Provides full-text search capabilities for POCs and sophisticated filtering. Offers advanced faceting and aggregation capabilities beyond what's possible with traditional SQL.

### Amazon Rekognition
**Definition:** A service that makes it easy to add image and video analysis to applications.
**Context:** Used for image analysis in the content analysis pipeline.

### Amazon S3 (Simple Storage Service)
**Definition:** An object storage service offering industry-leading scalability, data availability, security, and performance.
**Context:** Stores POC assets, videos, reports, and other media assets. Configured with appropriate access controls and lifecycle policies (30 days hot storage, 1 year in cold storage).

### Amazon SNS (Simple Notification Service)
**Definition:** A fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication.
**Context:** Used for pub/sub messaging between services, fan-out event distribution, delivery status tracking, and for alerting. Integrated with PagerDuty for critical alerts.

### Amazon SQS (Simple Queue Service)
**Definition:** A fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.
**Context:** Used for decoupling services, message buffering for traffic spikes, and implementing dead letter queues for error handling.

### Anti-corruption Layer
**Definition:** A design pattern that creates an isolating layer to translate between different models, particularly when integrating with legacy systems or external services.
**Context:** Used to prevent external system concepts from leaking into our core domain models.

### API Gateway
**Definition:** AWS service for creating, publishing, maintaining, monitoring, and securing APIs at any scale.
**Context:** Manages API traffic with ALB for our backend services. Provides request throttling, quotas, and API documentation via Swagger UI.

### API Gateway Pattern
**Definition:** An architectural pattern where a single entry point is created for a group of microservices, handling cross-cutting concerns like authentication, monitoring, and rate limiting.
**Context:** Implemented using AWS API Gateway to provide a unified entry point for our microservices architecture.

### ASG (Auto Scaling Group)
**Definition:** AWS feature that ensures you have the correct number of Amazon EC2 instances available to handle the load for your application.
**Context:** Provides automated scaling of EC2 instances based on load metrics, ensuring cost-efficient resource utilization while maintaining performance.

### AWS Elemental MediaConvert
**Definition:** A file-based video transcoding service with broadcast-grade features.
**Context:** Used for transcoding in the video generation pipeline. Handles various input formats and outputs optimized streams for different devices and bandwidths.

### AWS IAM (Identity and Access Management)
**Definition:** A web service that helps you securely control access to AWS resources.
**Context:** Provides fine-grained access control for AWS services and resources. Implements the principle of least privilege with service roles and policies.

### AWS KMS (Key Management Service)
**Definition:** A managed service that makes it easy for you to create and control the encryption keys used to encrypt your data.
**Context:** Manages encryption keys and ensures data security through encryption at rest and in transit. Supports secure key rotation policies.

### AWS Lambda
**Definition:** A serverless compute service that runs your code in response to events and automatically manages the compute resources.
**Context:** Used for media processing coordination in the video generation pipeline. While not used for main services (to avoid cold starts), it's suitable for asynchronous processing tasks.

### AWS Shield
**Definition:** A managed Distributed Denial of Service (DDoS) protection service that safeguards applications running on AWS.
**Context:** Integrated with CloudFront for DDoS protection at both network and transport layers (Layer 3 and 4).

### AWS Step Functions
**Definition:** A serverless function orchestrator that makes it easy to sequence AWS Lambda functions and multiple AWS services into business-critical applications.
**Context:** Used for workflow orchestration in the video generation pipeline. Provides visual workflow management and error handling for complex processes.

### AWS WAF (Web Application Firewall)
**Definition:** A web application firewall that helps protect your web applications from common web exploits.
**Context:** Integrated with CloudFront for application layer protection. Configured with rules to prevent SQL injection, XSS, and other OWASP Top 10 vulnerabilities.

## B

### Backend for Frontend (BFF)
**Definition:** An architectural pattern where separate backend services are created specifically for different frontend clients.
**Context:** Implemented to optimize API responses for both mobile and web clients, reducing payload sizes and unnecessary processing.

### Blue/Green Deployment
**Definition:** A deployment strategy where two identical production environments exist, with only one serving production traffic at a time.
**Context:** Used to minimize downtime and risk by switching traffic between two identical environments after the new version is verified.

### BLoC (Business Logic Component) Pattern
**Definition:** A design pattern for Flutter that helps separate business logic from the presentation layer.
**Context:** Used for state management in the Flutter mobile apps.

### Bulkhead Pattern
**Definition:** A failure isolation pattern that prevents cascading failures by partitioning service instances into different pools.
**Context:** Implemented to isolate critical services from non-critical ones, ensuring core functionality remains available even when auxiliary services fail.

## C

### CAP Theorem
**Definition:** A concept that states a distributed system cannot simultaneously provide all three guarantees: Consistency, Availability, and Partition tolerance.
**Context:** Used to inform database design decisions, with our system generally favoring consistency and partition tolerance for data integrity.

### Canary Releases
**Definition:** A technique to reduce the risk of introducing a new software version by slowly rolling out the change to a small subset of users before rolling it out to the entire infrastructure.
**Context:** Used in conjunction with feature flags to gradually introduce new features to users.

### CDN (Content Delivery Network)
**Definition:** A geographically distributed network of proxy servers and their data centers to provide high availability and performance by distributing the service spatially relative to end-users.
**Context:** CloudFront serves as our CDN for static assets, reducing latency and improving user experience globally.

### CI/CD (Continuous Integration/Continuous Deployment)
**Definition:** A method to frequently deliver apps to customers by introducing automation into the stages of app development.
**Context:** Implemented with AWS CodePipeline and GitHub Actions for automated testing and deployment. Provides environment promotion workflows and infrastructure validation.

### Circuit Breaker Pattern
**Definition:** A design pattern that prevents cascading failures by detecting failures and encapsulating logic for preventing a failure from constantly recurring.
**Context:** Implemented in inter-service communication to handle graceful degradation during partial system failures.

### CloudWatch
**Definition:** AWS monitoring and observability service providing data and actionable insights for AWS, hybrid, and on-premises applications and infrastructure resources.
**Context:** Used for metrics, logs, and monitoring in our system. Configured with structured JSON logging format and log-based alerting.

### Command Query Responsibility Segregation (CQRS)
**Definition:** An architectural pattern that separates read and write operations to different models.
**Context:** Implemented in the POC search functionality, where complex queries use OpenSearch while writes go to PostgreSQL.

### Connection Pooling
**Definition:** A technique used to maintain a cache of database connections for reuse when future requests to the database are required.
**Context:** Implemented using HikariCP for efficient database connections management, improving performance and resource utilization.

### CORS (Cross-Origin Resource Sharing)
**Definition:** A mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served.
**Context:** Configured in S3 and API Gateway to restrict access to approved domains.

### CSP (Content Security Policy)
**Definition:** A computer security standard introduced to prevent cross-site scripting (XSS), clickjacking and other code injection attacks.
**Context:** Implemented as part of application security practices to restrict which resources can be loaded and executed.

## D

### D3.js
**Definition:** A JavaScript library for producing dynamic, interactive data visualizations in web browsers.
**Context:** Used with Chart.js for analytics dashboards in the web application.

### Data Partitioning
**Definition:** A technique to divide a database into distinct independent parts to improve manageability, performance, and availability.
**Context:** Implemented in our multi-tenant system with data separation by tenant ID for security and performance.

### Docker
**Definition:** A platform that uses OS-level virtualization to deliver software in packages called containers.
**Context:** Used for service isolation and sandbox execution for code in Dojo feature. Provides consistent environments across development and production.

### DDoS (Distributed Denial of Service)
**Definition:** A malicious attempt to disrupt normal traffic of a targeted server by overwhelming it with a flood of internet traffic.
**Context:** Protection provided by AWS Shield integrated with CloudFront, with additional layer 7 protection from AWS WAF.

### Domain-Driven Design (DDD)
**Definition:** An approach to software development that centers the development on programming a domain model with a rich understanding of the processes and rules of the domain.
**Context:** Applied to structure our core services around well-defined business domains like POC management, Dojos, and content generation.

## E

### ECS (Elastic Container Service)
**Definition:** A highly scalable, fast container management service that makes it easy to run, stop, and manage Docker containers on a cluster.
**Context:** Used for container management with EC2 launch type. Provides task definitions for resource allocation and service auto-scaling.

### Event-Driven Architecture
**Definition:** A software architecture paradigm promoting the production, detection, consumption of, and reaction to events.
**Context:** Implemented using SNS/SQS for asynchronous communication between services, improving system resilience and responsiveness.

### Exponential Backoff
**Definition:** A strategy where retry attempts are made with increasing time intervals between consecutive retries.
**Context:** Implemented in service communication to handle transient failures gracefully without overwhelming the target service.

## F

### Feature Flags
**Definition:** A technique that turns certain functionality on and off during runtime, without deploying new code.
**Context:** Used to enable gradual feature rollouts, A/B testing, and quick feature disabling in case of issues.

### FFmpeg
**Definition:** A free and open-source software project consisting of a suite of libraries and programs for handling video, audio, and other multimedia files and streams.
**Context:** Used for video encoding and composition in the content generation service.

### Flutter
**Definition:** An open-source UI software development kit created by Google used to develop applications for Android, iOS, Linux, Mac, Windows, and the web from a single codebase.
**Context:** Used as the framework for mobile applications, chosen for its cross-platform capabilities while maintaining near-native performance.

### Flyway
**Definition:** An open-source database migration tool that strongly favors simplicity and convention over configuration.
**Context:** Used for database migration in PostgreSQL to manage schema changes and versioning.

## G

### GitHub Actions
**Definition:** A CI/CD platform that allows you to automate your build, test, and deployment pipeline directly from GitHub.
**Context:** Used with AWS CodePipeline for automated testing and deployment, providing environment promotion workflows.

### Grafana
**Definition:** An open-source analytics and interactive visualization web application that provides charts, graphs, and alerts for the web.
**Context:** Used for visualization dashboards in monitoring. Configured with unified metrics/logs/traces for comprehensive system visibility.

### GraalVM
**Definition:** A high-performance JDK distribution designed to accelerate the execution of applications written in Java and other JVM languages.
**Context:** Used for Polyglot support in the Dojo service for multi-language code execution in a secure sandbox environment.

## H

### Hibernate
**Definition:** An object-relational mapping tool for Java that provides a framework for mapping an object-oriented domain model to a relational database.
**Context:** Used with JPA for entity management in the backend, providing robust data access capabilities.

### HikariCP
**Definition:** A solid, high-performance, JDBC connection pool.
**Context:** Used for connection pooling with PostgreSQL, improving database access performance and resource utilization.

### Hive
**Definition:** A lightweight and blazing fast key-value database written in pure Dart for Flutter applications.
**Context:** Used for lightweight key-value storage in mobile applications for local caching and offline capabilities.

## I

### Idempotency
**Definition:** The property of certain operations whereby they can be applied multiple times without changing the result beyond the initial application.
**Context:** Implemented in API endpoints that handle financial transactions or state changes to prevent duplicate processing.

### ImageMagick
**Definition:** A free and open-source software suite for displaying, converting, and editing raster image and vector image files.
**Context:** Used for thumbnail creation in the content generation service.

### Infrastructure as Code (IaC)
**Definition:** The process of managing and provisioning computing infrastructure through machine-readable definition files rather than manual processes.
**Context:** Implemented using Terraform for declarative infrastructure definition, ensuring environment consistency and modular component design.

### IoC (Inversion of Control)
**Definition:** A design principle in which custom-written portions of a computer program receive the flow of control from a generic framework.
**Context:** Implemented through Spring's Dependency Injection to improve modularity and testability.

## J

### Jackson
**Definition:** A suite of data-processing tools for Java, including the flagship JSON parsing and generation library.
**Context:** Used for JSON serialization in backend services, providing efficient data transformation between Java objects and JSON.

### Java
**Definition:** A class-based, object-oriented programming language designed to have as few implementation dependencies as possible.
**Context:** Java 21 (LTS) is used as the primary backend programming language for its robustness, performance, and enterprise features.

### JGit
**Definition:** A pure Java implementation of the Git version control system.
**Context:** Used for Git operations in the POC Management Service to interact with source code repositories.

### jjwt
**Definition:** A Java library providing end-to-end JWT creation and verification.
**Context:** Used for JWT generation and validation in the Authentication Service to implement secure, stateless authentication.

### JPA (Java Persistence API)
**Definition:** A Java application programming interface specification that describes the management of relational data in applications using Java Platform.
**Context:** Used with Hibernate for entity management and object-relational mapping.

### JWT (JSON Web Token)
**Definition:** A compact, URL-safe means of representing claims to be transferred between two parties.
**Context:** Used for secure authentication in the system, enabling stateless authentication across services.

## M

### Material-UI (MUI)
**Definition:** A popular React UI framework implementing Google's Material Design.
**Context:** Used as the UI component library for the web application, providing consistent and responsive user interface elements.

### Microservices Architecture
**Definition:** An architectural style that structures an application as a collection of small, loosely coupled services.
**Context:** Our system is built using microservices to ensure low coupling, independent scaling, and technology flexibility across different domains.

### Monaco Editor
**Definition:** The code editor that powers VS Code, a good choice for a code editor in the browser.
**Context:** Used for the code editor component in the Dojo feature to provide a rich coding experience in the browser.

### Multi-tenancy
**Definition:** A software architecture where a single instance of software serves multiple customers (tenants) with proper isolation.
**Context:** Our system implements multi-tenancy at the database level with tenant isolation through row-level security and separate data partitions.

## N

### NACL (Network Access Control List)
**Definition:** An optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.
**Context:** Used with Security Groups for network security as a stateless firewall at the subnet level.

## O

### OpenAPI
**Definition:** A specification for machine-readable interface files for describing, producing, consuming, and visualizing RESTful web services.
**Context:** Used for API documentation in backend services, generating interactive Swagger UI documentation.

### Operational Transform
**Definition:** A technology for supporting a range of collaboration functionalities in advanced collaborative software systems.
**Context:** Used for collaborative editing in the Dojo service to manage concurrent edits from multiple users.

### OWASP (Open Web Application Security Project)
**Definition:** An online community that produces freely available articles, methodologies, documentation, tools, and technologies in the field of web application security.
**Context:** OWASP Top 10 mitigation strategies are implemented for application security, with regular security testing and vulnerability scanning.

## P

### PagerDuty
**Definition:** A digital operations management platform that empowers teams with the right context to address critical incidents.
**Context:** Integrated with Amazon SNS for critical service alerts, implementing escalation policies and on-call rotation management.

### PDF
**Definition:** Portable Document Format, a file format developed by Adobe to present documents consistently across all platforms and software.
**Context:** Used for report generation in the content generation service, ensuring consistent document presentation across devices.

### PDFBox
**Definition:** An open-source Java tool for working with PDF documents.
**Context:** Used for PDF generation in the content generation service to create rich, formatted reports.

### PostgreSQL
**Definition:** A powerful, open-source object-relational database system.
**Context:** Used as the relational database engine for the system, providing ACID compliance, advanced query capabilities, and robust transaction support.

### Project Reactor
**Definition:** A Reactive library for building non-blocking applications on the JVM.
**Context:** Used for non-blocking operations in backend services, improving scalability and resource utilization.

### Prometheus
**Definition:** An open-source monitoring system with a dimensional data model, flexible query language, and alerting capabilities.
**Context:** Used for metric collection in the monitoring system. Integrated with AWS Managed Prometheus for scalable, managed metrics storage.

## R

### Rate Limiting
**Definition:** A strategy to control the rate of requests that clients can make to an API or service within a specified time window.
**Context:** Implemented at the API Gateway and application levels to prevent abuse and ensure fair resource allocation.

### Read Replica
**Definition:** A copy of a database instance that reflects the same data as the primary instance, used to offload read operations.
**Context:** Configured for PostgreSQL to scale read capacity and improve query performance for reporting and search operations.

### React
**Definition:** A JavaScript library for building user interfaces, particularly single-page applications.
**Context:** Used as the framework for the web application. Its virtual DOM provides efficient rendering for POC search results and real-time updates.

### React Hook Form
**Definition:** A performant, flexible, and extensible forms library for React with easy-to-use validation.
**Context:** Used for form handling in the web application, reducing unnecessary re-renders and improving performance.

### React Router
**Definition:** A standard library for routing in React applications.
**Context:** Used for routing in the web application (v6), providing declarative navigation and URL management.

### Redis
**Definition:** An in-memory data structure store, used as a database, cache, and message broker.
**Context:** Used with Amazon ElastiCache for caching, session storage, and more. Provides sub-millisecond response times for high-performance operations.

### Redux Toolkit
**Definition:** The official, opinionated, batteries-included toolset for efficient Redux development.
**Context:** Used with RTK Query for state management in the web application, providing predictable state management.

### REST (Representational State Transfer)
**Definition:** An architectural style for designing networked applications that rely on a stateless, client-server communication protocol, typically HTTP.
**Context:** Used for the API style in backend services, providing a standardized approach to API design with clear resource-oriented endpoints.

### Retry Pattern
**Definition:** A resilience pattern where failed operations are automatically retried a specified number of times with appropriate backoff strategies.
**Context:** Implemented for transient failures in service communication to improve system reliability.

### RTK Query
**Definition:** A powerful data fetching and caching tool built into Redux Toolkit.
**Context:** Used with Redux Toolkit for state management in the web application, providing automatic request deduplication and caching.

## S

### Saga Pattern
**Definition:** A pattern for managing failures in distributed transactions by coordinating a series of local transactions using messages.
**Context:** Implemented for operations that span multiple services, like content generation that requires coordination across multiple steps.

### Security Group
**Definition:** A virtual firewall that controls inbound and outbound traffic to AWS resources.
**Context:** Used with NACLs for network security, acting as a stateful firewall at the instance level.

### Service Discovery
**Definition:** The automatic detection of devices and services on a network.
**Context:** Implemented using AWS Cloud Map to allow services to locate and communicate with each other dynamically.

### Sharding
**Definition:** A database architecture pattern related to horizontal partitioning, splitting data across multiple databases to improve performance and scalability.
**Context:** Implemented for high-volume data like dojo code snapshots and chat messages to ensure consistent performance.

### Socket.IO
**Definition:** A JavaScript library for real-time web applications that enables real-time, bidirectional communication between web clients and servers.
**Context:** Used for real-time communication in the Dojo feature, providing fallback mechanisms when WebSockets aren't available.

### Spring Boot
**Definition:** An extension of the Spring framework that simplifies the initial setup and development of new Spring applications.
**Context:** Used as the main framework for backend services, providing robust enterprise features, excellent documentation, and integration capabilities.

### Spring Security
**Definition:** A powerful and highly customizable authentication and access-control framework for Spring applications.
**Context:** Used for role-based access control in the Authentication Service, implementing multi-layer security architecture.

### Spring WebSocket
**Definition:** A framework that provides WebSocket support for Spring applications.
**Context:** Used with STOMP for WebSocket implementation in the Dojo feature for real-time collaborative editing.

### SQLite
**Definition:** A C-language library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine.
**Context:** Used for structured local data in mobile applications, providing offline capabilities and local persistence.

### SSE-S3 (Server-Side Encryption with Amazon S3-Managed Keys)
**Definition:** An encryption option where Amazon S3 manages the encryption keys.
**Context:** Used for encrypting user-generated content in S3, ensuring data confidentiality at rest.

### STOMP (Simple Text Oriented Messaging Protocol)
**Definition:** A simple text-based messaging protocol, designed for working with message-oriented middleware.
**Context:** Used with Spring WebSocket for the Dojo feature to structure real-time message exchange.

### Swagger UI
**Definition:** A collection of HTML, JavaScript, and CSS assets that dynamically generate documentation from an OpenAPI specification.
**Context:** Used for API documentation with API Gateway, providing interactive API exploration capabilities.

## T

### Terraform
**Definition:** An open-source infrastructure as code software tool created by HashiCorp.
**Context:** Used for declarative infrastructure definition and environment consistency, ensuring reproducible deployments.

### Thymeleaf
**Definition:** A modern server-side Java template engine for both web and standalone environments.
**Context:** Used as the template engine for report generation, creating well-formatted PDF and HTML reports.

### Timeout Pattern
**Definition:** A resilience design pattern that limits the amount of time waiting for an operation to complete.
**Context:** Implemented in all service-to-service communications to prevent blocked threads and cascading failures.

## V

### Virtual DOM
**Definition:** A programming concept where an ideal, or "virtual", representation of a UI is kept in memory and synced with the "real" DOM by a library such as React.
**Context:** Provided by React for efficient rendering in the web application, particularly important for the real-time updates in Dojo sessions.

### Vite
**Definition:** A modern frontend build tool that significantly improves the frontend development experience.
**Context:** Used as the build tool for the web application, providing fast hot module replacement and efficient production builds.

### VPC (Virtual Private Cloud)
**Definition:** A logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define.
**Context:** Used with private subnets for network security. Services are placed in private subnets with controlled access through VPC endpoints.

## W

### WebSocket
**Definition:** A computer communications protocol, providing full-duplex communication channels over a single TCP connection.
**Context:** Used for real-time, bi-directional communication in the Dojo feature to enable collaborative coding and instant updates.

## X

### X-Ray
**Definition:** An AWS service that helps developers analyze and debug production, distributed applications.
**Context:** Used for distributed tracing in monitoring, integrated with CloudWatch ServiceLens to provide end-to-end transaction visibility.

## Y

### Yup
**Definition:** A JavaScript schema builder for value parsing and validation.
**Context:** Used with React Hook Form for validation in the web application, providing robust data validation on the client side.

## Z

### Zero Trust Security Model
**Definition:** A security concept centered on the belief that organizations should not automatically trust anything inside or outside its perimeters.
**Context:** Implemented through strict authentication, authorization, and encryption at all service boundaries, regardless of network location.