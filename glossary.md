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
**Context:** Used for global distribution of static assets with edge caching for improved performance.

### Amazon Comprehend
**Definition:** A natural language processing (NLP) service that uses machine learning to find insights and relationships in text.
**Context:** Used for text analysis in the content analysis pipeline.

### Amazon EC2 (Elastic Compute Cloud)
**Definition:** A web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.
**Context:** Hosts our backend services in Auto Scaling Groups for scalability and reliability.

### Amazon ElastiCache
**Definition:** A fully managed in-memory caching service supporting Redis or Memcached engines.
**Context:** Used for session storage, API response caching, and distributed locking mechanisms.

### Amazon OpenSearch Service
**Definition:** A managed service that makes it easy to deploy, operate, and scale OpenSearch clusters in the AWS Cloud.
**Context:** Provides full-text search capabilities for POCs and sophisticated filtering.

### Amazon Rekognition
**Definition:** A service that makes it easy to add image and video analysis to applications.
**Context:** Used for image analysis in the content analysis pipeline.

### Amazon S3 (Simple Storage Service)
**Definition:** An object storage service offering industry-leading scalability, data availability, security, and performance.
**Context:** Stores POC assets, videos, reports, and other media assets.

### Amazon SNS (Simple Notification Service)
**Definition:** A fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication.
**Context:** Used for pub/sub messaging between services and for alerts.

### Amazon SQS (Simple Queue Service)
**Definition:** A fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.
**Context:** Used for decoupling services and message buffering for traffic spikes.

### API Gateway
**Definition:** AWS service for creating, publishing, maintaining, monitoring, and securing APIs at any scale.
**Context:** Manages API traffic with ALB for our backend services.

### ASG (Auto Scaling Group)
**Definition:** AWS feature that ensures you have the correct number of Amazon EC2 instances available to handle the load for your application.
**Context:** Provides automated scaling of EC2 instances based on load metrics.

### AWS Elemental MediaConvert
**Definition:** A file-based video transcoding service with broadcast-grade features.
**Context:** Used for transcoding in the video generation pipeline.

### AWS IAM (Identity and Access Management)
**Definition:** A web service that helps you securely control access to AWS resources.
**Context:** Provides fine-grained access control for AWS services and resources.

### AWS KMS (Key Management Service)
**Definition:** A managed service that makes it easy for you to create and control the encryption keys used to encrypt your data.
**Context:** Manages encryption keys and ensures data security through encryption.

### AWS Lambda
**Definition:** A serverless compute service that runs your code in response to events and automatically manages the compute resources.
**Context:** Used for media processing coordination in the video generation pipeline.

### AWS Shield
**Definition:** A managed Distributed Denial of Service (DDoS) protection service that safeguards applications running on AWS.
**Context:** Integrated with CloudFront for DDoS protection.

### AWS Step Functions
**Definition:** A serverless function orchestrator that makes it easy to sequence AWS Lambda functions and multiple AWS services into business-critical applications.
**Context:** Used for workflow orchestration in the video generation pipeline.

### AWS WAF (Web Application Firewall)
**Definition:** A web application firewall that helps protect your web applications from common web exploits.
**Context:** Integrated with CloudFront for application layer protection.

## B

### BLoC (Business Logic Component) Pattern
**Definition:** A design pattern for Flutter that helps separate business logic from the presentation layer.
**Context:** Used for state management in the Flutter mobile apps.

## C

### CDN (Content Delivery Network)
**Definition:** A geographically distributed network of proxy servers and their data centers to provide high availability and performance by distributing the service spatially relative to end-users.
**Context:** CloudFront serves as our CDN for static assets.

### CI/CD (Continuous Integration/Continuous Deployment)
**Definition:** A method to frequently deliver apps to customers by introducing automation into the stages of app development.
**Context:** Implemented with AWS CodePipeline and GitHub Actions for automated testing and deployment.

### CloudWatch
**Definition:** AWS monitoring and observability service providing data and actionable insights for AWS, hybrid, and on-premises applications and infrastructure resources.
**Context:** Used for metrics, logs, and monitoring in our system.

### CORS (Cross-Origin Resource Sharing)
**Definition:** A mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served.
**Context:** Configured in S3 to restrict access to approved domains.

### CSP (Content Security Policy)
**Definition:** A computer security standard introduced to prevent cross-site scripting (XSS), clickjacking and other code injection attacks.
**Context:** Implemented as part of application security practices.

## D

### D3.js
**Definition:** A JavaScript library for producing dynamic, interactive data visualizations in web browsers.
**Context:** Used with Chart.js for analytics dashboards in the web application.

### Docker
**Definition:** A platform that uses OS-level virtualization to deliver software in packages called containers.
**Context:** Used for service isolation and sandbox execution for code in Dojo feature.

### DDoS (Distributed Denial of Service)
**Definition:** A malicious attempt to disrupt normal traffic of a targeted server by overwhelming it with a flood of internet traffic.
**Context:** Protection provided by AWS Shield integrated with CloudFront.

## E

### ECS (Elastic Container Service)
**Definition:** A highly scalable, fast container management service that makes it easy to run, stop, and manage Docker containers on a cluster.
**Context:** Used for container management with EC2 launch type.

## F

### FFmpeg
**Definition:** A free and open-source software project consisting of a suite of libraries and programs for handling video, audio, and other multimedia files and streams.
**Context:** Used for video encoding and composition in the content generation service.

### Flutter
**Definition:** An open-source UI software development kit created by Google used to develop applications for Android, iOS, Linux, Mac, Windows, and the web from a single codebase.
**Context:** Used as the framework for mobile applications.

### Flyway
**Definition:** An open-source database migration tool that strongly favors simplicity and convention over configuration.
**Context:** Used for database migration in PostgreSQL.

## G

### GitHub Actions
**Definition:** A CI/CD platform that allows you to automate your build, test, and deployment pipeline directly from GitHub.
**Context:** Used with AWS CodePipeline for automated testing and deployment.

### Grafana
**Definition:** An open-source analytics and interactive visualization web application that provides charts, graphs, and alerts for the web.
**Context:** Used for visualization dashboards in monitoring.

### GraalVM
**Definition:** A high-performance JDK distribution designed to accelerate the execution of applications written in Java and other JVM languages.
**Context:** Used for Polyglot support in the Dojo service for multi-language code execution.

## H

### Hibernate
**Definition:** An object-relational mapping tool for Java that provides a framework for mapping an object-oriented domain model to a relational database.
**Context:** Used with JPA for entity management in the backend.

### HikariCP
**Definition:** A solid, high-performance, JDBC connection pool.
**Context:** Used for connection pooling with PostgreSQL.

### Hive
**Definition:** A lightweight and blazing fast key-value database written in pure Dart for Flutter applications.
**Context:** Used for lightweight key-value storage in mobile applications.

## I

### ImageMagick
**Definition:** A free and open-source software suite for displaying, converting, and editing raster image and vector image files.
**Context:** Used for thumbnail creation in the content generation service.

### IoC (Inversion of Control)
**Definition:** A design principle in which custom-written portions of a computer program receive the flow of control from a generic framework.
**Context:** Implemented through Spring's Dependency Injection.

## J

### Jackson
**Definition:** A suite of data-processing tools for Java, including the flagship JSON parsing and generation library.
**Context:** Used for JSON serialization in backend services.

### Java
**Definition:** A class-based, object-oriented programming language designed to have as few implementation dependencies as possible.
**Context:** Java 21 (LTS) is used as the primary backend programming language.

### JGit
**Definition:** A pure Java implementation of the Git version control system.
**Context:** Used for Git operations in the POC Management Service.

### jjwt
**Definition:** A Java library providing end-to-end JWT creation and verification.
**Context:** Used for JWT generation and validation in the Authentication Service.

### JPA (Java Persistence API)
**Definition:** A Java application programming interface specification that describes the management of relational data in applications using Java Platform.
**Context:** Used with Hibernate for entity management.

### JWT (JSON Web Token)
**Definition:** A compact, URL-safe means of representing claims to be transferred between two parties.
**Context:** Used for secure authentication in the system.

## M

### Material-UI (MUI)
**Definition:** A popular React UI framework implementing Google's Material Design.
**Context:** Used as the UI component library for the web application.

### Monaco Editor
**Definition:** The code editor that powers VS Code, a good choice for a code editor in the browser.
**Context:** Used for the code editor component in the Dojo feature.

## N

### NACL (Network Access Control List)
**Definition:** An optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.
**Context:** Used with Security Groups for network security.

## O

### OpenAPI
**Definition:** A specification for machine-readable interface files for describing, producing, consuming, and visualizing RESTful web services.
**Context:** Used for API documentation in backend services.

### Operational Transform
**Definition:** A technology for supporting a range of collaboration functionalities in advanced collaborative software systems.
**Context:** Used for collaborative editing in the Dojo service.

### OWASP (Open Web Application Security Project)
**Definition:** An online community that produces freely available articles, methodologies, documentation, tools, and technologies in the field of web application security.
**Context:** OWASP Top 10 mitigation strategies are implemented for application security.

## P

### PagerDuty
**Definition:** A digital operations management platform that empowers teams with the right context to address critical incidents.
**Context:** Integrated with Amazon SNS for critical service alerts.

### PDF
**Definition:** Portable Document Format, a file format developed by Adobe to present documents consistently across all platforms and software.
**Context:** Used for report generation in the content generation service.

### PDFBox
**Definition:** An open-source Java tool for working with PDF documents.
**Context:** Used for PDF generation in the content generation service.

### PostgreSQL
**Definition:** A powerful, open-source object-relational database system.
**Context:** Used as the relational database engine for the system.

### Project Reactor
**Definition:** A Reactive library for building non-blocking applications on the JVM.
**Context:** Used for non-blocking operations in backend services.

### Prometheus
**Definition:** An open-source monitoring system with a dimensional data model, flexible query language, and alerting capabilities.
**Context:** Used for metric collection in the monitoring system.

## R

### React
**Definition:** A JavaScript library for building user interfaces, particularly single-page applications.
**Context:** Used as the framework for the web application.

### React Hook Form
**Definition:** A performant, flexible, and extensible forms library for React with easy-to-use validation.
**Context:** Used for form handling in the web application.

### React Router
**Definition:** A standard library for routing in React applications.
**Context:** Used for routing in the web application (v6).

### Redis
**Definition:** An in-memory data structure store, used as a database, cache, and message broker.
**Context:** Used with Amazon ElastiCache for caching, session storage, and more.

### Redux Toolkit
**Definition:** The official, opinionated, batteries-included toolset for efficient Redux development.
**Context:** Used with RTK Query for state management in the web application.

### REST (Representational State Transfer)
**Definition:** An architectural style for designing networked applications that rely on a stateless, client-server communication protocol, typically HTTP.
**Context:** Used for the API style in backend services.

### RTK Query
**Definition:** A powerful data fetching and caching tool built into Redux Toolkit.
**Context:** Used with Redux Toolkit for state management in the web application.

## S

### Security Group
**Definition:** A virtual firewall that controls inbound and outbound traffic to AWS resources.
**Context:** Used with NACLs for network security.

### Socket.IO
**Definition:** A JavaScript library for real-time web applications that enables real-time, bidirectional communication between web clients and servers.
**Context:** Used for real-time communication in the Dojo feature.

### Spring Boot
**Definition:** An extension of the Spring framework that simplifies the initial setup and development of new Spring applications.
**Context:** Used as the main framework for backend services.

### Spring Security
**Definition:** A powerful and highly customizable authentication and access-control framework for Spring applications.
**Context:** Used for role-based access control in the Authentication Service.

### Spring WebSocket
**Definition:** A framework that provides WebSocket support for Spring applications.
**Context:** Used with STOMP for WebSocket implementation in the Dojo feature.

### SQLite
**Definition:** A C-language library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine.
**Context:** Used for structured local data in mobile applications.

### SSE-S3 (Server-Side Encryption with Amazon S3-Managed Keys)
**Definition:** An encryption option where Amazon S3 manages the encryption keys.
**Context:** Used for encrypting user-generated content in S3.

### STOMP (Simple Text Oriented Messaging Protocol)
**Definition:** A simple text-based messaging protocol, designed for working with message-oriented middleware.
**Context:** Used with Spring WebSocket for the Dojo feature.

### Swagger UI
**Definition:** A collection of HTML, JavaScript, and CSS assets that dynamically generate documentation from an OpenAPI specification.
**Context:** Used for API documentation with API Gateway.

## T

### Terraform
**Definition:** An open-source infrastructure as code software tool created by HashiCorp.
**Context:** Used for declarative infrastructure definition and environment consistency.

### Thymeleaf
**Definition:** A modern server-side Java template engine for both web and standalone environments.
**Context:** Used as the template engine for report generation.

## V

### Virtual DOM
**Definition:** A programming concept where an ideal, or "virtual", representation of a UI is kept in memory and synced with the "real" DOM by a library such as React.
**Context:** Provided by React for efficient rendering in the web application.

### Vite
**Definition:** A modern frontend build tool that significantly improves the frontend development experience.
**Context:** Used as the build tool for the web application.

### VPC (Virtual Private Cloud)
**Definition:** A logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define.
**Context:** Used with private subnets for network security.

## W

### WebSocket
**Definition:** A computer communications protocol, providing full-duplex communication channels over a single TCP connection.
**Context:** Used for real-time, bi-directional communication in the Dojo feature.

## X

### X-Ray
**Definition:** An AWS service that helps developers analyze and debug production, distributed applications.
**Context:** Used for distributed tracing in monitoring.

## Y

### Yup
**Definition:** A JavaScript schema builder for value parsing and validation.
**Context:** Used with React Hook Form for validation in the web application.