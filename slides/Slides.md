---
marp: true
theme: custom-default
transition: cover
footer: 'https://chris-ayers.com'
---

<!-- 
_color: white
_footer: 'https://github.com/Codebytes/sre-devops-platform-eng'
-->

![bg](./img/techorama.png)

<div class="columns">
<div>

</div>
<div>

# SRE, DevOps, and Platform Engineering
## Unraveling the Differences

### Chris Ayers

</div>
</div>


---

![bg left:40%](./img/portrait.png)

## Chris Ayers
### Senior Customer Engineer<br>Microsoft

<i class="fa-brands fa-twitter"></i> Twitter: @Chris\_L\_Ayers
<i class="fa-brands fa-mastodon"></i> Mastodon: @Chrisayers@hachyderm.io
<i class="fa-brands fa-linkedin"></i> LinkedIn: [chris-l-ayers](https://linkedin.com/in/chris-l-ayers/)
<i class="fa fa-window-maximize"></i> Blog: [https://chris-ayers.com/](https://chris-ayers.com/)
<i class="fa-brands fa-github"></i> GitHub: [Codebytes](https://github.com/codebytes)

---

![bg right w:500px](./img/sre-devops-plat-eng.drawio.svg)
# Agenda

- Common Problems
- Introduction to <br/>Site Reliability Engineering (SRE)
- Dive into DevOps
- Exploring Platform Engineering

---

# The Historical Divide

---

![bg right fit](img/silos.jpg)
## Development and Operations: Separate Realms

Historically, Development and Operations teams operated in silos, each with distinct responsibilities and goals.

---

# Historical Divide: Development vs Operations

| Aspect| Development (Dev)                             | Operations (Ops)                                   |
|-------------------------|--------------------------------------------------|-------------------------------------------------------|
| Focus       | Writing & updating code                          | Managing infrastructure & ensuring service reliability |
| Challenges      | Ensuring code works across environments          | Handling unforeseen changes & mitigating disruptions   |
| Mindset             | "Let's release new features quickly!"            | "Change can introduce issues; caution is necessary."   |
| Metrics | Speed of feature releases, Code quality          | System uptime, Response time to incidents              |

---

## The Wall of Confusion

<div class="columns">
<div>

The lack of collaboration often resulted in a "Wall of Confusion," where software released by the Development team would encounter issues in the environments managed by the Operations team.

</div>
<div>

![center](./img/wall-of-confusion.png)

</div>
</div>

---

### Results of the Divide

- **Slower Releases:** Waiting for Operations to deploy.
- **Missed Deadlines:** Unforeseen issues leading to back-and-forth.
- **Blame Games:** Pointing fingers when things went wrong.
- **Decreased Productivity:** Duplication of effort and miscommunication.

---

### Bridging the Gap

The realization of these inefficiencies led to the rise of the DevOps movement, seeking to break down the silos and promote collaboration between Development and Operations.

---

![bg left:40% w:80%](./img/sre.png)
# Introduction to SRE
> Site Reliability Engineering

---

# **SRE is what happens when you ask a software engineer to design an operations team**
*Benjamin Treynor Sloss*

---

# SRE Responsibilities

<div class="columns">
<div>

- Availability
- Latency
- Performance
- Efficiency

</div>
<div>

- Change Management
- Monitoring
- Emergency Response
- Capacity Planning

</div>
</div>

---

<!-- _footer: "" -->

![bg w:80%](img/yo-sre.png)

---

# <!-- fit --> Hope is not a strategy.
>Common SRE Saying

---

# Embracing Risk
   - Achieving high reliability is tough.
   - Learn from unexpected failures.
   - Always expect systems to have shortcomings.
   - SRE teams should proactively address risks.
   - Balance the costs and benefits of increased reliability.

---

<!-- _footer: "" -->

![bg](img/risk.png)

---
<style scoped>
table { display: table; }
tr { display: table-row; }
td, th { display: table-cell; }
table {
  width: 100%;
}
</style>
# Reliability

| Level       | Monthly Downtime | Annual Downtime | Cost  |
| ----------- | ---------------- | --------------- | ----- |
| **99.9%**   | 43.8m            | 8.75h           | $     |
| **99.95%**  | 21.9m            | 4.375h          | $$    |
| **99.99%**  | 4.38m            | 52.6m           | $$$   |
| **99.995%** | 2.19m            | 26.3m           | $$$$  |
| **99.999%** | 26s              | 5.25m           | $$$$$ |

>https://uptime.is/five-nines

---

# Service Level Objectives
| SLI | SLO | SLA |
|---|---|---|
| Service Level Indicator | Service Level Objective | Service Level Agreement |
| Metrics for service quality, e.g., error rate. | Targets, e.g., 99.9% uptime/month. | Contracts with set metrics and penalties. |
| Assess service quality. | Define service quality goals. | Formalize commitments and consequences. |

---

![SLA Pyramid](img/sla-slo-sli.png)

---

# Error Budgets

- A tool to balance reliability and rate of innovation.
- Allows for a predetermined level of acceptable unreliability.

---

<!-- _footer: "" -->

![bg  fit ](img/budget.png)

---

# Components of Error Budgets

| Component     | Description                 | Example                                     |
| ------------- | --------------------------- | ------------------------------------------- |
| **Objective** | Desired success level       | 99.95%                                      |
| **SLI**       | Evaluation of failed events | 95th percentile latency < 100ms over 5 mins |
| **Timeframe** | Recency bias for the SLI    | Previous 28 days                            |

---

# Constructing an Error Budget

> "99.95% of the 95th percentile latency of API requests over 5 mins is < 100ms over the previous 28 days."

**Error Budget** = 1 - *Objective*

For our example:

- Objective: 99.95% (or 0.9995)
- Error Budget: 0.05% (or 0.0005)

Over 28 days, this is:

> 20.16 minutes (.0005 * (28 * 24 * 60))

---

# When the Error Budget is Exhausted?

<div class="columns">
<div>

- **Halt**: 
  - No new features or deployments.
  - No changes or experiments.

</div>
<div>

- **Prioritize**:
  - Enhance reliability.
  - Minimize toil.
  - Bolster monitoring & automation.
  - Strengthen testing.

</div>
</div>

* **Improve reliability.**
* **Improve reliability.**

---

# Toil
- Manual work needed to maintain a service.
- SREs use automation to minimize toil.
![bg right w:90%](https://imgs.xkcd.com/comics/automation.png)

---

![bg right fit](img/toil.png)
# Managing Toil
- Identify time-consuming SRE tasks.
- Distinguish actual toil from manual tasks.
- Set clear guidelines.
- Build features that reduce toil and enhance reliability.

---

## Examples of Toil

- Regularly restarting a failing service.
- Manually scaling services up/down based on traffic.
- Running repetitive database maintenance tasks.
- Hand-creating reports from logs.
- Daily cleanup of temporary files.
- Manually updating configuration files across servers.

---


# Feedback Loops in SRE

- **Feedback Loops** ensure that systems are continuously improved based on results or feedback.
- They promote a culture of iterative refinement and rapid response.

## Why are they important?

- Identify areas of improvement quickly.
- Adjust strategies or methodologies based on outcomes.
- Foster better communication and understanding between teams.

---

# Monitoring Distributed Systems

## Why Monitor?
- Distributed systems span multiple locations, increasing complexity.
- Detect anomalies early to prevent bigger problems.
- Gain insights into system health and pinpoint areas for improvement.

---
<style scoped>
table { display: table; }
tr { display: table-row; }
td, th { display: table-cell; }
table {
  width: 100%;
}
</style>

# Core Monitoring Types

|                 | **Black-box**       | **White-box**          |
| --------------- | ------------------- | ---------------------- |
| **Focus**       | System Outputs      | System Internals       |
| **Reflection**  | User Experience     | Component Interactions |
| **Data Source** | External Tests      | Internal Metrics/Logs  |
| **Use Case**    | Availability Checks | Debugging & Profiling  |

---

## Tech Metrics Overview
| Metric | Full Form | Purpose |
|---|---|---|
| MTBF | Mean Time Before Failure | Average time between failures. |
| MTTR | Mean Time To Recovery/Repair/Respond/Resolve | Time to recover from a failure. |
| MTTF | Mean Time To Failure | Expected time to the first failure. |
| MTTA | Mean Time To Acknowledge | Time to acknowledge an incident. |

---

# Effective Alerting
- Alert based on potential user impact.
- Notify when nearing an SLO breach.
- Make alerts clear and directly useful.
![bg right fit](img/monitoring.png)

---

# Monitoring Distributed Systems
## Best Practices
- **Consistent Metrics**: Adopt uniform metrics throughout components for clarity.
- **Granular Monitoring**: Detailed observation, both system-wide and at the component level.
- **Postmortems**: Utilize monitoring data post-incident to derive insights and prevent recurrences.

---

# Monitoring Distributed Systems
## Visualization & Review
- **Dashboards**: Implement live visualization tools for real-time system status overviews.
- **Feedback Loops**: Continually refine monitoring based on feedback and new challenges.
- **Regular Reviews**: Periodically examine the system's monitoring setup for relevance and efficiency.

---

# Alerting & On-Call

- **Prioritize Alerts**  
   - High, medium, low severity levels.
   - Avoid alert fatigue with proper thresholds.
   
- **Ensure Alert Relevancy**  
   - Only trigger alerts for actionable events.
   - Refine and tune alerts regularly.

---

# On-Call Engineers
- **Rotation Schedules**  
   - Avoid burnout with shifts and breaks.
   - Implement regular handoffs for continuity.
   
- **Necessary Resources** 
   - Access to documentation and tools.
   - Clear escalation paths for critical issues.

---

# Troubleshooting & Emergency
- **Systematic Approach**  
   - Start from checking basic functionalities.
   - Use a top-down or bottom-up methodology.
   
- **Use Monitoring and Logging**  
   - Access to real-time data.
   - Historical logs for pattern analysis.

---

#  Handling System Emergencies and Outages
- **Establish Clear Communication Channels**  
   - Inform stakeholders promptly.
   - Regular status updates to teams and users.
   
- **Implement Quick Rollbacks**  
   - Have mechanisms to revert changes.
   - Backup systems to restore functionality.

---

# Incident Management
- **Incident Classification**  
   - Define what constitutes an incident.
   - Categorize by impact and urgency.
   
- **Assemble a Response Team**  
   - Cross-functional members for expertise.
   - Clear roles and responsibilities.

---

# Blameless Postmortems

- Understand incidents and prevent future ones.
- Focus on learning, not blaming.

<div class="columns">
<div>

## **Core Steps**:

- **Documentation**:  
   - Events timeline.
   - Taken actions.
   
- **Review Meeting**:  
   - Discuss outcomes.
   - Define action items.

</div>
<div>

## **Components**:

- **Timeline**: Sequence of events.
- **Impact Analysis**: Affected entities.
- **Root Cause**: Reason for incident.
- **Actions**: Preventative measures.


</div>
</div>

---

# **Release Engineering: Essence & Impact**

- **Essence**: Safe and efficient software updates deployment.
   - Key areas: Version control, CI/CD, rollout strategies, canary releases, and monitoring.

- **Impact**:  
   - Minimized downtime.
   - Faster deployments via automation.
   - Consistency and reduced issues.
   - Enhanced system reliability.

---

# Blast Radius of Change

![bg right fit](img/blast-radius.png)

- The "Blast Radius" refers to the potential impact of a change or failure.
- Understanding and managing the blast radius is crucial in minimizing disruptions.
- SREs focus on reducing the blast radius to ensure system stability and reliability.

---

# Feature Flags & Toggles

- **Feature Flags** (or Feature Toggles) are a technique that allows teams to modify system behavior without changing code.
  
## Benefits

- Enable/Disable features without deploying new code.
- Gradually roll out features to a subset of users.
- Easily roll back problematic features.
- Test in production, ensuring real-world performance.

---

# Canary Deployments

![bg right w:55%](img/canary1.drawio.png)

A release strategy involving gradual rollout to a small group before full deployment.

---

# Canary Deployments

![bg right w:55%](img/canary2.drawio.png)

"Canaries" are the initial users/servers to detect issues or bugs in the new release.

---

# Canary Deployments

![bg right w:55%](img/canary3.drawio.png)

Incremental deployment reduces the risk of widespread outages.

---

# Canary Deployments

![bg right w:55%](img/canary4.drawio.png)

Continuous monitoring and feedback gather performance insights.

---

# Blue Green Deployments

![bg right:40% w:90%](img/blue-green1.drawio.png)

- Parallel Environments: Maintain Blue (production) and Green (updates).
- Zero Downtime: Switch between Blue and Green without downtime.
- Testing & Validation: Thoroughly validate updates in the Green environment.
- Instant Rollback: Quickly revert to the stable Blue environment if issues arise.

---

# Blue Green Deployments

![bg right:40% w:90%](img/blue-green2.drawio.png)

- Controlled Release: Gradually shift traffic from Blue to Green.
- Canary Testing: Test updates with a small portion of traffic in the Green environment.
- Traffic Cut-Over: Switch all traffic to Green after successful validation.
- Rollback Option: Instantly return to the stable Blue environment if needed.

---

![bg left fit](./img/devops.png)

# Dive into DevOps

DevOps, popularized by figures like **Patrick Debois** and **Andrew Shafer**, emphasizes collaboration between development and operations, focusing on *cultural shifts*, *automation*, and *feedback loops* for faster, reliable software releases.

---

<div class="columns">
<div>

<br>
<br>

# “DevOps is the union of people, process, and products to enable continuous delivery of value to our end users.”

## - Donovan Brown

</div>
<div>

<br>
<br>

![w:300px center](img/donovan-brown.png)

</div>
</div>

---

## Cultural Shifts in DevOps

- **Collaboration Over Silos:** Breaking down the barriers between development and operations teams to work together seamlessly.
- **Blameless Culture:** Instead of pointing fingers, teams focus on learning from failures and continuously improving.
- **Empowerment and Ownership:** Every team member takes responsibility for the software's life cycle, from development to production.
- **Continuous Learning:** Regular retrospectives and a focus on iterative improvement.

---

# How we Work
- Agile
- Scrum
- Pair Programming
- Kanban
 
---

![bg fit left:40%](./img/team-topologies.jpg)

# Team Topologies

Understanding team structures and their interactions is crucial for efficient software delivery and system reliability. "Team Topologies" by Matthew Skelton and Manuel Pais offers insight into different team patterns for IT delivery.

---

## Four Core Team Patterns

1. **Stream-aligned Team:** Directly aligned to a flow of work from a segment of the business domain.
2. **Enabling Team:** Helps a stream-aligned team overcome obstacles.
3. **Complicated Subsystem Team:** Where mathematics/calculation is the main focus, separate from the main flow.
4. **Platform Team:** Offers services to other teams to accelerate delivery.

---

![bg w:80%](./img/Shapes%20Normal.png)
 
---

![bg right fit](./img/cicd-pipeline.png)

# CI/CD

**Continuous Integration & Continuous Deployment** streamline the software development lifecycle, ensuring that code changes are continuously integrated, tested, and delivered to production.

---

<div class="columns">
<div>

## Continuous Integration (CI)

- Automatically integrate and validate code changes.
- Run tests and security scans

</div>
<div>

## Continuous Deployment (CD)

- Automate deployment processes to various environments.
- Ensures production-ready releases.

</div>
</div>

---

## Benefits of CI/CD

- 🚀 **Faster Releases:** Reduced manual processes speed up software delivery.
- 🐞 **Improved Quality:** Early and frequent testing leads to fewer bugs.
- 🔁 **Rapid Feedback:** Immediate feedback on code changes for developers.
- 📈 **Increased Productivity:** Less time spent on manual tasks.

---

### Infrastructure as Code (IaC)

- Manage and provision infrastructure using code and automation.
- Ensures consistent and repeatable infrastructure deployments.
- Easily scale and replicate environments, reducing manual setup and errors.

---

### Feedback Loops

- Incorporate real-time feedback throughout the development process.
- Iteratively refine based on results or feedback.
- Enables rapid adjustments and promotes continuous improvement.

---

### Collaborative Culture

- Foster open communication and collaboration across departments.
- Eliminate traditional silos between development and operations.
- Shared responsibilities ensure everyone is accountable for the end product.

---

### Monitoring & Logging

- Continuous observation of applications and infrastructure.
- Rapidly detect, address, and prevent issues.
- Provide insights into system health, usage, and potential bottlenecks.

---

### Configuration Management

- Maintain and manage the software's consistency, performance, and functional attributes.
- Tools like Ansible, Chef, and Puppet standardize and automate configurations.

---

### Microservices

- Design software as suites of independently deployable services.
- Enables faster development, testing, and scaling of individual components.

---

### Containers & Orchestration

- Lightweight, standalone executable software packages.
- Ensure consistency across environments and scalability.
- Tools like Docker for containerization and Kubernetes for orchestration.

---

### DevSecOps

- Embed security into the DevOps process.
- Automated security checks during CI/CD.
- Ensures secure code and infrastructure from the start.

---

![bg left:40%](./img/platform.jpg)

# Exploring Platform Engineering

Platform Engineering is the nexus of software development, infrastructure management, and best practices, centered on providing robust, scalable, and efficient platforms for applications and services.

---

## Defining Platform Engineering

Platform Engineering facilitates:
- Streamlined software deployments
- Infrastructure scalability
- Seamless integration between tools and services
- Accelerated development processes

It's about laying the foundation upon which applications thrive.

---

## Key Concepts of Platform Engineering

---

### Self-service Platforms

Empowering developers with:
- Automated deployment pipelines
- Infrastructure provisioning with a click
- Monitoring and logging integrations

The aim? Minimize manual intervention and speed up the development lifecycle.

---

### Abstract Complexity

What does this mean?
- Hide intricate infrastructure details from developers.
- Provide standardized templates for deployment.
- Ensure developers focus on code, not infra setup.

Simplified processes, maximized efficiency.

---

### Microservices & Containers

Why are they crucial?
- **Flexibility:** Break applications into smaller, manageable units.
- **Scalability:** Scale components independently as needed.
- **Portability:** Containers ensure consistent environments across stages.

Tools like Kubernetes orchestrate these containers, ensuring reliability and scalability.

---

### Scaling & Performance

As demand grows:
- Dynamically allocate resources.
- Load balance to distribute traffic.
- Monitor in real-time for performance insights.

Optimizing resources ensures the system remains responsive even under peak loads.

---

## Why is Platform Engineering Vital?

1. **Developer Experience**
1. **Accelerated Development:** Less time grappling with infrastructure means more time coding.
1. **Consistency:** Same tools, processes, and environments across teams.
1. **Reliability:** Best practices ensure high availability and minimal downtime.
1. **Future-proofing:** Designed with growth and change in mind.

---

## Challenges in Enterprise Workflow

- **Ticketing Systems:** Delays due to lengthy "ServiceNow" ticket resolutions.
  
- **Approval Bottlenecks:** 
  - Security signoffs
  - Network configurations
  - Multiple rejections without clear feedback
  - Ambiguous task descriptions leading to incorrect implementations


![bg right:40% fit](img/one-eternity-later.png)

---

# Enhancing Developer Experience

- **Self-service:** Automated processes for greater developer autonomy.
- **Simplified Infrastructure:** Shielding developers from complex infrastructure details.
- **Microservices & Containers:** Ensuring application flexibility, scalability, and consistent environments.
- **Efficient Scaling:** Dynamic resource allocation and optimized load balancing.
- **Holistic Experience:** Faster development cycles, uniformity across tools, reliable systems


---

## Conclusion

Platform Engineering is more than just tools and processes. It's an ethos that prioritizes efficiency, reliability, and scalability, ensuring applications and services are always at their best.

---

## Conclusion

---

SRE, DevOps, and Platform Engineering intersect at ensuring efficient and reliable software delivery and operation.

---

**Key Takeaways**

- **Collaboration & Automation:** Central to all disciplines.
- **Continuous Improvement:** Better processes and tools.
- **End-to-end Responsibility:** From code to operation.

---

**SRE, DevOps, and Platform Engineering: Disentangling the Trio**

---

**Introduction**

In the ever-evolving landscape of software engineering, terms like SRE, DevOps, and Platform Engineering have become increasingly popular. But what do they mean, and how do they differ? Let’s delve into these disciplines and shed light on their distinctions.

---


**DevOps**

**Origin:** Coined from merging ‘Development’ and ‘Operations’, DevOps is a cultural shift that promotes collaboration between these two traditionally siloed teams.

**Key Features:**
- **CI/CD:** Continuous Integration and Continuous Deployment allow for quick code integrations and releases.
- **Infrastructure as Code (IaC):** Automation of infrastructure tasks.
- **Feedback Loops:** Quick detection and resolution of issues.

**Objective:** Streamline the process from code development to deployment, ensuring faster release cycles and better product quality.

---

**Platform Engineering**

**Origin:** As companies scaled and sought to manage their infrastructure more efficiently, the discipline of platform engineering emerged.

**Key Features:**
- **Self-service Platforms:** Tools that allow developers to deploy, manage, and scale applications.
- **Abstract Complexity:** Providing simpler interfaces to developers by hiding underlying complexities.
- **Containerization and Orchestration:** Use of containers for application deployment and orchestration tools like Kubernetes to manage them.

**Objective:** Create robust platforms that allow for scalable, efficient deployment and management of applications and services.

---

**SRE vs. DevOps vs. Platform Engineering: The Overlap**

While the three disciplines have distinct objectives, there is a significant overlap. For instance, automation is a common theme across all three. SRE and DevOps both focus on improving the release cycle, while Platform Engineering provides the tools to achieve this. 

---

**Conclusion**

In essence, SRE, DevOps, and Platform Engineering are disciplines that, while distinct, work hand-in-hand. SRE ensures reliability, DevOps promotes collaboration and streamlining, and Platform Engineering provides the tools and platforms necessary to achieve both. Understanding their nuances allows for better implementation and synergy among teams.

---

# DevOps vs. SRE

---

## Introduction

- DevOps and SRE: Overlapping and distinct areas in software engineering.

---

## Similarities

1. **Bridge Ops and Dev**: Synergy between teams.
2. **Automation**: Central to both.
3. **Combine Development and Operations**: Integrated processes.

---

## Differences: SRE

- **Focus**: Production, technical practices, metrics.
- **Concerns**: System availability, reliability, production.
- **People**: System engineers writing code.
- **Approach**: "How" things are done.

---

## Differences: DevOps

- **Focus**: Removing silos, end-to-end process.
- **Concerns**: Product development and delivery. 
- **People**: Diverse teams - product owners to ops.
- **Approach**: "What" unifies dev and ops.

---

## DevOps in Depth

### Definition

- Automating software lifecycle with dev/ops principles.

---

### DevOps: Focus & Goals

- **Collaboration, Automation, CI/CD**
- Goals: Improve collaboration, automate tasks, efficient pipelines.

---

### DevOps: Day-to-Day

- Infrastructure provisioning & configuration.
- CI/CD setup.
- Monitoring & troubleshooting.

---

### DevOps: Tools

- **Provisioning**: Ansible, SaltStack, Puppet...
- **CI/CD**: Jenkins, GitLab...
- **Containers**: Docker, Kubernetes...
- **Cloud & Monitoring**: AWS, Nagios...

---

### DevOps: Skills

- Linux, Git, Cloud, CI/CD, Scripting.

---

## SRE in Depth

### Definition

- Ensuring scalability, reliability, availability of systems.

---

### SRE: Focus & Goals

- **Stability, Reliability, Availability**
- Goals: Reduce incidents, improve recovery, best monitoring practices.

---

### SRE: Day-to-Day

- Ensure software reliability.
- Monitor metrics.
- Infrastructure automation.
- Root cause analysis.

---

### SRE: Tools

- **SLO Monitoring**: New Relic, Datadog...
- **Incidents**: Slack, PagerDuty...
- **Automation & Observability**: Terraform, OpenTelemetry...

---

### SRE: Skills

- Coding, Monitoring, Troubleshooting, Networking.

---

## Case Studies

- **Netflix (SRE)**: Simian Army.
- **Etsy (DevOps)**: CI/CD pipelines.

---

## Dual Approaches

- **Theory vs. Practical**: Two sides of a coin.
- **DevOps**: Core development, failures, tickets.
- **SRE**: Core implementation, deployment, monitoring.

---

## Final Thoughts

- **DevOps Principles**: Reduce silos, accept failure, measure.
- **SRE Philosophy**: Engineer-designed operations.
- **Noteworthy**: Patrick Debois, Andrew Shafer, Amazon's motto.

---

