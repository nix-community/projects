# Sovereign Tech Fund / Nixpkgs Security Story

## What open source infrastructure component would you like to contribute to? Please provide more details.

[Nix](https://nix.dev/) is an open source build system, configuration management system, and mechanism for deploying software, focused on reproducibility. It is the basis of an ecosystem of exceptionally powerful tools – including Nixpkgs, [the largest, most up-to-date software repository in the world](https://repology.org/repositories/graphs), and NixOS, a Linux distribution that can be configured fully declaratively, with unmatched flexibility. For its proponents, Nix embodies technology sovereignty. It is leveraged and relied upon by computer enthusiasts, professionals, and organisations who recognise its value for all steps in the software development lifecycle.

This project’s goal is to systematically leverage the very core of the Nix ecosystem: the Nix store. The store implements the [purely functional software deployment model](https://edolstra.github.io/pubs/phd-thesis.pdf): It deals with files in a file system like a modern computer program deals with objects in memory, by ensuring [referential integrity](https://en.m.wikipedia.org/wiki/Referential_integrity), and enabling garbage collection and transparent caching. It allows handling software builds like pure (that is, side-effect-free) computations in a declarative programming 
language, offering powerful building blocks for a sound security ecosystem.

Nixpkgs is the largest software collection in existence, at the time of writing, totaling more than 89.1K of packages according to [Repology](), it does this by absorbing various software ecosystems such as Python packages, Node.js packages and more. As a result, nixpkgs is an very interesting security target, we would like to address three of them: bootstrapping nixpkgs from very small auditable binaries, tracking and addressing security on the whole ecosystem in an efficient fashion and finally ensuring a proper boot security chain for NixOS, our Nix and Nixpkgs based Linux distribution.

## Why is this technology critical? Please explain to us the relevance of this technology.

This year Nix has seen its 20th anniversary. We estimate the community to consist of 100 mostly volunteer developers, 2 000 contributors, more than 15 000 active users, and 100 companies using and relying on Nix. [Recent social media activity](https://www.youtube.com/watch?v=fuWPuJZ9NcU) reaches on the order of 100 000 people. The Nix ecosystem is on an [exponential growth trajectory](https://ossinsight.io/analyze/NixOS/nixpkgs#overview) in terms of user adoption and development activity at the periphery.

Nix has the potential to become a default in the software development tool stack, by drastically reducing the time required to start working on software development projects – written in any language – and the cost of maintaining and sharing build setups and development environments. These can build on top of Nixpkgs, which today supplies the largest collection of free software in existence ready for use. Packages and services can be configured and deployed through NixOS more flexibly, reliably, efficiently than with any comparable tool. The Nix ecosystem can enable almost indefinite reproducibility of builds and configurations: [Nix and legacy enterprise software development: an unlikely match made in heaven](https://talks.nixcon.org/nixcon-2022/talk/QQPBFW/).

It serves as the platform accelerating and keeping usable countless software experiments that would otherwise be intractable or have long become inaccessible as their environments grow past them.

Moreover, the public [Nix binary cache](http://cache.nixos.org/) provides operational software artefacts from more than a decade back, some of which cannot be obtained otherwise any more.

In short, Nix reduces the global cost of software production and long-term use by a tangible amount.

Now this is said, bringing the security posture of nixpkgs to another level is crucial to improve the whole ecosystem and provide defense in depths to measures even if we cannot control all the package's contents.

Here, we focus on reducing our reliance on foreign binaries to recompile nixpkgs from scratch and improve our trust following [Reflections on Trusting the Trust](https://www.cs.cmu.edu/~rdriley/487/papers/Thompson_1984_ReflectionsonTrustingTrust.pdf), ensuring we are able to trust what we boot exploiting the existing security platform and finally trusting that we always strive to use the most up-to-date, patched software whenever it is available in a sustainable fashion.

## Please provide a brief overview over your project’s dependencies, including your own dependencies and projects that rely on your technology.

Bootstrapping nixpkgs is all about reducing dependencies but this is reliant on projects like [stage0-posix](https://github.com/oriansj/stage0-posix) and a Linux kernel which offers many necessary pieces to get a C compiler environment where you can continue the bootstrapping chain of nixpkgs.

Early boot security is an initiative worked with the [UAPI group](https://github.com/orgs/uapi-group/) formed by Linux distribution developers, from which NixOS is part of.
UEFI is also another important piece of the puzzle, but one we are dependent in a modular fashion and we could replace it, an interesting example in community is [OwnerBoot](https://sr.ht/~amjoseph/ownerboot/), a completely "user-owned" boot chain leveraging [Coreboot](https://www.coreboot.org/) and [LinuxBoot](https://www.linuxboot.org/) which completely replaces UEFI. Finally, most, if not all, of the software is developed in the [Rust programming language](https://www.rust-lang.org/), known for safe low-level programming, with excellent UEFI support.

As for tracking security issues, we would use web technologies such as Django / Python and we will be able to generate full software bill of materials of the project during its lifetime because Nix can provide them out of the box.

Nixpkgs would depend on all these technologies, sometimes in an optional way, e.g. bootstrapping or boot security.

A selection of projects and companies depending on Nix, Nixpkgs, or NixOS:

- [Replit](https://blog.replit.com/nix)
- [Shopify](https://shopify.engineering/shipit-presents-how-shopify-uses-nix)
- [Cachix](https://www.cachix.org/)
- [flox](https://floxdev.com/)
- [INRIA’s Grid’5000 computing cluster](https://nix-tutorial.gitlabpages.inria.fr/nix-tutorial/index.html)
- [Haskell Stack](https://docs.haskellstack.org/en/stable/nix_integration/)
- [The European Commission’s IT department](https://www.youtube.com/watch?v=I7wdcJ3YhoU)
- Various [scientific projects](https://www.youtube.com/watch?v=SjjEDTccpQA), such as in [high-performance computing](https://github.com/freuk/awesome-nix-hpc)
- A plethora of [community projects around Nix](https://github.com/nix-community/)

## Who benefits from this technology and the improvements or contributions? Which target groups does your project address (who are its users?) and how do they benefit from the funding (directly and indirectly)?

Tools in the Nix ecosystem are primarily suited to professional software developers and computer enthusiasts (many of which are students), but are also known to support scientific work, and are used as a foundational technology and force multiplier in a multitude of organisations and commercial enterprises.

Usually, a Linux distribution can be tailored to a specific usecase or can be offered in variants, e.g. desktop, server, immutable. In the case of NixOS and Nixpkgs, there is no real choice to take as Nixpkgs is a recipe to build Nix-based Linux distributions.

We draw from success stories like Intel's one with processors, i.e. the fact that a processor should contain all features, be it for server or clients, in the same hardware, empowering developers to build on the top of those enterprise features and create new unexpected usecases.

In nixpkgs, everything is possible and there is no "server" or "client" orientation, our users even run nixpkgs on routers and some dream of running it on switch, the idea of having a single source of software collection as a meta Linux distribution is achieved by Nix, the package manager, the orchestrator of all these pieces to form a runnable system.

Take for example [Liminix](https://nlnet.nl/project/Liminix/) which provides a NixOS alternative for routers with low resource capabilities.

Therefore, improving Nixpkgs is improving all of that at the same time: improving security tracking, boot chains and finally bootstrapping contributes to strengthening large and various ecosystems which all share this single common point: they derive their packages, therefore systems, from nixpkgs.

The NLnet Foundation is partnering with the NixOS Foundation to leverage Nix’s capabilities for providing sustainably accessible software under the umbrella of the Next Generation Internet initiative of the European Commission. It also funds numerous projects building on top of Nix to provide better tools for FOSS developers. Improving security of Nixpkgs on those areas would open up a way for those projects to build more advanced primitives and solutions to tackle state of the art problems in the industry.

## How are decisions regarding this technology’s development made? Please describe the project’s governance model.

Individuals and loosely organised contributor or maintainer teams review each other’s work and discuss technical decisions in public. Despite the principal author technically being a BDFL for Nix, the package manager, there are only weak and implicit power structures that are largely centered around demonstrated achievements, and decisions largely are based on technical merit as judged by those involved.

Self-organised formal [community teams](https://nixos.org/community/#governance-teams) take responsibility for maintaining code in their areas of expertise, and have a more formal communication and permission structure. Otherwise, apart from more regular activity, they operate just like any other group of contributors.

Nix itself is currently [maintained by a team of six people](https://github.com/NixOS/nix/tree/master/maintainers#members) including principal author, who meet twice a week to discuss technical decisions and review contributions.

Ecosystem-wide technical decisions are negotiated in an [RFC process](https://github.com/NixOS/rfcs/).

The NixOS Foundation mainly ensures funding for critical assets such as the binary cache, manages permissions in the GitHub organisation, and facilitates community activities. The Foundation board as a legal entity is not involved in technical decisions.

Project governance has immensely gained in structure lately: In the past year, four of the eleven currently active community teams were formed, the NixOS Foundation board was restructured, and there exist plans for setting up paid support functions to ensure continued operations.

## How does this project handle security risks? Are there policies, procedures, or tools in place to minimize the introduction of vulnerabilities or undesired contributions?

There exists a [security team](https://nixos.org/community/teams/security.html) and two infrastructure team: a ["build" infrastructure](https://nixos.org/community/teams/infrastructure.html) and "non-build" infrastructure. Build infrastructure tends to critical assets, including the precious security keys which signs nixpkgs software, whereas the recently formed "non-build" infrastructure tends to any non-critical assets but still important for making any Nix community work easier, e.g. end to end encrypted password managers.
There is also a [Nix community](...) entity which serves as a staging area for any Nix ecosystem initiative before promoting it to an official Nix ecosystem project, once they mature enough.

[Security-relevant issues and pull-requests](https://github.com/NixOS/nixpkgs/labels/1.severity%3A%20security) are tagged by their maintainers, security team and any contributor who deem there is ground to think that a PR has security contents, e.g. in case where CVEs are not used.

In nixpkgs, there are two big families of software: package that is depending upon in nixpkgs and "leaf" packages.

The first has subfamilies depending on the importance of the package, some are C libraries, very critical for any kind of software, some are geospatial Python dependencies, critical only for the geospatial ecosystem.

The second can be all sorts of ad-hoc software leveraging the rich ecosystem of dependencies already present in nixpkgs.

There are multiple attack surfaces when it comes to nixpkgs:

(1) Authenticating sources and ensuring we package software from trusted source: not all upstreams have a signing infrastructure and publish signed tarballs, our system is able to secure even non-HTTPS sources by pinning the hash of their sources.
(2) Community should re-validate that upstream is in good health and not jeopardized: we confirmed our ability to do this in multiple times when it comes to the various Minecraft launchers incidents in the past leading to multiple forks.
(3) Tarballs can exploit vulnerable code in our decompressor, we already apply defense in depth to ensure we limit the blast radius but we can go much further and completely sandbox / restrain the capabilities of our decompressors while pushing for more memory-safe decompressors. The same applies for any source fetching software, like Git or Mercurial.
(4) Backdooring attempts to ship innocent updates with hidden payloads can happen, like with the Linux kernel, systemd or any open source project. Our code review system will usually thwarts this as long as (1) is honored, but sophisticated attacks can be mounted with long-term covert operations against the repository by crafting virtual identities manipulated by the same rogue entity, those attacks can only be mitigated by pushing for more and more defense in depths measures like we do with systemd hardening and hardening of our software by default (via compiler flags).

The first family of software can sometimes have ownership structures (CODEOWNERs) where it is expected to wait for their approval before getting a change, for example, this is the case for systemd and low-level parts of nixpkgs (compilers) in general.

The second family is much more prone to the full attack surface because of the discoverability problem of finding a contributor having domain expertise on that leaf package which takes a bit of time before happening, therefore, code reviews are closer to courtesy reviews in those situations.

In nixpkgs, newer processes are constantly being discussed regarding this and [a committer RFC is in discussion](...) to clarify a mutual understanding of the roles and expectations on a committer in nixpkgs.

Different components have different ownership structures. For Nix itself, only maintainers have write access, and only the principal author can publish releases. Nixpkgs and NixOS have a much broader committer community with largely implicit rules. There is a high degree of social trust involved, and active developers and maintainers, while culturally and geographically diverse, usually have ongoing working relationships marked by diligent reviews and critical discussions.

## How will you address the challenge described? Give an overview of your work and why it is significant, specifically addressing the challenge. Explain what the field will learn from your proposed work and how it contributes to the long-term sustainability of the technology.

[0. Merged proposal]

Overall, this proposal is about improving the entire production of the FOSS software collection that is nixpkgs, a very large one and depended upon.

Each item contributes to fundamental hardening measures and aims to close class of vulnerabilities against this software collection, e.g. bootstrapping reduces our surface of foreign opaque binaries to recompile nixpkgs from zero, security tracker gives us the ability to triage through the large firehose of security vulnerabilities and be more efficient about security patching, boot security is about offering strong trust primitives for machines that can be development, continuous integration or anything.

We will express the significance in matters of "what would a win look like".

More precisely:

A security team usually provides many automation for security team, maintainers and end users:

- Triaging interface to ACK/mark as irrelevant/etc. vulnerabilities as they come from many pipelines, loosely matched with nixpkgs
- Monitoring the delivery pipeline (hydra.nixos.org) to notify users or alert security team when all non-EOL distribution channels receive security updates
- Statistics and tracking over time of vulnerabilities for research and organizational improvement

In the past, Archlinux's security tracker was considered for reuse in NixOS but it is very old and tailored to Archlinux needs.

Here, we propose to write a new security tracker with NixOS in mind, but in a generic way, which can be reused, not only for nixpkgs but any overlay of nixpkgs and can be deployed in organisations and for nixpkgs needs.

Our main challenge is to tackle the information overload generated by the ingestion process from many security feeds, we would tackle this by providing powerful filtering capabilities linking all the available metadata from Repology and nixpkgs for example.

A security.nixos.org prototype usable by Security Team would:

- Reduce the intense churn on security team and foster sustainability for FOSS volunteers
- Improve security posture of nixpkgs, especially for hard to track channels, e.g. "soon to be end of life" NixOS releases
- Make expectations to users transparent about "when will this security vulnerability will be patched in my system" and inform them about their options, e.g. [grafting](https://guix.gnu.org/manual/en/html_node/Security-Updates.html) (`system.replaceRuntimeDependencies`) where long time before delivery are predicted based on existing data.

As for boot security, NixOS recently acquired [a form of user-owned Secure Boot](https://github.com/nix-community/lanzaboote) as part of [a NLnet grant](https://nlnet.nl/project/NixOS-UEFI/).

As of now, Secure Boot in nixpkgs is slowly being upstreamed as part of https://github.com/NixOS/nixpkgs/pull/231951 but the Secure Boot ecosystem is still in its infancy with systemd having a lot of features which are not necessarily completely all wired up in Linux distributions.

The next stage after Secure Boot is to have measured boot which is the final piece to have a reasonable form of security in the boot of a Linux distribution.

To achieve this, one can leverage `systemd-cryptenroll` tooling to tie various entities to cryptographic entities in TPM2s.

The problem is that systemd semantics are not totally aligned with NixOS rollback capabilities and some footwork upstream has to be finished:

- https://github.com/systemd/systemd/pull/28057
- https://github.com/systemd/systemd/pull/28070

After this work, NixOS can boot with:

(1) UEFI Secure Boot with user-owned keys or MSFT-backed key infrastructure via shim
(2) Key storage can be secure with a HSM or similar hardware token as long as it is supported by PKCS#7 standards, Nitrokey will have a special emphasis as it is a mature, open hardware, affordable HSM product

And NixOS can be deployed in situations where:

(1) It is desirable to lock down completely the runnable binaries, e.g. only the Nix store is allowed to execute binaries.
(2) It is desirable to authenticate and verify for the integrity of the Nix store via a signed boot file containing the root hash (of the Merkle tree)
(3) Reduce maximally the presence of "interpreters", e.g. Python, Bash, Perl, Nix, any binary which can enable escape from the security model and offer further exploitation measures to an adversary
(4) Updates are mission-critical and recovery must be assured in case of failed upgrades, e.g. A/B-style layouts like Android, embedded systems, etc.

providing one of the most secure and reliable way to deploy software in production.

Finally, [bootstrap]


### What the field will learn from our work

Nix puts forward a unique (indeed, we claim, revolutionary) approach to software development to begin with. One can argue that it is still somewhat obscured for various reasons, and one of them is that the core mechanisms are hidden away as an implementation detail.

Clarifying concepts by formalising and documenting interfaces would enable others to build on top of, reimplement, or innovate over what Nix has to offer, and help spread its ideas beyond the currently entrenched but limited notion of a package manager and beyond the particular implementation angle the Nix ecosystem has taken.

Furthermore, in all security areas we presented, most of our work is reusable and is reused or we are reusing other Linux distribution works, this is all part of a circuit where we share and we aim to do even better by abstracting what we produce as much as possible to offer it "on the shelf".

### How our work will contribute to sustainability of Nix, the Nix ecosystem, and FOSS more generally

Depending on the mentioned pieces will provide developer force from Nixpkgs to those upstream projects, providing maintenance and improvements.

Furthermore, the security tracker will serve as a sustainability platform regarding security responses across all Nixpkgs and can also be reused for derivatives of Nixpkgs.

## How will you accomplish the work? Please provide a list of deliverables with associated effort and cost of each deliverable.

For the boot security chain, here is the list of deliverables:

- [ ] Preparatory fundamental upstream features (systemd and more): 4w, 10K EUR.
- [ ] NixOS's default UEFI Secure Boot images via shim and shim-review: 4w, 10K EUR (*)
- [ ] NixOS RFC "Bootspec v2": 2w, 4K EUR
- [ ] Lanzaboote and TPM2: 4w, 10K EUR
- [ ] Safe updates (A/B schemas) in NixOS with systemd-boot: 2w, 5K EUR
- [ ] Safe Nix store via integrity techniques (*-verity): 4w, 10K EUR
- [ ] Safe NixOS via maximal reduction of attack surface through open interpreters: 4w, 10K EUR.
- Total: 59K EUR.

(*) This is dependent on the [shim-review project](https://github.com/rhboot/shim-review) owners to accept our application.

Explaination:

In order to make many of those features a stable and reliable reality, some work has to be done upstream
which will benefit the whole ecosystem and community and show the talent and expertise of our ecosystem.

Then, a lot of work would be performed in parallel via lanzaboote maintainers
but new developers who joined the project because they were seduced in the value proposition of combining NixOS and those features.

Because this work is particularly low-level and difficult, those rates are a minimum for the quality standards we set in nixpkgs,
it will probably entail many back'n'forth with UEFI ecosystem libraries in Rust as this is the tool of choice for
the development of our tools.

Finally, the last three points enable NixOS as, what we call, an "appliance operating system", that is, a highly-secure and locked-down
deployment of NixOS in the field, e.g. Internet of Things, application servers, where upgrades can only be performed by replacing
completely the whole system, in a safe way supporting safe rollbacks in case of failed upgrades but not supporting arbitrary
downgrades to vulnerable versions. We would also aim to remove any potential "bugdoors", be it a Python interpreter which can run
arbitrary Python code which are contained in NixOS for early boot due to flexibility and simplicity of the build story.


- [ ] Web service scaffholding (architecture, structure, testing, packaging, deployment) and core features: APIs & ingesting (3w, 10K EUR)
- [ ] [label-tracker](https://git.eno.space/label-tracker.git/) integration and improvements (2w, 5K EUR)
- [ ] User story "Security team" work (2w, 5K EUR): filtering, triaging, generating advisories, linking metadata
- [ ] User story "Maintainer" work (3w, 5K EUR): assisting security team, processing their own software, validating/participating, automation for PRs (bump, backport, mark EOL/vulnerable)
- [ ] User story "End-user" work (2w, 5K EUR): receiving data about the current security story of a release, subscribing to security updates for a release, various APIs to reuse alerting, open data and exports

- Total: 30K EUR

Explaination:

The working mode we envision is a strong web developer with extensive Nix experience developing a reusable high standard platform with
maintenance in mind, i.e. end to end testing, etc, which has a slight amount of flexibility to be reused for similar Linux distributions, e.g. Guix.

We decide to split the work in 3 "big milestones" or "target goals" under the User story item where we want the platform to be usable and acceptable for that target audience, i.e. security team, maintainers and end-users, each phase comes with its lots of features and should work closely with the target audience to ensure we build something of use to that particular audience on the basis of UX/UI research methods. Each phase includes a user discovery part and a development part, user discovery can be performed asynchronously in some situations to improve the velocity.

Label tracker is an important piece of the puzzle for end-users as a technical API for untangling the complicated relations with the large continuous integration of NixOS, our Git repositories, our channels to answer non-trivial questions like "Is this PR in my distribution channel?" or "When is this PR expected to land in my distribution channel?" so we can depend critically on it, those improvements can include performance work, scaling up the infrastructure to be a common good in the Nix community open to everyone.

---

Overall, Nix maintainers essentially have to buy their employers’ time or take compensation that can compete with other engagements; known contributors who could do the bulk of the work are in a similar situation or otherwise would need substantial time for onboarding. Therefore we have to assume consultancy rates to be able to keep to the time frame, with the option to trade budget for velocity to some extent.

We expect multiple contributors to work in parallel where possible.

## Describe your relationship to the maintainers of this technology. Are you yourself the maintainer? Do they know you plan to do this work and do they support it? Please tell us more about how you obtained their support and how you plan to work together to make sure your contributions are accepted.

[1. Security tracker]

I am not part of [security team](), but I am [contributor](https://github.com/NixOS/nixpkgs/pulls?q=is%3Apr+author%3ARaitoBezarius+label%3A%221.severity%3A+security%22+is%3Aclosed) and [reviewer of security fixes](https://github.com/NixOS/nixpkgs/pulls?q=is%3Apr+reviewed-by%3ARaitoBezarius+label%3A%221.severity%3A+security%22+is%3Aclosed+) in nixpkgs in critical software.
and I am the [current release manager of NixOS](https://nixos.org/community/teams/nixos-release.html) and released NixOS 23.05, I had to deal with [Node.js]() and [OpenSSL]() [end of life status]()
and offers non-bumpy upgrades paths to all our users out there. I am familiar with the challenges of the security team
as I worked on providing RSS feeds in [pr-tracker](https://git.qyliss.net/pr-tracker) a tracker of "when my PR is in some Nixpkgs channel", discovered [label-tracker](https://git.eno.space/label-tracker.git/)
which offers this solution for security updates.

I coordinated the disclosure in the [NixOS Graphical Installer vulnerability](https://github.com/NixOS/calamares-nixos-extensions/security/advisories/GHSA-3rvf-24q2-24ww) and am working on automatic remediation
at early boot time to fix it.

Finally, I am in close touch with the security team and we discussed many times the need for such a feature, such a contribution would
be very welcomed and its deployment / management could be offloaded to the [newly formed NixOS infrastructure team](https://github.com/NixOS/foundation/issues/79) which I also interact
with.

[2. Boot story]

I am part of the maintainers of [lanzaboote](https://github.com/nix-community/lanzaboote), one of the most complete UEFI Secure Boot implementation in NixOS, widely used in the NixOS community.
I am also one of the shepherd of [the Bootspec v1 RFC](https://github.com/NixOS/rfcs/pull/125), author of [an RFC on how to bring UEFI to legacy users](https://github.com/NixOS/rfcs/pull/154) and working towards Bootspec v2.

I also re-implemented most of `systemd-stub` in lanzaboote in Rust, as part of the [reimplementation proposal](https://github.com/nix-community/lanzaboote/issues/94).

Finally, I work with systemd in bringing powerful primitives for every Linux distribution which would enable lanzaboote and NixOS
to reuse upstream primitives directly: see [systemd#28057](https://github.com/systemd/systemd/pull/28057), [systemd#28070](https://github.com/systemd/systemd/pull/28070) for some examples.

For the last years, we discussed most of the controversial contents with upstreams, especially systemd, and we are now in a state where
we believe to have a consensual path forward to obtain a fully integrated vision encompassing Linux kernel, systemd and NixOS.

Discussion about "the next steps" of lanzaboote have been discussed all the time and we have users asking more and more of that now that UEFI Secure Boot is easy to achieve.

[3. Bootstrapping]

Total so far: 89K EUR.

Preparations for the grant applications were [announced in the community forum](https://discourse.nixos.org/t/german-federal-funding-for-foss-development/29036/4).

We plan to follow our established routine to review and merge contributions in nixpkgs.
