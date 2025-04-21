# Securing global software distribution with Nixpkgs

1) Describe the technology this effort will support. (max 5 sentences)

   Nix is a software deployment system enabling reproducible builds and declarations of entire system configurations.
   It powers Nixpkgs, the world's largest, most up-to-date open-source package repository, and NixOS, a declaratively configured Linux distribution - forming critical infrastructure that numerous organizations rely on for their software supply chain.
   With its growing adoption, the ecosystem faces increasing security challenges around package distribution, vulnerability management, supply chain integrity, and update turnaround time.

2) Where is this technology being used? Why is it relevant and critical? How does this technology serve the public interest? (max 5 sentences)

   Nix and NixOS are used by the European Commission's IT department, scientific computing clusters, and companies providing essential public services.
   They enable secure and reproducible software deployment for critical infrastructure, scientific research, and public services.
   The technology serves the public interest by providing a reliable foundation for long-term maintenance of systems that citizens depend on daily.

   Currently our continuous integration infrastructure is facing a crisis:
   While we have stopgap measures for the imminent loss of substantial donated computing power at the end of 2024 (Equinix Metal is discontinued), that solution leaves us dependent on a single organisation (GitHub, where the Nixpkgs repository already operates far outside the usual boundaries for the free tier).
   This takes a toll on our volunteer infrastructure maintainers taking care of the emergency migration, and bears the risk of disrupting the work of hundreds of developers being able to efficiently review and test each other's contributions in order to keep the system operational and secure.

3) What are the problems the proposed work is trying to address? What activities do you propose and how do they address the problems described? How do those activities fit into STFʼs mission? (max 5-10 sentences or 2 paragraphs)

   Problems:
   
   - The growing popularity of Nix has made it an attractive target for supply chain attacks
   - Security vulnerabilities at Nixpkgs' scale are challenging to handle efficiently
   - The system lacks robust mechanisms for verifying security properties and deploying patches quickly
   - Current infrastructure relies heavily on root privileges and lacks modern security features
   
   Proposed activities:
   
   - Implement a rootless Nix daemon in NixOS
   - Harden and accelerate CI checks, and enhance reproducibility verification
   - Increase independence from large donors in our computing infrastructure
   - Remove script-based system activation for improved security
   
   These foundational security improvements align with STF's mission by strengthening critical open-source infrastructure that public institutions and essential services depend on.

4) Who is going to be performing the work and how are they qualified to do so? (max 5 sentences)

   The work will be implemented by authors or current maintainers of the subsystems in question, with tasks potentially distributed to experienced contributors where appropriate.
   These maintainers are typically senior software developers with years of experience in their specific areas of interest within the Nix ecosystem, all of whom have contributed thousands of code changes in the past.

   Concretely: [@Ericson2314](https://github.com/ericson2314/), [@roberth](https://github.com/roberth), [@Mic92](https://github.com/Mic92) (maintainers of Nix and Nixpkgs core components), [@dasJ](https://github.com/dasJ/), [@JulienMalka](https://github.com/JulienMalka/), (CI and infrastructure), [@raboof](https://github.com/raboof/), [@nikstur](https://github.com/nikstur/) (boot and supply chain security).

5) How is the technology maintained or governed? Is there a community behind the technology and do they approve of the work? (max 5 sentences)

   The Nix ecosystem is currently maintained by ca. 100 core volunteers and ca. 800 monthly contributors, and was built by more than 3 000 people over the past 20 years.
   Most work is done by volunteers, with some maintainers contributing through their jobs.
   The non-profit Stichting NixOS Foundation serves as the legal entity backing the project; it organisationally supports critical activities and manages institutional partnerships.

   This proposal was developed collaboratively by long-time maintainers and contributors, who together represent the active community around core components of the Nix ecosystem and have strong backing:
   @Ericson2314 and @roberth have been elected to serve on the communityʼs [steering committee](https://github.com/NixOS/org/blob/main/doc/governance.md).

6) Describe the Milestones or Work Packages Using the Template below (max 5 sentences per milestone or work package, ideally not more than one a month and ideally not more than 10 milestones)

   - **Harden CI checks (35 000 EUR, 3 months)**

     Responsible: @multivac61, @Mic92

     FODs (fixed-output derivations) represent a significant security risk in the Nix ecosystem due to their unrestricted network access and only-once hash verification. The following measures aim to improve security of CI on public open source projects through controlled network access and reproducibility verification:

     - Build a FOD proxy that filters for accepted protocols
     - Build a tool that scans for FODs in Nixpkgs
     - Create verification system for checking consistency of FOD hashes and rebuilds
     - Integrate the above with the Nixpkgs CI pipeline

     **Delivery date:** Start + 3 months

     **Milestone hours:** 305

   - **Interpreter-less system activation (30 000 EUR, 3 months)**

     Responsible: @nikstur

     System interpreters are a critical attack vector (MITRE T1059) that allow arbitrary code execution once breached. For high-security and appliance deployments, completely removing these interpreters offers the strongest mitigation (M1042).

     - Replace bespoke scripts with generic functionality
     - Remove bash dependency on core packages or make it optional
     - Build custom compiled tools to replace scripts
     - Add configuration options and documentation to make this easy to use

     **Delivery date:** Start + 5 months

     **Milestone hours:** 300

   - **Increase sustainability of CI infrastructure (40 000 EUR, 4.5 months)**

     Responsible: @dasJ, @Conni2461

     Workloads for CI checks on pull requests are dispatched by a custom tool called ofborg. The resources to run the builds (equivalent to a over-the-counter price of 30 000 EUR/month) were sponsored until recently, and the arrangement ends in December 2024. To establish a long-term solution and replace current improvised measures, to reduce dependence on a single sponsor, and to ease transitions of compute sponsoring in the future, we want to extend the architecture to allow for a community-driven, scalable approach of donating build capacity.

     - Evaluate security considerations
     - Establish a process for adding and removing externally managed nodes
     - Add observability tooling for the distributed setup
     - Add documentation for ofborg users and node sponsors
     - Set up a staging instance and provide options for local testing of ofborg Build a faster and more intuitive web interface

     **Delivery date:** Start + 6 months

     **Milestone hours:** 350

   - **Fix performance bottlenecks in our CI/CD (25 000 EUR, 2 months)**

     Responsible: @dasJ, @Conni2461

     Nixpkgs is growing faster than our infrastructure can keep up in terms of performance. This leads to a situation where CI checks become prohibitively expensive, incentivising maintainers to skip them altogether, or distribution of security updates gets delayed by days. The following improvements aim to address these bottlenecks with our CI system Hydra:

     - Investigate alternatives to maintaining Hydra and either refactor Hydra or implement an alternative setup
     - If Hydra is kept as the CI/CD solution:
         - Change the database schema to decrease access times
         - Rewrite the queue runner
         - Revisit and improve in-code and contributor documentation
     - Otherwise: Implement, test, optimise, and roll out the new setup

     **Delivery date:** Start + 8 months

     **Milestone hours:** 215

   - **Hash Collection Infrastructure (15 000 EUR, 2 months)**

     Responsible: @raboof @JulienMalka

     Nix-based builds are highly repeatable, but not necessarily bit-for-bit reproducible. They are mostly indexed by their inputs rather than outputs, which requires post-factum verification of build results.

     - Publish reproducibility reports for package collections corresponding to key artifacts, built from independently-verifiable build attestations from diverse sources
     - Provide tools for community members to create and upload independently-verifiable build attestations for package sets corresponding to key artifacts

     **Delivery date:** Start + 8 months

     **Milestone hours:** 130

   - **Investigate evaluator performance improvements (30 000 EUR, 4 months)**

     Responsible: @roberth

     The Nix evaluator is a critical component whose performance impacts all users of the ecosystem. Several optimization opportunities have been identified through parallel development efforts and usage at scale. The following tracks aim to improve evaluation performance across different usage patterns:

     - Set up benchmarks, port or implement known possible micro-optimizations
     - Develop a caching evaluator proxy with sandbox capabilities
     - Implement multi-evaluator support
     - Add a Nix language primitive for cached evaluation of an isolated expression

     **Delivery date:** Start + 10 months

     **Milestone hours:** 260

   - **Rootless Nix daemon (55 000 EUR, 4 months)**

     Responsible: @Ericson2314

     The Nix daemon currently runs with root privileges, creating unnecessary security risks. Reduce privileged processes while enabling store sharing between untrusting users.

     - Create configuration for limited rootless daemon running as NixOS-managed service
     - Implement multi-user garbage collection for rootless daemon
     - Implement separate per-user builders with shared store
     - Integrate secure Nix store on NixOS by implementing mixed-privilege store object lifecycle and local-overlay- store support

     **Delivery date:** Start + 11 months

     **Milestone hours:** 440

   This multifaceted development program is deliberately designed to avoid dependencies that would risk delays, and to simultaneously address the most important of the numerous challenges the system is currently facing.

   This project is intended to be run in the same fashion as the Contribute Back Challenge in 2023 and our NGI collaboration with NLnet: [@fricklerhandwerk](https://github.com/fricklerhandwerk) will assist with requirements specification, coordinate and validate the work, approve invoices, take care of public communication, and compile reports, such that participants, the NixOS Foundation, and the STF have a single point of contact for all administrative concerns.
