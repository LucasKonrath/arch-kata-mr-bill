# 🧬 Template

This is a template created by Diego Pacheco which the goal to better describe a tought process which is called architecture. This should be used to learn software architecture and to pratice with use cases.

## 🏛️ Structure

### 1. 🎯 Problem Statement and Context

````
Mr Bill wants a system to keep track of his favorite POCs. You need to build a mobile app where Mr Bill can register all his pocs, and he also needs to be able to search POCs by: name, language, by tags. This system should be multi-tenant, because Mr Bill will sell the system to a bunch of people in Brazil. Such system must also have the ability to generate reports and generate a video with all the pocs the user did in 1 year.

Such system must be secure and have proper login and be able to support realtime dojos using the Mr Bill platform you will build for him.
````


### 2. 🎯 Goals

1. Reliable solution with a balance between high availability and cost efficiency.
2. Robust security
3. Follow good practices of code
4. Modern technology stack
5. Designed for anti-fragility

### 3. 🎯 Non-Goals

1. Usage of Lambdas
2. A monolith or distributed monoliths
3. Single AZ solutions
4. No Ionic
5. We need a single language for mobile, needs to be native
6. No MongoDB
7. Having a single Relational DB for everything
8. Clouds other than AWS

### 📐 3. Principles

1. Low coupling - stray very far away from monoliths or distributed monoliths.
2. Reliability - design a highly available and reliable system
3. Security - follow good security practices with multi-layer security

### 🏗️ 4. Overall Diagrams

<img width="921" height="683" alt="image" src="https://github.com/user-attachments/assets/536be8f9-84b3-4194-bb8c-b7a4bd0dcf4b" />


Here there will be a bunch of diagrams, to understand the solution.
```
🗂️ 4.1 Overall architecture: Show the big picture, relationship between macro components.
🗂️ 4.2 Deployment: Show the infra in a big picture. 
🗂️ 4.3 Use Cases: Make 1 macro use case diagram that list the main capability that needs to be covered. 
```
Recommended Reading: http://diego-pacheco.blogspot.com/2020/10/uml-hidden-gems.html

### 🧭 5. Trade-offs

List the tradeoffs analysis, comparing pros and cons for each major decision.
Before you need list all your major decisions, them run tradeoffs on than.
example:
Major Decisions: 
```
1. One mobile code base - should be (...)
2. Reusable capability and low latency backends should be (...)
3. Cache efficiency therefore should do (...)
```
Tradeoffs:
```
1. React Native vs (Flutter and Native)
2. Services vs Serverless
3. Redis vs Enbeded Caches
```
Each tradeoff line need to be:
```
PROS (+) 
  * Benefit: Explanation that justify why the benefit is true.
CONS (+)
  * Problem: Explanation that justify why the problem is true.
```

Major Decisions:

1. No monoliths
2. Single native language for mobile
3. Multiple DBs - not one relational DB for everything
4. Restricted to AWS

Tradeoffs:
## 1. SOA (Service Oriented Architecture) vs Monoliths

PROS: 
  -  Better isolation
  - Horizontal Scalability
  - No Single Point of Failure

CONS:
  - Higher time to market (more development time)
  - Might be unnecessary spending if the platform is not used enough


## 2. Services vs Serverless

PROS:
  - Predictable performance
  - No need to worry about cold starts

CONS:
  - More infrastructure management
  - Might be more expensive than serverless depending on the workflows

## 3. Multiple DBs vs One Relational DB

PROS:
- Specialized DBs will incur better performance
- No distributed monolith
- Loosen coupling

CONS:
- Higher cost to maintain
- Higher integration between data sources and services needed

## 4. Restrict to AWS vs Private Cloud

PROS:
- Need to worry less about maintenance
- Usage of managed services will ease development and operations

CONS:
- If many managed solutions are used you might end up with vendor lock-in
- If using pay-as-you-go cost might be a big issue

### 🌏 6. For each key major component

What is a majore component? A service, a lambda, a important ui, a generalized approach for all uis, a generazid approach for computing a workload, etc...
```
6.1 - Class Diagram              : classic uml diagram with attributes and methods
6.2 - Contract Documentation     : Operations, Inputs and Outputs
6.3 - Persistence Model          : Diagrams, Table structure, partiotioning, main queries.
6.4 - Algorithms/Data Structures : Spesific algos that need to be used, along size with spesific data structures.
```

Exemplos of other components: Batch jobs, Events, 3rd Party Integrations, Streaming, ML Models, ChatBots, etc... 

Recommended Reading: http://diego-pacheco.blogspot.com/2018/05/internal-system-design-forgotten.html

### 🖹 7. Migrations

No migrations necessary.

### 🖹 8. Testing strategy

Our multi-layered testing strategy ensures quality, reliability, and security across the Mr. Bill platform:

#### Unit Tests
- **Coverage**: Aim for >85% code coverage in all services
- **Framework**: Jest for JavaScript/TypeScript, JUnit for Java
- **Mocking**: Use mock libraries to isolate units (Mockito for Java, Jest mocks for JS/TS)
- **Run frequency**: On every commit via CI pipeline

#### Integration Tests
- **Scope**: Verify interactions between services, databases, and third-party APIs
- **Approach**: Use test containers for database integration
- **Tools**: Postman collections for API testing, Testcontainers for DB testing
- **Run frequency**: Daily in CI pipeline

#### Contract Tests
- **Purpose**: Ensure service interfaces don't break consumer expectations
- **Tools**: Pact for consumer-driven contract testing
- **Implementation**: Define consumer expectations as contracts
- **Run frequency**: On API changes and during integration tests

#### End-to-End Tests
- **Scope**: Test complete user flows across the entire system
- **Tools**: Cypress for web, Detox for mobile
- **Scenarios**: Cover critical user journeys (POC creation, search, reporting)
- **Run frequency**: Nightly and before releases

#### UI Tests
- **Scope**: Verify UI components and interactions
- **Tools**: React Testing Library for components, Storybook for visual testing
- **Visual regression**: Percy for visual comparisons
- **Accessibility**: Include a11y tests using axe-core

#### Smoke Tests
- **Purpose**: Verify core functionality after deployment
- **Scope**: Login, POC creation, search, basic reporting
- **Run frequency**: After every deployment to any environment
- **Implementation**: Automated via CI/CD pipeline

#### Stress Tests
- **Purpose**: Verify system behavior under heavy load
- **Tools**: JMeter, Gatling, Locust
- **Scenarios**: High-volume POC creation, concurrent searches, report generation
- **Metrics**: Response time, error rate, resource utilization
- **Run frequency**: Monthly and before major releases

#### Chaos Tests
- **Purpose**: Ensure system resilience during failures
- **Tools**: Chaos Monkey, AWS Fault Injection Simulator
- **Scenarios**: Database failures, service outages, network latency
- **Implementation**: Controlled experiments in staging environment
- **Run frequency**: Quarterly

#### Mutation Tests
- **Purpose**: Verify test quality by modifying code
- **Tools**: Stryker for JavaScript, PIT for Java
- **Coverage**: Focus on critical services and business logic
- **Run frequency**: Weekly in development environment

#### Fuzzing Tests
- **Purpose**: Find security vulnerabilities and edge cases
- **Tools**: AFL for API fuzzing, OWASP ZAP for security
- **Targets**: API endpoints, input validation, authentication
- **Run frequency**: Monthly and for security-sensitive changes

#### Exploratory Tests
- **Approach**: Structured exploratory testing sessions
- **Documentation**: Use session-based testing with recorded findings
- **Focus areas**: New features, complex workflows, reported issues
- **Run frequency**: Before major releases and for complex features

#### A/B Tests
- **Purpose**: Compare feature variants with real users
- **Implementation**: Feature flags via LaunchDarkly
- **Metrics**: User engagement, time spent, feature adoption
- **Analysis**: Statistical significance testing for decision making
- **Monitoring**: Real-time dashboards for experiment monitoring

#### Testing Environments
1. **Development**: Unit, integration tests
2. **QA**: All automated tests except stress and chaos
3. **Staging**: Full suite including stress and chaos tests
4. **Production**: Smoke tests, A/B tests, production monitoring

#### Test Data Management
- Anonymized production data for realistic testing
- Seed data scripts for consistent test environments
- Data cleanup processes after test execution

#### Mocking Strategy
- External APIs mocked during unit and integration testing
- Service virtualization for third-party dependencies
- Consistent mocking patterns across test suites

### 🖹 9. Observability strategy

#### Distributed Tracing

- **Technology**: AWS X-Ray integrated with OpenTelemetry
- **Implementation**:
  - Unique trace ID propagated across all microservices
  - Automatic instrumentation for Java services via X-Ray SDK
  - Manual instrumentation for critical business operations
  - Sampling strategy: 100% for errors, 5% for successful requests
- **Key Metrics**:
  - End-to-end transaction latency
  - Service-to-service communication time
  - Dependency bottlenecks identification
  - Error tracing across service boundaries
- **Correlation**: Trace IDs embedded in logs and metrics for cross-referencing

#### Log Management

- **Collection**: AWS CloudWatch Logs with Fluent Bit agents
- **Processing**: CloudWatch Logs Insights for real-time analysis
- **Long-term Storage**: S3 with lifecycle policies (30 days hot, 1 year cold)
- **Standardization**:
  - JSON structured logging format
  - Common fields: timestamp, service, traceId, spanId, severity
  - Context-specific fields for business events
- **Log Levels**:
  - ERROR: All exceptions and failures
  - WARN: Degraded service, retries, slow operations
  - INFO: Key business events, service startup/shutdown
  - DEBUG: Development-only, disabled in production
- **Sensitive Data**: PII automatically redacted before ingestion

#### APM (Application Performance Monitoring)

- **Technology**: AWS CloudWatch ServiceLens with X-Ray integration
- **Instrumentation**: 
  - Automatic JVM metrics for Java services
  - Custom instrumentation for business-critical paths
  - Database query performance tracking
- **Key Metrics**:
  - Application response time distributions
  - Error rates and exception counts
  - Memory usage patterns
  - Garbage collection metrics
  - Thread pool utilization
  - Database connection pool metrics
- **Business Metrics**:
  - POC creation rate
  - Search latency
  - Video generation time
  - Tenant-specific usage patterns

#### Infrastructure Metrics

- **Collection**: AWS Managed Prometheus
- **Visualization**: AWS Managed Grafana
- **Key Metrics**:
  - CPU, memory, disk utilization
  - Network throughput and errors
  - Container health and restart counts
  - Database connection counts and query performance
  - Cache hit/miss ratios
  - Message queue depths and processing rates
- **Custom Metrics**:
  - Business-specific throughput indicators
  - Multi-tenancy resource utilization
  - Search engine performance metrics
  - Video processing queue metrics

#### Mobile Performance Monitoring

- **Technology**: AWS Pinpoint Analytics + Firebase Performance Monitoring
- **Key Metrics**:
  - App startup time
  - Screen render time
  - API call latency from device
  - UI responsiveness (frame rate)
  - App stability (crash rate)
  - Network errors from mobile perspective
  - Battery consumption
  - Memory usage on device
- **User Experience Metrics**:
  - Time to interactive
  - Tap response time
  - Search completion time
  - Video playback metrics
- **Segmentation**:
  - By device type
  - OS version
  - Network type (WiFi/4G/5G)
  - Geographic location

#### Alerting Strategy

- **Primary Tool**: AWS CloudWatch Alarms with PagerDuty integration
- **Severity Levels**:
  - P1: Service outage, immediate response (24/7)
  - P2: Service degradation, response within 1 hour
  - P3: Non-critical issues, next business day
- **Alert Types**:
  - Static threshold alerts
  - Anomaly detection alerts
  - Composite alerts (multiple conditions)
  - Forecast-based alerts (predictive)
- **Key Alerts**:
  - Error rate > 1% (P1)
  - API latency > 500ms (P2)
  - Database CPU > 80% (P2)
  - Disk usage > 85% (P3)
  - Failed tenant authentications spike (P1)
  - Video generation failure > 5% (P2)
- **Alert Reduction**:
  - Correlation rules to prevent alert storms
  - Auto-remediation for known issues
  - Alert suppression during maintenance windows

#### Dashboard Strategy

- **Organization**:
  - Executive dashboard (high-level SLAs, business metrics)
  - Service-specific dashboards (per-service health)
  - Infrastructure dashboards
  - Mobile app performance dashboards
  - Tenant-specific dashboards
- **Key Visualizations**:
  - Service health heatmap
  - Request volume and latency histograms
  - Error rate time-series
  - Resource utilization gauges
  - User experience metrics
  - Business KPI correlations with system performance

#### SLOs and SLIs

- **Service Level Objectives**:
  - API availability: 99.9%
  - API latency (95th percentile): < 300ms
  - Search results: < 1s
  - Video generation: < 10 minutes
  - Mobile app crash rate: < 0.1%
- **SLI Measurement**:
  - Synthetic monitoring probes
  - Real user monitoring data
  - Error budget tracking
  - Burn rate alerts for SLO violations

#### Correlation and Root Cause Analysis

- **Implementation**:
  - Common correlation IDs across all observability data
  - Service dependency mapping
  - Automated RCA suggestions
  - Change event correlation with incidents
- **Tools**:
  - AWS X-Ray service maps
  - Custom Grafana dashboards with unified metrics/logs/traces

### 🖹 10. Data Store Designs

For each different kind of data store i.e (Postgres, Memcached, Elasticache, S3, Neo4J etc...) describe the schemas, what would be stored there and why, main queries, expectations on performance. Diagrams are welcome but you really need some dictionaries.

### 🖹 11. Technology Stack

Describe your stack, what databases would be used, what servers, what kind of components, mobile/ui approach, general architecture components, frameworks and libs to be used or not be used and why.

### 🖹 12. References

* Architecture Anti-Patterns: https://architecture-antipatterns.tech/
* EIP https://www.enterpriseintegrationpatterns.com/
* SOA Patterns https://patterns.arcitura.com/soa-patterns
* API Patterns https://microservice-api-patterns.org/
* Anti-Patterns https://sourcemaking.com/antipatterns/software-development-antipatterns
* Refactoring Patterns https://sourcemaking.com/refactoring/refactorings
* Database Refactoring Patterns https://databaserefactoring.com/
* Data Modelling Redis https://redis.com/blog/nosql-data-modeling/
* Cloud Patterns https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/introduction.html
* 12 Factors App https://12factor.net/
* Relational DB Patterns https://www.geeksforgeeks.org/design-patterns-for-relational-databases/
* Rendering Patterns https://www.patterns.dev/vanilla/rendering-patterns/
* REST API Design https://blog.stoplight.io/api-design-patterns-for-rest-web-services
