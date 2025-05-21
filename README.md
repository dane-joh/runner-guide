# GitHub-Hosted OR Self-Hosted Runners? 
Every triggered job in GitHub Actions is executed on a runner.

GitHub Actions offers two types of runners: **GitHub-Hosted Runners (GHRs)** and **Self-Hosted Runners (SHRs)**. What is the difference between the two?

**A GitHub-Hosted Runner (GHR) is:**

- Instantiated as a ephemeral, network-isolated VM (in Azure)
- Based on a GitHub-secured and managed VM image OR a customer-generated custom VM image
- Re-imaged with a clean VM image for _every_ job run
- Provisioned, warmed, auto-scaled, network-secured, monitored, and deprovisioned by GitHub (i.e. fully-managed)
- Billed per-minute (inclusive of compute, storage, networking and GitHub managed services)

**A Self-Hosted Runner (SHR), while similar to a GHR, differs from a GHR in these notable ways:**

- It may be instantiated as a full VM (Linux, Windows, macOS) OR, if auto-scaling is desired, may be instatiated as a container on Kubernetes (Linux only). Network isolation _must_ be properly configured and monitored by the customer. The customer deploys to whatever cloud or on-premises server platform they desire.
- It is typically based on a customer-generated and managed custom container/VM image.
- It is typically re-imaged for every job run. However, customers have the ability to persist the runner (which GitHub actively DISCOURAGES for security reasons).
- All implementation and ongoing management of a SHR to keep it secure, performant, available, cost-efficient, and easy to troubleshoot is the full responsibility of the customer.
- The compute is typically billed per-minute by the public cloud provider platform via which the runner is provisioned. Customers must also factor in additional storage and networking costs, cloud governance services costs supporting the implementation, and labor costs associated to managing the SHR deployment.

**When surveying the differences between the two types of runners, customers should acknowledge the following:**

- **Security.** Zero trust microsegmentation and SLSA Level 3 build isolation comes out-of-the-box with GHRs. For SHRs, customers must design, implement, and monitor a similar network isolation architecture themselves. 
- **Labor costs.** GHRs feature minimal upfront and ongoing administrative labor costs. SHRs require extensive upfront and ongoing labor costs.
- **Turnkey utilization.** When starting off, GHRs can be used almost immediately in turnkey fashion. With SHRs, customers must first go through a security-validated implementation process.
- **Pricing.** Because GHRs are a fully-managed SaaS service, customers should expect to pay more per-minute for compute utilized than they would do with SHRs. However, customers will pay notably more in labor costs associated to implementing and managing SHRs in ongoing fashion.
- **Configuration flexibility.** While GHRs give customers a great extent of flexibility in configuring the runner environment, SHRs will ultimately provide customers with a greater degree of flexibility. That said, GHRs provide the flexibility need to meet the requirements of most CI/CD use cases. Where GHRs cannot meet those requirements, SHRs provdie an optional path for runner hosting.
