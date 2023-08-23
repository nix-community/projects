# Sovereign Tech Fund / Migrations for NixOS Modules

# Describe your project in a sentence.

The project fills a crucial conceptual gap in NixOS by introducing a migration infrastructure for seamless upgrades and downgrades of stateful services, aligning imperative steps with the declarative and immutable nature of NixOS configurations.

## Describe your project more in-depth. Why is it critical?

Nix is an open-source build system, configuration management system, and mechanism for deploying software focused on reproducibility.
It is the basis of an ecosystem of exceptionally powerful tools – including Nixpkgs, the largest, most up-to-date software repository in the world, and NixOS, a Linux distribution that can be configured fully declaratively with unmatched flexibility.
For its proponents, Nix embodies technology sovereignty.
It is leveraged and relied upon by computer enthusiasts, professionals, and organizations who recognize its value for all steps in the software development lifecycle.

This project is crucial for software developers, and in particular for enterprises, who rely on open source software for running services that store data.
Currently, the immutable nature of NixOS poses significant challenges for upgrading such software when the data formats change in between versions, causing frustration and difficulties, oftentimes making upgrades practically infeasible without either losing data or sticking to the originally configured version of the software in question forever.
The project addresses this by introducing a migration infrastructure that fills the conceptual gap between immutable configuration and stateful services and allows for seamless upgrades and downgrades, unlocking the full potential of the declarative paradigm.

The significance extends beyond immediate pain points.
The migration infrastructure allows software experts to rely on NixOS for hosting their services in the long term, reaping all the benefits of the Nix ecosystem without the aforementioned risks.
Since the project will provide turnkey solutions for migrating between versions of open source services on top of just implementing the mechanism, as an outcome it will even further reduce global software develoment costs and lower the barrier to entry into competitive markets for young professionals and encumbent enterprises.
Additionally, it will increase the reach of the software projects that are supported in NixOS out of the box.

> https://github.com/NixOS/rfcs/pull/155

# Please provide a brief overview over your project’s own dependencies.

This project is an infrastructure addition to NixOS and depends exclusively on the code in the Nixpkgs repository.
The projects that rely on stateful services in NixOS configuration are numerous and include all enterprise deployments of NixOS as well as open-source projects.

# Which target groups does your project address (who are its users?) and how do they benefit from the funding (directly and indirectly)?

This infrastructure serves everyone who uses stateful services provided by NixOS, including many companies such as Replit, Hashicorp, Flying Circus, and others.
It is relevent both for verticals ranging from Robotics to Bioinformatics and Blockchain, but also start-ups as well as the numerous self-hostable open source projects supported through the NGI program of the European Commission.

This project is a significant effort and requires the establishment of migrations for numerous complex stateful services already available in Nixpkgs.
Funding is absolutely necessary to undertake an effort of this scale.
For example, in addition to the introduction of the infrastructure abstractly, we intend to provide working migrations for the following services:

* GitLab
* Postgresql
* Jira
* MySQL
* Kibana
* LDAP
* MongoDB
* Graphana
* Neo4J
* Jupyter
* Jenkins
* CouchDB
* Consul
* And others...

Each requires new documentation, and testing and quality assurance efforts

# How was the work on the project made possible so far (structurally, financially, including volunteer work)? If applicable, list others sources of funding that you applied for and/or received.

Work on this project has yet to start beyond the RFC and endorsements and collaboration from the NixOS Foundation and NixOS maintainers.

# What are possible alternatives to your project and how does your project compare to them? (optional)

None exist at this time within Nix.
This project is innovative and would be the first to provide migrations for immutable configurations of stateful services.

However, the Guix project has applied for the Sovereign Tech Fund challenges to implement their own version of a similar feature, which would be incompatible with NixOS due to the differences between Nix and Guix.
