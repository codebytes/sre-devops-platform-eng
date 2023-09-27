---
marp: true
theme: custom-default
transition: cover
footer: 'https://chris-ayers.com'
---

<!-- _footer: 'https://github.com/Codebytes/sre-devops-platform-eng' -->

![bg left w:500px](./img/sre-devops-plat-eng.drawio.svg)


![w:120](img/portrait.png)
## Chris Ayers

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

# Agenda

- Introduction to SRE
- Dive into DevOps
- Exploring Platform Engineering

---

![bg left:40%](./img/reliability.jpg)

# Introduction to SRE

---

SRE, or Site Reliability Engineering, originated at Google when they tasked a team to enhance the reliability of their services.

---

## Key Concepts of SRE

---

- **Software Engineering meets Systems Administration:** SRE applies software engineering principles to operations tasks.

---

| SLI | SLO | SLA |
|---|---|---|
| Service Level Indicator | Service Level Objective | Service Level Agreement |
| Metrics that provide a quantitative measure of the level of service. | A target level or range of performance for the SLI over a period of time. | A formal, often contractual agreement between a service provider and its users that defines the expected performance and availability metrics, as well as penalties for not meeting them. |

---

# Error Budgets

---

## Components of Error Budgets

1. **Objective:** The desired success level, typically a percentage.
    - **Example:** 99.95%
2. **SLI (Service Level Indicator):** An evaluation used to differentiate the number of failed events.
    - **Example:** 95th percentile latency of API requests over 5 mins is < 100ms.
3. **Timeframe:** Introducing a recency bias to the SLI.
    - **Example:** Previous 28 days.

---

## Constructing an SLO

Given the example components, the SLO can be expressed as:

> "99.95% of the 95th percentile latency of API requests over 5 mins is < 100ms over the previous 28 days."

---

## Calculating the Error Budget

The Error Budget is derived from:
> Error Budget = 1 - Objective of the SLO

**Example Calculation:**
(1 - .9995 = .0005) or 0.05%

Given a 28-day timeframe, this translates to an error "budget" of:
> 20.16 minutes (.0005 * (28 * 24 * 60))

---

# What is Infrastructure as Code (IaC)?

Infrastructure as code (IaC) is a way to manage and provision infrastructure resources using configuration files and automation tools. 

![bg right:40% 90% fit](img/iac.drawio.png)

---

## IaC in SRE & DevOps: Key Benefits

1. **Automation & Consistency:** IaC automates provisioning, ensuring consistent infrastructure across environments.
2. **Version Control:** Infrastructure, like software code, can be versioned, allowing for easy rollbacks and history tracking.

---

## IaC in SRE & DevOps: Scalability & Collaboration

1. **Scalability:** With IaC, scaling infrastructure is as simple as adjusting parameters, facilitating easy growth.
2. **Collaboration:** Teams can review infrastructure changes like software code, fostering collaboration and preventing errors.

In SRE and DevOps, the drive is to minimize manual work and increase repeatability and reliability. IaC stands as a foundational component for these goals.

---

![bg left:40%](./img/devops.jpg)

# Dive into DevOps

---

DevOps promotes collaboration between development and operations teams through a set of practices and cultural philosophies.

---

## Key Concepts of DevOps

- **CI/CD:** Automatic build, test, and deploy processes.

---

- **Infrastructure as Code:** Automation of infrastructure tasks.

---

- **Feedback Loops:** Quick detection and resolution of issues.

---

- **Collaborative Culture:** Breaking silos and shared responsibilities.

---

![bg left:40%](./img/platform.jpg)

# Exploring Platform Engineering

---

Platform Engineering involves building and managing scalable platforms for deploying applications and services.

---

## Key Concepts of Platform Engineering

- **Self-service Platforms:** Empowering developers to deploy and scale.

---

- **Abstract Complexity:** Simplifying infrastructure complexities for developers.

---

- **Microservices & Containers:** Using architectures like Kubernetes.

---

- **Scaling & Performance:** Managing large-scale demands and optimizing resources.

---

## Conclusion

---

SRE, DevOps, and Platform Engineering intersect at ensuring efficient and reliable software delivery and operation.

---

**Key Takeaways**

- **Collaboration & Automation:** Central to all disciplines.
- **Continuous Improvement:** Better processes and tools.
- **End-to-end Responsibility:** From code to operation.

