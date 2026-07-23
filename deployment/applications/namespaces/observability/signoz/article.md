# Testing SigNoz as a Long-Time Grafana User: Pros, Cons, and Surprises

## 1. Introduction: Coming to SigNoz from the Grafana World
- Your background with Grafana
- Why you decided to try SigNoz
- Initial expectations vs curiosity
- Brief hint at surprises (both good and bad)

---

## 2. Initial Setup Experience
- How the installation/deployment process felt
- Comparison with Grafana + Prometheus + Loki stack
- Anything that felt easier or more opinionated
- Notes on resources, configs, or defaults

---

## 3. First Impressions of the UI & UX
- General look and feel
- Navigation experience
- Built-in dashboards vs Grafana’s blank-canvas approach
- Things that felt intuitive vs things that felt missing

---

## 4. Using SigNoz as an Observability Suite

### 4.1 Metrics
- Charting experience
- Querying metrics (ease vs complexity)
- Comparison to Grafana’s flexibility

### 4.2 Logs
- Log search/filter experience
- Performance comparisons to Loki
- Notes on ergonomics or indexing

### 4.3 Traces
- First impressions of built-in tracing
- Differences from Grafana Tempo/Jaeger setups
- Anything surprisingly good or unexpectedly rough

---

## 5. Pros — What SigNoz Did Better Than Expected
- Unified observability experience
- OpenTelemetry-native advantages
- Simpler setup for smaller teams
- Cleaner defaults or visualizations
- Any standout features

*(Add specific examples from your testing.)*

---

## 6. Cons — Where Grafana Still Wins
- Visualization limitations
- Smaller plugin ecosystem
- Less flexible dashboard options
- Areas that feel immature or missing
- Any pain points during testing

*(Keep this honest but constructive.)*

---

## 7. Unexpected Surprises
- Features you didn’t know existed
- Things you liked more than expected
- Things that didn’t meet expectations
- Any “aha!” moments worth sharing

---

## 8. Should Grafana Users Try SigNoz? — Your Verdict
- Who should seriously consider trying SigNoz
- Who should stay with Grafana for now
- Situations where SigNoz shines
- Situations where Grafana remains unbeatable

---

## 9. Closing Thoughts
- Your personal conclusion
- What you'd like to explore next
- Hopes for future improvements
- Invite readers to share their experiences

---


# Notes
I have been working in many projects with Prometheus Grafana Loki Tempo stack
I wanted to check if signoz provided better experience for not so technical users
short answer yes. ui is more friendly, lots ot resources out of the box
by out of the box i mean few modifications from default helm chart and not complex
But for specific scenarions grafana stack flexibility may be required. ie: multi tenanct

Infra used. K8s
(ill provide a link for signoz helm chart template)
(ill provide a link for signoz k8s-infra helm chart template)
we can get complex as we like, but with few and not complex setup we take a lot of benefits already
k8s-infra is important to automatically send logs and kubernetes metrics to signoz
obi will be useful to automatically instrument the entire cluster using ebpf

Platform
Both signoz and grafana hides a lot of complexity.
In exchange for flexibility and more community adoptiom grafana exposes a bit more complexity. Where you need more stack elements, such as Temop, Loki, Prometheus
No right answer, its a choice.
signoz uses customized collectors to supports its operation. but the initial user does not need to know much about it.

Logs
  Automatic setup using k8s-infra, you can customize blcklists, whitelists using namespaces
  Nice UI experience, switching between pods, deployments and other filters
  Logs multitenancy is not supported at this moment, this is a disadvantage agains grafana/loki for those who need it. an strategy would be to have multiple signoz instances

Tracing:
  The initial setup is simple you only need to send traces to signoz collector service endpoint
  Rich tracing vizualization with links to the logs when properly exported, service graphs.
  panel with latency, sorting by percetiles, errors rates, number of calls
  The servicemap is usefull to give a quick overview of the status of the services. (ill provide pictures)
  I wish it would be possible to click nodes in the service map to zoom in details about the service and connections

Metrics:
  Kubernetes metrics collected with k8s-infra will be automatically exported to Signoz
  One concert is many teams use prometheus metrics by default. This custom metrics monitored by Prometheus Service Monitor will not work automatically
  Signoz does not pull metrics as Prometheus does uf you need custom Prometheus metrics exporting then either you need to export it directly to signoz collector or use opentelemetry collectors with target allocators to collect and point them to signoz collectors. reference: https://signoz.io/docs/userguide/prometheus-metrics/
  This adds complexity to the very friendly signoz infra, but on the other side helps with collecting scaling as prometheus can be troublesome to horizontally.

Uptime/BlackBox like:
  Since signoz provides lots of bultin feature, it would be nice to have something such as uptimee/blackbox.

Alerts:
  TODO

Infrastructure section
  It maps your infra, k8s in this setup
  We can list every main k8s objects such as deplotment, pods, namespace, daemonset
  and easily find usefull inputs such as status, sirtable resource request limits usage.
  You can click and zoom in specfic obhect such as pod, and easily check logs, metrics, traces and events

Cost Meter:
  its useful to know how much data you are ingesting, by metrics, traces and logs.
  You can also see it as timeline

ui experience
UI is more interesting/friendlt than grafana, resemble enterprise dynatrace and possible other tools.
dashboards creation resembles a lot grafana dashboards, making it easier for a lot of people. (ill provide pictures)
it would be nice for a possibility to enable them directly in the ui, insteading of copying and paste json

community
we dont have the same amount of public dashboards tempaltes as grafana, but the are a variety of application tempaltes dashboards.
The ones for Kubernetes and pods details are usefull (ill provide picture)
