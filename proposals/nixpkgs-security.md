# Sovereign Tech Fund / Nixpkgs Security Story

## What open source infrastructure component would you like to contribute to? Please provide more details.

[Nix](https://nix.dev/) is an open source build system, configuration management system, and mechanism for deploying software, focused on reproducibility.
It is the basis of an ecosystem of exceptionally powerful tools – including Nixpkgs, [the largest, most up-to-date software repository in the world](https://repology.org/repositories/graphs), and NixOS, a Linux distribution that can be configured fully declaratively, with unmatched flexibility.
For its proponents, Nix embodies technology sovereignty.
It is leveraged and relied upon by computer enthusiasts, professionals, and organisations who recognise its value for all steps in the software development lifecycle.

Nixpkgs is the largest software collection in existence, at the time of writing, totaling more than 85 000 of packages according to [Repology](https://repology.org/repository/nix_unstable).
It does this by encapsulating various software ecosystems such as [Python, Rust, Node.js, and more](https://nixos.org/manual/nixpkgs/unstable/#chap-language-support).
As a result, Nixpkgs is a valuable security target with a far reach, and we would like to address three aspects of it:

- Bootstrapping Nixpkgs from very small auditable binaries
- Tracking and addressing security on the whole ecosystem in an efficient fashion
- Ensuring a proper boot security chain for NixOS

## Why is this technology critical? Please explain to us the relevance of this technology.

This year Nix has seen its 20th anniversary.
We estimate the community to consist of 100 mostly volunteer developers, 2 000 contributors, more than 15 000 active users, and 100 companies using and relying on Nix.
[Recent social media activity](https://www.youtube.com/watch?v=fuWPuJZ9NcU) reaches on the order of 100 000 people.
The Nix ecosystem is on an [exponential growth trajectory](https://ossinsight.io/analyze/NixOS/nixpkgs#overview) in terms of user adoption and development activity at the periphery.

Nix has the potential to become a default in the software development tool stack, by drastically reducing the time required to start working on software development projects – written in any language – and the cost of maintaining and sharing build setups and development environments.
These can build on top of Nixpkgs, which today supplies the largest collection of free software in existence ready for use.
Packages and services can be configured and deployed through NixOS more flexibly, reliably, efficiently than with any comparable tool.
The Nix ecosystem can enable almost indefinite reproducibility of builds and configurations: [Nix and legacy enterprise software development: an unlikely match made in heaven](https://talks.nixcon.org/nixcon-2022/talk/QQPBFW/).

It serves as the platform accelerating and keeping usable countless software experiments that would otherwise be intractable or have long become inaccessible as their environments grow past them.

Moreover, the public [Nix binary cache](http://cache.nixos.org/) provides operational software artefacts from more than a decade back, some of which cannot be obtained otherwise any more.

In short, Nix reduces the global cost of software production and long-term use by a tangible amount.
Making it the trusted choice for reliable, up-to-date software will also make said software production dependable by default.

## Please provide a brief overview over your project’s dependencies, including your own dependencies and projects that rely on your technology.

Bootstrapping Nixpkgs is all about *reducing dependencies*, but this effort builds on top of the work of [stage0-posix](https://github.com/oriansj/stage0-posix) and [GNU Mes](https://www.gnu.org/software/mes/), which form our trusted minimal bootstrapping chain.

Early boot security is an initiative in collaboration with the [UAPI group](https://github.com/orgs/uapi-group/) formed by Linux distribution developers, which NixOS is a member of.
UEFI is another important piece of the puzzle, but one we depend on in a modular fashion, and we could replace it.
An interesting example in the Nix community is [OwnerBoot](https://sr.ht/~amjoseph/ownerboot/), a completely "user-owned" boot chain leveraging [Coreboot](https://www.coreboot.org/) and [LinuxBoot](https://www.linuxboot.org/) which completely replaces UEFI.
Finally, most, if not all, of the software is developed in the [Rust programming language](https://www.rust-lang.org/), known for safe low-level programming, with excellent UEFI support.

As for tracking security issues, we will use web technologies such as Django (Python) to track security issues and display the full software bill of materials (SBOM) generated from the project during its lifetime.

A selection of projects and companies depending on Nix, Nixpkgs, or NixOS:

- [Replit](https://blog.replit.com/nix)
- [Shopify](https://shopify.engineering/shipit-presents-how-shopify-uses-nix)
- [Cachix](https://www.cachix.org/)
- [flox](https://floxdev.com/)
- [INRIA’s Grid’5000 supercomputing cluster](https://nix-tutorial.gitlabpages.inria.fr/nix-tutorial/index.html)
- [Haskell Stack](https://docs.haskellstack.org/en/stable/nix_integration/)
- [The European Commission’s IT department](https://www.youtube.com/watch?v=I7wdcJ3YhoU)
- Various [scientific projects](https://www.youtube.com/watch?v=SjjEDTccpQA), such as in [high-performance computing](https://github.com/freuk/awesome-nix-hpc)
- A plethora of [community projects around Nix](https://github.com/nix-community/)

## Who benefits from this technology and the improvements or contributions? Which target groups does your project address (who are its users?) and how do they benefit from the funding (directly and indirectly)?

Tools in the Nix ecosystem are primarily suited to professional software developers (and computer enthusiasts, many of which are students), but are also known to support scientific work, and are used as a foundational technology and force multiplier in a multitude of organisations and commercial enterprises.

Therefore, improving Nixpkgs is improving all of those users' projects at the same time: providing security tracking, boot chains, and a bootstrap toolchain contributes to strengthening large and diverse software ecosystems building on top of Nix.

The NLnet Foundation is partnering with the NixOS Foundation to leverage Nix’s capabilities for providing sustainably accessible software under the umbrella of the Next Generation Internet (NGI) initiative of the European Commission.
Improving security of Nixpkgs would open up a way for downstream projects supported through NGI to build more advanced solutions to tackle state of the art problems in the industry.

A working bootstrap toolchain, providing total control of our dependencies, will ensure the ability to access and use historical software, as preserved by Software Heritage, in the long run.
This will enable projects that build and run with Nix today to continue working decades into the future.

## How are decisions regarding this technology’s development made? Please describe the project’s governance model.

Individuals and loosely organised contributor or maintainer teams review each other’s work and discuss technical decisions in public.
Despite the principal author technically being a [BDFL](https://en.wikipedia.org/wiki/Benevolent_dictator_for_life), there are only weak and implicit power structures that are largely centered around demonstrated achievements, and decisions largely are based on technical merit as judged by those involved.
We proudly cultivate a vibrant and growing community of contributors, as demontrated by Nixpkgs being one of the most active projects on GitHub.

Self-organised formal [community teams](https://nixos.org/community/#governance-teams) take responsibility for maintaining code in their areas of expertise, and have a more formal communication and permission structure.
Otherwise, apart from more regular activity, they operate just like any other group of contributors.

Nix itself is currently [maintained by a team of six people](https://github.com/NixOS/nix/tree/master/maintainers#members) including principal author, who meet twice a week to discuss technical decisions and review contributions.

Ecosystem-wide technical decisions are negotiated in an [RFC process](https://github.com/NixOS/rfcs/).

The NixOS Foundation mainly ensures funding for critical assets such as the binary cache, manages permissions in the GitHub organisation, and facilitates community activities.
The Foundation board as a legal entity is not involved in technical decisions.

Project governance has immensely gained in structure lately: In the past year, four of the eleven currently active community teams were formed, the NixOS Foundation board was restructured, and there exist plans for setting up paid support functions to ensure continued operations.

## How does this project handle security risks? Are there policies, procedures, or tools in place to minimize the introduction of vulnerabilities or undesired contributions?

There exists a [security team](https://nixos.org/community/teams/security.html) and an [infrastructure team](https://nixos.org/community/teams/infrastructure.htm).
The latter tends to critical assets, such as the build servers and the security keys which sign Nixpkgs software.

[Security-relevant issues and pull-requests](https://github.com/NixOS/nixpkgs/labels/1.severity%3A%20security) are tagged by their maintainers, the security team, or contributors, e.g. in case where CVEs are not used.

There are multiple attack surfaces in Nixpkgs:

1. Authenticating sources: not all upstreams sign their code. Our system is able to sources by validating their content hash.
2. Vetting upstream projects: we confirmed our ability as a community to identify at-risk upstream projects.
3. Tarballs can exploit vulnerable code in our decompressor. The same applies for any tool to fetch sources.
4. Adversarial contributions: Our code review system will usually thwart attempts at this as long as source validation is honored. Dedicated actors could still mount long-term sophisticated attacks.

Core packages, whire are depended upon by many others, usually have clear ownership structures where it is expected to wait for maintainers' approval before merging a change.

Packages at the leaves of the dependency graph are more vulnerable, as it's usually hard to find contributors with the necessary expertise.
This tends to encourage courtesy approvals by maintainers who are otherwise not involved.

Process improvements are constantly being discussed in order to establish a mutual understanding of the roles and expectations of committers.
Still, in Nixpkgs and NixOS the committer community follows largely implicit rules.
There is a high degree of social trust involved, and active developers and maintainers, while culturally and geographically diverse, usually have ongoing working relationships marked by diligent reviews and critical discussions.

## How will you address the challenge described? Give an overview of your work and why it is significant, specifically addressing the challenge. Explain what the field will learn from your proposed work and how it contributes to the long-term sustainability of the technology.

Reinforcing the security posture of Nixpkgs is crucial to enable mass adoption in a safe way, and provide defense in depth that scales to the size and diversity of our package ecosystem.

Here, we focus on reducing our reliance on foreign binaries to recompile Nixpkgs from scratch (along the lines of [Reflections on Trusting Trust](https://www.cs.cmu.edu/~rdriley/487/papers/Thompson_1984_ReflectionsonTrustingTrust.pdf)), ensuring we are are indeed running the code we compiled by leveraging existing security components, and putting in place mechanisms that allow us to deliver the most up-to-date, secure software whenever it is available in a way that can be sustained given our maintainer capacities.

Each of these three items contributes to fundamental security hardening measures, and aims to protect Nixpkgs against a class of vulnerabilities.
We will express the significance in matters of "what would success look like".

More precisely:

A security team usually provides automation for itself, maintainers, and end users:

- Triaging interface for marking vulnerabilities
- Monitoring the build and distribution pipeline to notify users or alert the security team
- Statistics and tracking of vulnerabilities for research and organizational improvements

In the past, Arch Linux's security tracker was considered for reuse in NixOS, but it is very old and tailored to Arch Linux.
Here, we propose to set up a new security tracker with Nixpkgs and NixOS in mind, but in a generic way, which can be reused and self-hosted, not only for Nixpkgs but any overlay of Nixpkgs.

Our main challenge is to process the large amount of data generated from ingesting many security feeds.
We would tackle this by providing powerful filtering capabilities linking all the available metadata, for example from Repology and Nixpkgs.

A prototype usable by the security team would:

- Reduce the workload for the security team
- Improve security posture of Nixpkgs, especially for hard-to-track channels, e.g. "soon to be end of life" NixOS releases
- Manage users' expectations, clearly communicate when vulnerabilities will be patched on their systems and inform them about possible paths for remediation

As for boot security, NixOS recently acquired [a form of user-owned Secure Boot](https://github.com/nix-community/lanzaboote) as part of [an NLnet grant](https://nlnet.nl/project/NixOS-UEFI/).

As of now, Secure Boot in Nixpkgs is [slowly being upstreamed](https://github.com/NixOS/nixpkgs/pull/231951), but the Secure Boot ecosystem is still in its infancy.
It still requires merging existing patches to `systemd` to be viable in the long run.
The next stage after Secure Boot is to have measured boot, which is the final piece to have a reasonable form of security in the boot process of a Linux distribution.

As a result of this project, NixOS will be able to boot with:

1. UEFI Secure Boot with user-owned keys or MSFT-backed key infrastructure via shim
2. Key storage scured through a Hardware Security Module (HSM) or similar hardware token as long as it is supported by PKCS#7 standards. Nitrokey will have a special emphasis as it is a mature, open hardware, affordable HSM product

Also, NixOS will be able to be deployed in situations where:

1. It is desirable to lock down completely the runnable binaries, e.g. only the Nix store is allowed to execute binaries.
2. It is desirable to authenticate and verify the integrity of the Nix store
3. Updates are mission-critical and recovery must be assured in case of failed upgrades, e.g. mobile or embedded systems.

A complete bootstrapping toolchain will for the first time make possible to inspect our complete build graph down to a piece of foundational machine code that is small enough to be audited manually.
More importantly, it will allow us to automatically ensure the absolute integrity of our entire software supply chain, and that all build artefacts correspond to their source code.
This will also unlock our long-term goal to find ever shorter bootstrapping chains in order to reduce our reliance on massive amounts of historical source code, auditing which is intractable.

### What the field will learn from our work

In all security areas we presented, most of our work will be both reusable component-wise as well as available as a whole "off the shelf".
Having a complete integration of the various techniques and tools will provide a unique opportunity for any software developer to inspect and work with our solution.
By offering a sufficiently transparent setup in a highly visible project such as NixOS, we intend to provide learning opportunities for motivated people.

### How our work will contribute to sustainability of Nix, the Nix ecosystem, and FOSS more generally

Introducing the mentioned security projects as dependencies to Nixpkgs will raise awareness of security concerns, and direct the Nix community's attention to those upstream projects.
This is likely to translate into additiodevelopment and maintenance capacity these projects would benefit from.

Similarly, the security tracker will serve as a central place for building and sharing organisational knowledge around security considerations.
We expect this to be a first point of contact for potential contributors.

## How will you accomplish the work? Please provide a list of deliverables with associated effort and cost of each deliverable.

### Boot chain security

- Introduce preparatory upstream features: (4w, 20 000 EUR).
- Produce NixOS's default UEFI Secure Boot images with `shim` and `shim-review`: (4w, 20 000 EUR) (*)
- Write a NixOS RFC "Bootspec v2" and provide an initial working implementation: 2w, 8 000 EUR)
- Add TPM2 support to Lanzaboote: (4w, 20 000 EUR)
- Safe updates (A/B schemas) in NixOS with `systemd-boot`: (2w, 10 000 EUR)
- Integrity checks for the Nix store (`*-verity`): (4w, 20 000 EUR)
- Integration: Provide a minimal hardened NixOS configuration stripped of interpreters: (4w, 20 000 EUR).

Total: 120 person days, 118 000 EUR.

(*) This is dependent on the [shim-review project](https://github.com/rhboot/shim-review) owners to accept our application.

### Security tracker

- Web service scaffholding and core features: APIs & vuln. tracker ingestion (3w, 12 000 EUR)
    - architecture, structure, testing, packaging, deployment
- [`label-tracker`](https://git.eno.space/label-tracker.git/) integration and improvements (2w, 8 000 EUR)
- User story "Security team" (2w, 8 000 EUR)
    - filtering, triaging, generating advisories, linking metadata
- User story "Maintainers" (3w, 12 000 EUR)
    - assisting security team by auditing their tools, validating their workflows, introducing automation for their PRs (bump, backport, mark EOL/vulnerable)
- User story "End-user" (5w, 20 000 EUR)
    - gathering information about the current security properties of a release
    - subscribing to the security tracker for a release's security updates
    - various APIs to reuse alerting, open data, exports

Total: 75 person days, 60 000 EUR

Explanation:

The working mode we envision is having a strong web developer with extensive Nix experience developing a reusable high-standard platform with maintenance in mind, i.e. end-to-end testing, etc, with enough flexibility to be reused by similar Linux distributions, e.g. Guix.

We decided to split the work into 3 "big milestones" or "target goals", aiming to make the platform usable for the given target audience.
Each milestone involves developing specific features and requires close collaboration with the target audience to ensure we satisfy their needs, following UX/UI research methods and best practices.
Each phase includes a user discovery part and a development part; user discovery can be performed asynchronously in some situations to improve the velocity.

[`label-tracker`] is an important piece of the puzzle for end-users to benefit from the integration of NixOS, our Git repositories, and our channels to answer non-trivial questions like "Is this PR in my distribution channel?" or "When is this PR expected to land in my distribution channel?".
Those improvements can include performance work, scaling up the infrastructure to make it an asset in the Nix community available to everyone.

### Bootstrapping Nixpkgs

- Develop the Nixpkgs C/C++ bootstrap chain with [stage0-posix](https://github.com/oriansj/stage0-posix): 4w, 16 000 EUR
- Reviews, testing, infrastructure setup and maintenance: during the whole project, 4w, 16 000 EUR
- Prototyping bootstrapping of additional programming languages, e.g. Rust, Go. 4w, 16 000 EUR
- Total: 60 person days, 48 000 EUR

Explaination:

The first deliverable [stage0-posix](https://github.com/oriansj/stage0-posix) requires modification of the [Nixpkgs standard environment](https://nixos.org/manual/nixpkgs/unstable/#part-stdenv).
This is surgical work to avoid breaking things and introducing significant regressions while not disturbing the work of the others by introducing very long recompile times.

Moreover, review and testing is particularly important here, as Nixpkgs maintainers usually have their own domain expertise specific to some part of the standard environment.
Improving tooling support and processes for work on those pieces is also important for long-term maintenance.

Finally, currently, most of Nixpkgs is bootstrapped with C programs and Bash scripts.
Future exploration of alternative programming languages for that task will require the capability to bootstrap those programming languages.

### Summary

Overall, Nix maintainers essentially have to dedicate their employers’ time or take compensation that can compete with other engagements; known contributors who could do the bulk of the work are in a similar situation or otherwise would need substantial time for onboarding.
Therefore we have to assume consultancy rates to be able to keep to the time frame, with the option to trade budget for velocity to some extent.

We expect multiple contributors to work in parallel where possible.

Total: 226 000 EUR

## Describe your relationship to the maintainers of this technology. Are you yourself the maintainer? Do they know you plan to do this work and do they support it? Please tell us more about how you obtained their support and how you plan to work together to make sure your contributions are accepted.

I assisted Ryan Lahfa and Emily Trau with developing this proposal.

Ryan Lahfa is a [Nixpkgs security contributor](https://github.com/NixOS/nixpkgs/pulls?q=is%3Apr+author%3ARaitoBezarius+label%3A%221.severity%3A+security%22+is%3Aclosed) and [reviewer of security fixes](https://github.com/NixOS/nixpkgs/pulls?q=is%3Apr+reviewed-by%3ARaitoBezarius+label%3A%221.severity%3A+security%22+is%3Aclosed+), the [current release manager of NixOS](https://nixos.org/community/teams/nixos-release.html), and oversaw the release of NixOS 23.05.

He coordinated handling the [end of life status](https://github.com/NixOS/nixpkgs/pull/233024) of [Node.js](https://github.com/NixOS/nixpkgs/pull/233399) and [OpenSSL](https://github.com/NixOS/nixpkgs/pull/231899) and offering smooth upgrade paths.
He also coordinated the disclosure in the [NixOS Graphical Installer vulnerability](https://github.com/NixOS/calamares-nixos-extensions/security/advisories/GHSA-3rvf-24q2-24ww) and is working on a fix.

Ryan works closely with the security team and is familiar with their challenges, and will lead the work on on the security tracker and secure boot deliverables.
The security team expressedly welcomes the contributions outlined in this proposal.

Ryan is one of the maintainers of [lanzaboote](https://github.com/nix-community/lanzaboote), and collaborates with systemd maintainers on bringing powerful primitives for every Linux distribution which would enable lanzaboote and NixOS to reuse upstream primitives directly.

The bootstrapping work will be led by Emily Trau who kickstarted the [minimal bootstrap project](https://github.com/NixOS/nixpkgs/pull/232329) and is involved in the bootstrap community that also delivered the [Guix full-source bootstrap](https://guix.gnu.org/blog/2023/the-full-source-bootstrap-building-from-source-all-the-way-down/).

Preparations for the grant applications were [announced in the community forum](https://discourse.nixos.org/t/german-federal-funding-for-foss-development/29036/4), with support of the NixOS Foundation board:

> While the NixOS Foundation board is not involved in technical decisions in the Nix ecosystem, we strongly support these proposed efforts to solve long-standing issues and trust the authors of these proposals to implement them as described.
> We are convinced that succeeding with these projects will enable more reliable software infrastructure and support its long-term maintenance both in the Nix ecosystem as well as for projects relying on it.
>
> — NixOS Foundation board
