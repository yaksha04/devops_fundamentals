What is OpenTelemetry?

OpenTelemetry (often called OTel) is an open-source observability framework used to collect, generate, process, and export telemetry data from applications and infrastructure.

Telemetry data mainly means:

Logs → “What happened?”
Metrics → “How much/how often?”
Traces → “Where exactly is the problem?”

It is maintained under the Cloud Native Computing Foundation (same ecosystem as Kubernetes and Prometheus).

Why OpenTelemetry was Needed

Earlier companies used:

One tool for logs
One tool for monitoring
One tool for tracing

Example:

Logs → ELK stack
Metrics → Prometheus
Traces → Jaeger

Problem:
Every vendor had:

different SDKs
different agents
different APIs
vendor lock-in

If company changed monitoring vendor:
👉 Entire instrumentation rewrite.

OpenTelemetry solved this by creating:

one standard
one instrumentation format
one collection pipeline

So now:

Instrument once → export anywhere.

Simple Real-Life Example

Imagine your app:

User → Frontend → API Gateway → Auth Service → Payment Service → Database

User says:

“Payment failed.”

Without OpenTelemetry:

You manually check logs everywhere
Waste hours

With OpenTelemetry:
You can see:

request journey
exact failing service
response times
bottleneck
DB query delay
error traces

Basically:

X-ray for distributed systems.

Core Pillars of OpenTelemetry
1. Traces

Tracing tracks the journey of a request across services.

Example:

Request ID: abc123

Frontend
   ↓
API Gateway
   ↓
Auth Service
   ↓
Payment Service
   ↓
Database

Every step is called a Span.

Collection of spans = Trace

Important Terms in Tracing
Span

A single unit of work.

Example:

DB query
API call
function execution

Span contains:

start time
end time
duration
status
metadata
Trace

Complete request lifecycle.

Example:

Trace:
User login request

Spans:
- API request
- authentication
- DB query
- token generation
Parent Span & Child Span

Example:

Frontend Request
 ├── Auth Service
 │     └── DB Query
 └── Payment Service

Hierarchy helps identify bottlenecks.

2. Metrics

Metrics are numeric measurements over time.

Example:

CPU usage
memory usage
request count
latency
error rate

Examples:

requests_total = 5000
cpu_usage = 70%
response_time = 240ms
Types of Metrics
Counter

Only increases.

Example:

total_requests = 1000
Gauge

Can increase/decrease.

Example:

memory_usage = 2GB
Histogram

Measures distributions.

Example:

API response times:
100ms
120ms
500ms

Used for latency analysis.

3. Logs

Traditional logs:

INFO User logged in
ERROR Payment failed

OpenTelemetry now standardizes logs too.

Earlier:

logs separate
traces separate

Now:
You can correlate them.

Example:

TraceID = abc123
ERROR Payment failed

Now you can connect:

logs
traces
metrics

Together.

This is called:

Observability
What is Observability?

Monitoring tells:

“Something broke.”

Observability tells:

“WHY it broke.”

Huge difference.

OpenTelemetry Architecture

Main components:

Application
   ↓
OTel SDK
   ↓
OTel Collector
   ↓
Backend (Grafana/Jaeger/NewRelic/etc.)
1. Instrumentation

Adding telemetry generation into code.

Example in Python:

from opentelemetry import trace

tracer = trace.get_tracer(__name__)

with tracer.start_as_current_span("login"):
    print("User login")

This creates a span.

2. SDK

SDK does:

generate spans
metrics
context propagation
sampling

Each language has SDK:

Java
Go
Python
Node.js
Rust
etc.
3. OpenTelemetry Collector

MOST IMPORTANT PART.

OpenTelemetry Collector acts like a telemetry pipeline server.

It:

receives telemetry
processes data
filters data
batches data
exports data
Why Collector is Important

Without collector:

App → Datadog
App → Jaeger
App → Prometheus

Messy.

With collector:

Apps
  ↓
OTel Collector
  ↓
Any backend

Cleaner architecture.

Collector Pipeline
Receiver → Processor → Exporter
Receiver

Collects telemetry.

Examples:

OTLP
Jaeger
Zipkin
Prometheus receiver
Processor

Modifies telemetry.

Examples:

batching
filtering
sampling
memory limiting
Exporter

Sends telemetry somewhere.

Examples:

Jaeger
Prometheus
Grafana
Datadog
Splunk
OTLP Protocol

OTLP = OpenTelemetry Protocol.

Default standard communication protocol.

Uses:

gRPC
HTTP

This is the standard way services send telemetry.

Context Propagation

VERY IMPORTANT concept.

Suppose request moves:

Frontend → API → DB

How does every service know:

“This belongs to same request”?

Using Trace Context.

OpenTelemetry injects:

trace-id
span-id

inside headers.

Example:

traceparent: 00-abcd1234...

This is called:

Distributed Tracing
Auto Instrumentation vs Manual Instrumentation
Auto Instrumentation

Agent automatically collects telemetry.

Example:

Java agent
Python auto instrumentation

Easy setup.

Good for:

beginners
fast setup
Manual Instrumentation

Developer writes spans manually.

More control.

Used for:

custom business logic
advanced debugging
Sampling

Tracing every request is expensive.

Imagine:

1 million requests/sec

Storage explodes.

So sampling decides:

which traces to keep
which to ignore

Types:

head sampling
tail sampling
OpenTelemetry + DevOps

This is why DevOps engineers LOVE it.

Because in microservices:

debugging becomes nightmare
especially Kubernetes

OTel helps:

production debugging
performance monitoring
latency tracking
SRE workflows
incident response
OpenTelemetry in Kubernetes

Very common architecture:

Pods
 ↓
OTel Agent
 ↓
OTel Collector
 ↓
Grafana/Jaeger/Tempo

Usually deployed using:

DaemonSets
sidecars
gateway collectors
Common Stack in Industry
Open Source Stack
OpenTelemetry
   ↓
Prometheus
   ↓
Grafana

Tracing:

OpenTelemetry
   ↓
Jaeger or Tempo

Logs:

OpenTelemetry
   ↓
Loki or Elasticsearch
OpenTelemetry + Prometheus

OTel can expose metrics in Prometheus format.

Prometheus scrapes metrics.

Very common setup in DevOps.

OpenTelemetry + Grafana

Grafana visualizes:

metrics
logs
traces

with dashboards.
