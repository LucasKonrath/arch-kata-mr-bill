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

### 4.1 Overall diagram
![alt text](image-9.png)

### 4.2 Use cases
![alt text](image-10.png)


### 🧭 5. Trade-offs

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

#### 6.1 - Class Diagrams

![alt text](image-3.png)

![alt text](image-4.png)

![alt text](image-7.png)

![alt text](image-6.png)

![alt text](image-8.png)
#### 6.2 - Contract Documentation

#### Swagger Contract (Sync)

View [openapi-spec.yml](./openapi-spec.yml) on [Swagger Editor](https://editor.swagger.io/)

#### Async Api Contract (Messages/Websocket)
View [asyncapi-spec.yml](./asyncapi-spec.yml) on [AsyncApi Studio](https://studio.asyncapi.com/)

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

Persistence Model - Table Structure and Main Queries

![alt text](image-11.png)

##### PostgreSQL Database Schemas

##### Tenants
```sql
CREATE TABLE tenants (
  tenant_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(100) NOT NULL,
  domain VARCHAR(255) NOT NULL UNIQUE,
  subscription_plan VARCHAR(50) NOT NULL,
  status VARCHAR(20) NOT NULL DEFAULT 'ACTIVE',
  created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  settings JSONB NOT NULL DEFAULT '{}'::jsonb
);

CREATE INDEX idx_tenants_domain ON tenants(domain);
CREATE INDEX idx_tenants_status ON tenants(status);
```

##### Users
```sql
CREATE TABLE users (
  user_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID NOT NULL REFERENCES tenants(tenant_id),
  email VARCHAR(255) NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  full_name VARCHAR(100) NOT NULL,
  role VARCHAR(20) NOT NULL DEFAULT 'USER',
  created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  last_login_at TIMESTAMP WITH TIME ZONE,
  status VARCHAR(20) NOT NULL DEFAULT 'ACTIVE',
  UNIQUE (tenant_id, email)
);

CREATE INDEX idx_users_tenant_id ON users(tenant_id);
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_status ON users(status);

-- Enable Row Level Security
ALTER TABLE users ENABLE ROW LEVEL SECURITY;

-- Create policy for tenant isolation
CREATE POLICY tenant_isolation_policy ON users
  USING (tenant_id = current_setting('app.current_tenant_id')::uuid);
```

#### POCs
```sql
CREATE TABLE pocs (
  poc_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(user_id),
  tenant_id UUID NOT NULL REFERENCES tenants(tenant_id),
  name VARCHAR(100) NOT NULL,
  description TEXT,
  repository_url VARCHAR(255) NOT NULL,
  language VARCHAR(50),
  is_public BOOLEAN NOT NULL DEFAULT FALSE,
  created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  deleted_at TIMESTAMP WITH TIME ZONE,
  thumbnail_url VARCHAR(255)
);

CREATE INDEX idx_pocs_tenant_id ON pocs(tenant_id);
CREATE INDEX idx_pocs_user_id ON pocs(user_id);
CREATE INDEX idx_pocs_language ON pocs(language);
CREATE INDEX idx_pocs_created_at ON pocs(created_at);
CREATE INDEX idx_pocs_is_public ON pocs(is_public);

-- Enable Row Level Security
ALTER TABLE pocs ENABLE ROW LEVEL SECURITY;

-- Create policy for tenant isolation
CREATE POLICY tenant_isolation_policy ON pocs
  USING (tenant_id = current_setting('app.current_tenant_id')::uuid);

CREATE TABLE poc_tags (
  poc_id UUID NOT NULL REFERENCES pocs(poc_id) ON DELETE CASCADE,
  tag VARCHAR(50) NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  PRIMARY KEY (poc_id, tag)
);

CREATE INDEX idx_poc_tags_tag ON poc_tags(tag);

CREATE TABLE poc_frameworks (
  poc_id UUID NOT NULL REFERENCES pocs(poc_id) ON DELETE CASCADE,
  framework VARCHAR(50) NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  PRIMARY KEY (poc_id, framework)
);

CREATE INDEX idx_poc_frameworks_framework ON poc_frameworks(framework);
```

#### Content Generation(Report/Video)
```sql
CREATE TABLE content_requests (
  request_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(user_id),
  tenant_id UUID NOT NULL REFERENCES tenants(tenant_id),
  type VARCHAR(20) NOT NULL, -- 'VIDEO' or 'REPORT'
  status VARCHAR(20) NOT NULL DEFAULT 'PENDING', -- 'PENDING', 'PROCESSING', 'COMPLETED', 'FAILED'
  title VARCHAR(100) NOT NULL,
  description TEXT,
  from_date TIMESTAMP WITH TIME ZONE,
  to_date TIMESTAMP WITH TIME ZONE,
  parameters JSONB, -- Stores format-specific parameters
  created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  completed_at TIMESTAMP WITH TIME ZONE,
  error_message TEXT,
  result_url VARCHAR(512),
  progress INT DEFAULT 0 -- 0-100 percentage
);

CREATE INDEX idx_content_requests_tenant_id ON content_requests(tenant_id);
CREATE INDEX idx_content_requests_user_id ON content_requests(user_id);
CREATE INDEX idx_content_requests_status ON content_requests(status);
CREATE INDEX idx_content_requests_created_at ON content_requests(created_at);
CREATE INDEX idx_content_requests_type ON content_requests(type);

-- Enable Row Level Security
ALTER TABLE content_requests ENABLE ROW LEVEL SECURITY;

-- Create policy for tenant isolation
CREATE POLICY tenant_isolation_policy ON content_requests
  USING (tenant_id = current_setting('app.current_tenant_id')::uuid);

CREATE TABLE content_request_pocs (
  request_id UUID NOT NULL REFERENCES content_requests(request_id) ON DELETE CASCADE,
  poc_id UUID NOT NULL REFERENCES pocs(poc_id),
  sequence_order INT NOT NULL,
  duration_seconds INT, -- For videos
  PRIMARY KEY (request_id, poc_id)
);

CREATE INDEX idx_content_request_pocs_poc_id ON content_request_pocs(poc_id);
```

#### Dojos

```sql
CREATE TABLE dojos (
  dojo_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  creator_id UUID NOT NULL REFERENCES users(user_id),
  tenant_id UUID NOT NULL REFERENCES tenants(tenant_id),
  name VARCHAR(100) NOT NULL,
  description TEXT,
  language VARCHAR(50) NOT NULL,
  max_participants INT,
  is_private BOOLEAN NOT NULL DEFAULT TRUE,
  scheduled_start_time TIMESTAMP WITH TIME ZONE,
  initial_code TEXT,
  join_code VARCHAR(20) NOT NULL UNIQUE,
  status VARCHAR(20) NOT NULL DEFAULT 'SCHEDULED', -- 'SCHEDULED', 'ACTIVE', 'COMPLETED', 'CANCELLED'
  created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  started_at TIMESTAMP WITH TIME ZONE,
  ended_at TIMESTAMP WITH TIME ZONE
);

CREATE INDEX idx_dojos_tenant_id ON dojos(tenant_id);
CREATE INDEX idx_dojos_creator_id ON dojos(creator_id);
CREATE INDEX idx_dojos_status ON dojos(status);
CREATE INDEX idx_dojos_join_code ON dojos(join_code);
CREATE INDEX idx_dojos_scheduled_start_time ON dojos(scheduled_start_time);

-- Enable Row Level Security
ALTER TABLE dojos ENABLE ROW LEVEL SECURITY;

-- Create policy for tenant isolation
CREATE POLICY tenant_isolation_policy ON dojos
  USING (tenant_id = current_setting('app.current_tenant_id')::uuid);

CREATE TABLE dojo_participants (
  dojo_id UUID NOT NULL REFERENCES dojos(dojo_id) ON DELETE CASCADE,
  user_id UUID NOT NULL REFERENCES users(user_id),
  role VARCHAR(20) NOT NULL DEFAULT 'PARTICIPANT', -- 'PARTICIPANT', 'OBSERVER'
  join_time TIMESTAMP WITH TIME ZONE,
  leave_time TIMESTAMP WITH TIME ZONE,
  last_active_time TIMESTAMP WITH TIME ZONE,
  PRIMARY KEY (dojo_id, user_id)
);

CREATE INDEX idx_dojo_participants_user_id ON dojo_participants(user_id);

CREATE TABLE dojo_code_snapshots (
  snapshot_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  dojo_id UUID NOT NULL REFERENCES dojos(dojo_id) ON DELETE CASCADE,
  timestamp TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  code TEXT NOT NULL,
  user_id UUID REFERENCES users(user_id) -- NULL for system-generated snapshots
);

CREATE INDEX idx_dojo_code_snapshots_dojo_id ON dojo_code_snapshots(dojo_id);
CREATE INDEX idx_dojo_code_snapshots_timestamp ON dojo_code_snapshots(timestamp);

CREATE TABLE dojo_chat_messages (
  message_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  dojo_id UUID NOT NULL REFERENCES dojos(dojo_id) ON DELETE CASCADE,
  user_id UUID NOT NULL REFERENCES users(user_id),
  message TEXT NOT NULL,
  timestamp TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_dojo_chat_messages_dojo_id ON dojo_chat_messages(dojo_id);
CREATE INDEX idx_dojo_chat_messages_timestamp ON dojo_chat_messages(timestamp);
```

### OpenSearch

#### POC Search Index
```json
{
  "settings": {
    "index": {
      "number_of_shards": 3,
      "number_of_replicas": 1
    },
    "analysis": {
      "analyzer": {
        "code_analyzer": {
          "type": "custom",
          "tokenizer": "standard",
          "filter": ["lowercase", "asciifolding", "code_filter"]
        }
      },
      "filter": {
        "code_filter": {
          "type": "stop",
          "stopwords": ["function", "class", "var", "const", "let", "return", "if", "else", "for", "while"]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "poc_id": { "type": "keyword" },
      "user_id": { "type": "keyword" },
      "tenant_id": { "type": "keyword" }, 
      "name": { 
        "type": "text", 
        "analyzer": "standard",
        "fields": {
          "keyword": { "type": "keyword" }
        }
      },
      "description": { "type": "text", "analyzer": "standard" },
      "language": { "type": "keyword" },
      "tags": { "type": "keyword" },
      "frameworks": { "type": "keyword" },
      "is_public": { "type": "boolean" },
      "repository_url": { "type": "keyword" },
      "created_at": { "type": "date" },
      "updated_at": { "type": "date" },
      "code_snippets": { "type": "text", "analyzer": "code_analyzer" }
    }
  }
}
```

#### Dojo Search Index
```json
{
  "settings": {
    "index": {
      "number_of_shards": 2,
      "number_of_replicas": 1
    }
  },
  "mappings": {
    "properties": {
      "dojo_id": { "type": "keyword" },
      "creator_id": { "type": "keyword" },
      "tenant_id": { "type": "keyword" },
      "name": { 
        "type": "text", 
        "fields": {
          "keyword": { "type": "keyword" }
        }
      },
      "description": { "type": "text" },
      "language": { "type": "keyword" },
      "status": { "type": "keyword" },
      "is_private": { "type": "boolean" },
      "scheduled_start_time": { "type": "date" },
      "created_at": { "type": "date" },
      "started_at": { "type": "date" },
      "ended_at": { "type": "date" },
      "participant_count": { "type": "integer" },
      "tags": { "type": "keyword" }
    }
  }
}
```

### Main Queries
#### Search POC by criteria
```sql
-- PostgreSQL query to search POCs with filters and tenant isolation
SELECT p.*, array_agg(DISTINCT pt.tag) as tags, array_agg(DISTINCT pf.framework) as frameworks
FROM pocs p
LEFT JOIN poc_tags pt ON p.poc_id = pt.poc_id
LEFT JOIN poc_frameworks pf ON p.poc_id = pf.poc_id
WHERE p.tenant_id = :tenant_id  -- Multi-tenant isolation
  AND (p.user_id = :user_id OR p.is_public = TRUE)
  AND (:language IS NULL OR p.language = :language)
  AND (
    :search_term IS NULL OR 
    p.name ILIKE '%' || :search_term || '%' OR
    p.description ILIKE '%' || :search_term || '%'
  )
  AND p.deleted_at IS NULL
GROUP BY p.poc_id
HAVING (:tag IS NULL OR :tag = ANY(array_agg(pt.tag)))
ORDER BY p.created_at DESC
LIMIT :limit OFFSET :offset;
```

### OpenSearch POC Query
```json
{
  "query": {
    "bool": {
      "must": [
        { "term": { "tenant_id": "{{tenant_id}}" } },
        {
          "bool": {
            "should": [
              { "term": { "user_id": "{{user_id}}" } },
              { "term": { "is_public": true } }
            ],
            "minimum_should_match": 1
          }
        },
        {
          "multi_match": {
            "query": "{{search_term}}",
            "fields": ["name^3", "description^2", "code_snippets"]
          }
        }
      ],
      "filter": [
        {
          "bool": {
            "should": [
              { "term": { "language": "{{language}}" } },
              { "bool": { "must_not": { "exists": { "field": "language" } } } }
            ]
          }
        },
        {
          "bool": {
            "should": [
              { "term": { "tags": "{{tag}}" } },
              { "bool": { "must_not": { "exists": { "field": "tags" } } } }
            ]
          }
        }
      ]
    }
  },
  "sort": [
    { "created_at": { "order": "desc" } }
  ],
  "from": "{{offset}}",
  "size": "{{limit}}",
  "aggs": {
    "languages": {
      "terms": { "field": "language", "size": 20 }
    },
    "tags": {
      "terms": { "field": "tags", "size": 50 }
    },
    "frameworks": {
      "terms": { "field": "frameworks", "size": 20 }
    }
  }
}
```

#### Get POCs for annual video
```sql
-- Get all POCs for the year for video generation with tenant isolation
SELECT p.*, array_agg(DISTINCT pt.tag) as tags, array_agg(DISTINCT pf.framework) as frameworks
FROM pocs p
LEFT JOIN poc_tags pt ON p.poc_id = pt.poc_id
LEFT JOIN poc_frameworks pf ON p.poc_id = pf.poc_id
WHERE p.tenant_id = :tenant_id  -- Multi-tenant isolation
  AND p.user_id = :user_id
  AND p.created_at BETWEEN :from_date AND :to_date
  AND p.deleted_at IS NULL
  AND (:include_tag IS NULL OR EXISTS (
    SELECT 1 FROM poc_tags 
    WHERE poc_id = p.poc_id AND tag = ANY(:include_tags)
  ))
  AND (:exclude_tag IS NULL OR NOT EXISTS (
    SELECT 1 FROM poc_tags 
    WHERE poc_id = p.poc_id AND tag = ANY(:exclude_tags)
  ))
GROUP BY p.poc_id
ORDER BY p.created_at ASC;
```

#### Dojo Queries
#### Find active and upcoming dojos
```SQL
-- Find active and upcoming public dojos with tenant isolation
SELECT d.*, 
       u.full_name AS creator_name,
       COUNT(dp.user_id) AS participant_count
FROM dojos d
JOIN users u ON d.creator_id = u.user_id
LEFT JOIN dojo_participants dp ON d.dojo_id = dp.dojo_id
WHERE d.tenant_id = :tenant_id  -- Multi-tenant isolation
  AND d.status IN ('SCHEDULED', 'ACTIVE')
  AND (d.is_private = FALSE OR d.creator_id = :user_id OR EXISTS (
    SELECT 1 FROM dojo_participants 
    WHERE dojo_id = d.dojo_id AND user_id = :user_id
  ))
  AND (:language IS NULL OR d.language = :language)
  AND (
    :search_term IS NULL OR 
    d.name ILIKE '%' || :search_term || '%' OR
    d.description ILIKE '%' || :search_term || '%'
  )
GROUP BY d.dojo_id, u.full_name
ORDER BY 
  CASE 
    WHEN d.status = 'ACTIVE' THEN 0 
    ELSE 1 
  END,
  d.scheduled_start_time ASC
LIMIT :limit OFFSET :offset;
```

#### Get Dojo details
```sql
-- Get dojo details with participants and tenant isolation
SELECT d.*,
       u.full_name AS creator_name,
       json_agg(
         json_build_object(
           'user_id', dp.user_id,
           'full_name', pu.full_name,
           'role', dp.role,
           'join_time', dp.join_time,
           'last_active_time', dp.last_active_time
         )
       ) AS participants
FROM dojos d
JOIN users u ON d.creator_id = u.user_id
LEFT JOIN dojo_participants dp ON d.dojo_id = dp.dojo_id
LEFT JOIN users pu ON dp.user_id = pu.user_id
WHERE d.tenant_id = :tenant_id  -- Multi-tenant isolation
  AND d.dojo_id = :dojo_id
GROUP BY d.dojo_id, u.full_name;
```

#### Get Dojo chat history
```sql
-- Get chat history for a dojo session with tenant isolation
SELECT m.message_id,
       m.user_id,
       u.full_name AS user_name,
       m.message,
       m.timestamp
FROM dojo_chat_messages m
JOIN users u ON m.user_id = u.user_id
JOIN dojos d ON m.dojo_id = d.dojo_id
WHERE d.tenant_id = :tenant_id  -- Multi-tenant isolation
  AND m.dojo_id = :dojo_id
ORDER BY m.timestamp ASC;
```

### S3 Storage Schema
```
mr-bill-platform/
│
├── static/                             # Static web resources
│   ├── images/                         # UI images
│   │   ├── logos/                      # Brand logos
│   │   ├── icons/                      # UI icons
│   │   └── backgrounds/                # Background images
│   ├── css/                            # Stylesheets
│   │   └── {version}/                  # Version-specific CSS
│   └── js/                             # JavaScript files
│       └── {version}/                  # Version-specific JavaScript
│
├── tenants/                            # Tenant-specific assets
│   └── {tenant_id}/                    # Partitioned by tenant ID
│       ├── branding/                   # Tenant branding assets
│       │   ├── logo.{ext}              # Tenant logo
│       │   └── theme.json              # Tenant UI theme configuration
│       └── users/                      # User content within this tenant
│           └── {user_id}/              # User-specific content
│               ├── profile/            # User profile assets
│               │   └── avatar.{ext}    # User avatar
│               ├── pocs/               # POC related assets
│               │   └── {poc_id}/       # POC specific assets
│               │       ├── thumbnail.{ext} # POC thumbnail
│               │       └── screenshots/    # POC screenshots
│               └── reports/            # Generated reports
│                   └── {report_id}.pdf # PDF reports
│
├── videos/                             # Generated videos
│   └── {tenant_id}/                    # Partitioned by tenant ID
│       └── {user_id}/                  # Further partitioned by user ID
│           ├── {year}/                 # Organized by year
│           │   └── {request_id}.mp4    # Video files
│           └── thumbnails/             # Video thumbnails
│               └── {request_id}.jpg    # Thumbnail for video preview
│
├── dojos/                              # Dojo session assets
│   └── {tenant_id}/                    # Partitioned by tenant ID
│       └── {dojo_id}/                  # Partitioned by dojo ID
│           └── snapshots/              # Code snapshots
│               └── {timestamp}.json    # Snapshot at specific time
│
└── temp/                               # Temporary assets
    └── {uuid}/                         # Temporary unique folders
        └── *                           # Various temporary files
```
### Caching
#### Service: Amazon ElastiCache (Redis 7.x LTS):
- Session storage
- API response caching
- Rate limiting implementation
- Distributed locking mechanisms

## 11.4 Messaging and Integration
### Event Bus
#### Service: Amazon SNS
- Pub/sub messaging between services
- Fan-out event distribution
- Delivery status tracking

### Message Processing
#### Service: Amazon SQS:
- Decoupling services
- Message buffering for traffic spikes
- Dead letter queues for error handling

## 11.5 Infrastructure and Deployment
### Compute
#### Service: Amazon EC2 with Auto Scaling Groups:
- Right-sized instances for each service
- Spot instances for cost optimization where applicable
- Automated scaling based on load metrics
### Content Delivery
#### Service: Amazon CloudFront:
- Global distribution of static assets
- Edge caching for improved performance
- AWS Shield integration for DDoS protection
- AWS WAF for application layer protection
### API Management
#### Service: Amazon API Gateway with Application Load Balancer:
- API traffic management
- Request throttling and quotas
- API documentation with Swagger UI
### Container Management
#### Service: Amazon ECS with EC2 launch type:
- Docker containers for service isolation
- Task definitions for resource allocation
## Service auto-scaling
### Infrastructure as Code:
#### Tool: Terraform (latest):
- Declarative infrastructure definition
- Environment consistency
- Modular component design
## 11.6 Security
### Encryption and Key Management
#### Service: AWS KMS:
- Encryption key management
- Data encryption at rest and in transit
- Secure key rotation
### Identity and Access Management
#### Service: AWS IAM:
- Fine-grained access control
- Service roles and policies
- Least privilege principle
### Network Security
#### Components:
- VPC with private subnets
- Security groups and NACLs
- VPC endpoints for AWS services
- AWS Shield for DDoS protection
- AWS WAF for web application firewall
### Application Security
#### Practices:
- OWASP Top 10 mitigation strategies
- Input validation and sanitization
### Content Security Policy (CSP):
- Rate limiting and bot protection
- Dependency vulnerability scanning
## 11.7 DevOps and Monitoring
### CI/CD Pipeline
#### Service: AWS CodePipeline with GitHub Actions:
- Automated testing and deployment
- Environment promotion workflows
- Infrastructure validation
- Monitoring and Observability
### Services:
- AWS CloudWatch for metrics and logs
- X-Ray for distributed tracing
- Grafana for visualization dashboards
- Prometheus for metric collection
### Logging
#### Implementation:
- Centralized logging with CloudWatch Logs
- Structured JSON logging format
- Log retention policies
- Log-based alerting
### Alerting
#### Service: Amazon SNS with PagerDuty integration
- Critical service alerts
- Escalation policies
- On-call rotation management
## 11.8 Video and Content Processing
### Video Generation Pipeline
#### Components:
- FFmpeg for video encoding and composition
- AWS Elemental MediaConvert for transcoding

## 11.9 Technology Selection Justification
### Flutter for Mobile: Chosen for its cross-platform capabilities while maintaining near-native performance. The hot reload feature accelerates development cycles, and the widget-based architecture aligns with modern UI development practices.

### React for Web: Selected for its component-based architecture, large ecosystem, and strong community support. React's virtual DOM provides efficient rendering for POC search results and real-time updates during dojo sessions.

### Spring Boot Backend: Offers robust enterprise features, excellent documentation, and integration capabilities. The mature ecosystem provides solutions for security, data access, and API development needs.

### PostgreSQL: Selected over MongoDB (as specified in non-goals) for its ACID compliance, reliable transactions, and advanced query capabilities needed for complex POC searches and analytics.

### OpenSearch: Provides powerful full-text search capabilities for POCs, better than what could be achieved with standard database queries. The aggregation framework enables sophisticated filtering and faceting.

### AWS Managed Services: Chosen to reduce operational overhead while providing enterprise-grade reliability and security. The ability to scale resources based on demand aligns with the cost-efficiency goals.

### SNS/SQS Messaging: Enables loose coupling between services, improving system resilience and allowing independent scaling of components.

### CloudFront with WAF: Provides content acceleration, security, and DDoS protection at the edge, critical for serving global users with low latency.

### EC2 with ASGs: Offers predictable performance (avoiding Lambda cold starts as mentioned in non-goals) while maintaining scalability and high availability.

### KMS for Encryption: Ensures data security through proper key management and encryption, addressing the robust security requirement.

### 🖹 12. References

####  API Design & Documentation
OpenAPI Specification: https://spec.openapis.org/oas/v3.0.3

AsyncAPI Specification: https://www.asyncapi.com/docs/specifications/v2.6.0

API Security Best Practices: https://owasp.org/www-project-api-security/

REST API Design Rules: https://restfulapi.net/

Diagramming & Architecture Visualization

PlantUML Documentation: https://plantuml.com/guide

C4 Model for Software Architecture: https://c4model.com/

Architecture Decision Records: https://adr.github.io/
#### AWS Architecture
AWS Well-Architected Framework: https://aws.amazon.com/architecture/well-architected/

AWS Multi-tenant SaaS Architecture: https://docs.aws.amazon.com/prescriptive-guidance/latest/saas-multitenant-separation/welcome.html

AWS Media Services: https://aws.amazon.com/media-services/
#### Multi-tenancy & SaaS
Multi-tenant Data Architecture: https://docs.microsoft.com/en-us/azure/architecture/guide/multitenant/considerations/data-considerations

SaaS Security Architecture: https://www.cisecurity.org/insights/white-papers/security-considerations-for-cloud-saas

#### Testing Strategy
Testing Microservices: https://martinfowler.com/articles/microservice-testing/

Contract Testing with Pact: https://docs.pact.io/

Testing Pyramid: https://martinfowler.com/articles/practical-test-pyramid.html

Chaos Engineering: https://principlesofchaos.org/

#### Observability
Distributed Tracing: https://opentracing.io/docs/overview/

OpenTelemetry: https://opentelemetry.io/docs/

SRE Observability: https://sre.google/sre-book/monitoring-distributed-systems/

Observability-Driven Development: https://charity.wtf/2020/03/03/observability-is-a-many-splendored-thing/
#### Collaborative Coding
WebSocket Protocol: https://datatracker.ietf.org/doc/html/rfc6455

Real-time Collaboration Patterns: https://www.ably.io/blog/8-real-time-challenges-to-consider-when-building-multiplayer-collaboration-apps

Operational Transform: https://en.wikipedia.org/wiki/Operational_transformation

#### Video Generation & Processing

FFmpeg Documentation: https://ffmpeg.org/documentation.html

Video Encoding Best Practices: https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Video_codecs

AWS Elemental Media Services: https://aws.amazon.com/media-services/resources/
#### Security

OWASP Top 10: https://owasp.org/www-project-top-ten/

OAuth 2.0 and OpenID Connect: https://oauth.net/2/

NIST Cybersecurity Framework: https://www.nist.gov/cyberframework

AWS Security Best Practices: https://aws.amazon.com/architecture/security-identity-compliance/
#### Database & Data Modeling

PostgreSQL Documentation: https://www.postgresql.org/docs/

Data Access Patterns: https://docs.microsoft.com/en-us/azure/architecture/patterns/category/data-management

Amazon OpenSearch: https://docs.aws.amazon.com/opensearch-service/

#### Event-Driven Architecture

Event-Driven Architecture: https://aws.amazon.com/event-driven-architecture/

CQRS Pattern: https://docs.microsoft.com/en-us/azure/architecture/patterns/cqrs

Event Sourcing: https://martinfowler.com/eaaDev/EventSourcing.html
#### DevOps & Monitoring

DevOps Handbook: https://itrevolution.com/the-devops-handbook/

Site Reliability Engineering: https://sre.google/books/

Prometheus Documentation: https://prometheus.io/docs/introduction/overview/

Infrastructure as Code with Terraform: https://learn.hashicorp.com/terraform
