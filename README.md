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

**That said, here are the high-level diffentiators to consider when comparing the two runner types:**

- **Security.** Zero trust microsegmentation and SLSA Level 3 build isolation comes out-of-the-box with GHRs. For SHRs, customers must design, implement, and monitor a similar network isolation architecture themselves. 
- **Labor costs.** GHRs feature minimal upfront and ongoing administrative labor costs. SHRs require extensive upfront and ongoing labor costs.
- **Turnkey utilization.** When starting off, GHRs can be used almost immediately in turnkey fashion. With SHRs, customers must first go through a security-validated implementation process.
- **Pricing.** Because GHRs are a fully-managed SaaS service, customers should expect to pay more per-minute for compute utilized than they would do with SHRs. However, customers will pay notably more in labor costs associated to implementing and managing SHRs in ongoing fashion.
- **Configuration flexibility.** While GHRs give customers a great extent of flexibility in configuring the runner environment, SHRs will ultimately provide customers with a greater degree of flexibility. That said, GHRs provide the flexibility needed to meet the requirements of most CI/CD use cases. Where GHRs cannot meet those requirements, SHRs provide an alternative option for consideration.

# Intro to GitHub-Hosted Runners (GHRs)

As mentioned above, GHRs are ephemeral, network-isolated VMs that GitHub provides and manages on behalf of customers. They can be booted from GitHub-provided VM images OR booted from customer-provided custom VM images and _always_ feature a clean image for every job run. 

Each GHR is based on a select VM SKU chosen by the customer from the variety of SKUs featured in the GHR compute fleet. This fleet of SKUs features the following:

- Multiple OSes (Linux, Windows Server and Desktop, macOS)
- Multiple hardware types (x64, arm64)
- A broad range of machine sizes, from 2-cores up to 96 cores
- GPU-enabled machines (more coming soon)

More SKUs are tentatively slated to join the fleet in CY2025, namely M2 Pros, M4 Pros, more GPU-enabled machines, memory- and storage-optimized machines, and (potentially) a new lightweight compute SKU option for jobs that run in under 1 minute. Please NOTE: New SKU plans are always subject to change.

As of May 2025, here (see the graphic below) is the current state of GitHub's GHR fleet:

<img width="1006" alt="Screenshot 2025-05-21 at 6 07 25 PM" src="https://github.com/user-attachments/assets/3b8ba78f-ae18-44ad-87de-0ec69ea893c4" />

# Why NOT GitHub-Hosted Runners (GHRs)?

If GHRs can meet or surpass your requirements in regard to security (first and foremost), performance, availability, total cost of ownership, and ease of troubleshooting, why would you NOT choose to utilize them? 

That said, based on the investments GitHub has made in GHRs over the past several years and the feedback we've gathered from our customers about their experiences with both GHRs and SHRs, **GitHub encourages customers to adopt a GHR-first mentality when making decisions about whether to use GHRs or SHRs**. 

Our reason for doing so stems from our demonstrated ability to indeed meet (and even surpass) customer requirements in each of the the five areas of concern mentioned above for most CI/CD use cases. The following graphic helps explain our reasoning in more detail:

<img width="1006" alt="Screenshot 2025-05-21 at 6 33 46 PM" src="https://github.com/user-attachments/assets/6f18f165-0a6a-4b8a-aed2-77ae3aa0911a" />

I'll unpack the GHR story in each of these areas of concern in the text that follows. 👇

**Security and GHRs**


