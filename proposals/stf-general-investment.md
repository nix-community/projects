# The great fix forward – Sovereign Tech Fund general investment

This proposal was collaboratively developed by

- @fricklerhandwerk
- @proofconstruction
- @RaitoBezarius
- @wamirez

with contributions by (in ASCIIbetical order):

- @Ericson2314
- @Janik
- @edef
- @mweinelt
- @refroni
- @roberth
- @tfc

## Project title

*May be identical with application name*

Transforming global software distribution with Nix

## Describe your project in a sentence. 100 words

Nix makes computation with file systems highly repeatable; Nixpkgs is the largest, most up-to-date free software collection in the world; NixOS is a Linux distribution with a uniform declarative configuration interface.

## Describe your project more in-depth. Why is it critical? 300 words

[Nix](https://nix.dev) meaningfully reduces the global cost of software production and long-term use.
It is the basis of an ecosystem of exceptionally powerful tools – including Nixpkgs, [the largest, most up-to-date software repository in the world](https://repology.org/repositories/graphs), and NixOS, a Linux distribution that can be configured fully declaratively, with unmatched flexibility.

A large and growing number of open source applications and decentralized internet services can be deployed on NixOS with a single line of code.
This significantly lowers the barrier to open source adoption.

The Nix ecosystem is already on the way to become a default in the software development tool stack, by drastically shortening the time required to start working on software projects – written in any language – and lowering the cost of maintaining and sharing build setups and development environments.
It offers tools to bring together all of open source in one coherent, dependable environment.
It eases and stimulates contributions to public code.

It also serves as the platform to accelerate, keep usable, and drive adoption of countless software innovations that would otherwise be inaccessible to their audiences.
Moreover, the public [Nix binary cache](http://cache.nixos.org/) provides operational software artefacts from more than a decade back, some of which cannot be obtained otherwise any more.

We estimate the community to consist of 100 mostly volunteer maintainers, more than 2 000 contributors, more than [38 000 active users](https://survey.stackoverflow.co/2024/technology#2-other-tools), and 100 companies using and relying on Nix.
[Recent social media activity](https://www.youtube.com/watch?v=fuWPuJZ9NcU) reaches on the order of 500 000 people.
The Nix ecosystem is on an [exponential growth trajectory](https://ossinsight.io/analyze/NixOS/nixpkgs#overview) in terms of user adoption and development activity at the periphery.

Increasing popularity also puts the Nix ecosystem and its users at growing risk of supply chain attacks.
Ever more individuals and organizations rely on it, but our capacity to protect them from harm is still limited.

## Please provide a brief overview over your project’s own, most important, dependencies. 300 words

*This means code or software that your project uses.*

- Git, GitHub
- cURL
- Bash
- Various C and C++ compilers
- Python
- Rust
- OpenSSL
- OpenSSH
- Various GNU projects
- Meson
- systemd
- Linux kernel

## Please provide a brief overview of projects that depend on your technology. 300 words

- There are [12k active GitHub repositories using the Nix language](https://github.com/search?q=language%3ANix+archived%3Afalse&type=repositories&s=&o=desc)
  - Including a plethora of [community projects around Nix](https://github.com/nix-community/)
- The [NGI Zero software ecosystem](https://nlnet.nl/project/) with more than 400 active projects
- [Spectrum OS](https://spectrum-os.org), a security-focused computing environment iterating on the ideas behind [Qubes OS](https://www.qubes-os.org)
- [The European Commission's IT department](https://www.youtube.com/watch?v=I7wdcJ3YhoU)
- [INRIA’s Grid’5000 computing cluster](https://nix-tutorial.gitlabpages.inria.fr/nix-tutorial/index.html)
- Various [scientific projects](https://www.youtube.com/watch?v=SjjEDTccpQA), such as in [high-performance computing](https://github.com/freuk/awesome-nix-hpc)
- [Haskell Stack](https://docs.haskellstack.org/en/stable/nix_integration/)
- Companies worldwide run their business on Nix or NixOS, for example:
  - [Eviny](https://www.eviny.no), a Norwegian energy supplier
  - [WDZ](https://www.wdz.de), software for German public infrastructure
  - [Warren](https://warren.io), a European self-service cloud computing platform
  - [Google IDX](https://idx.dev), collaborative software development platform
  - [Replit](https://replit.com)

## Which target groups does your project address (who are its users?) and how would they benefit from activities proposed for funding (directly and indirectly)? 300 words

The Nix ecosystem serves anyone who needs computers to do exactly as intended, repeatably, far into the future.
Currently this manifests in three main target audiences:
- Professional software developers and students of the field
- Scientific researchers in industry and academia
- Enterprises and organisations

The proposed improvements for our contributor experience and quality of maintenance will benefit our users by:
- Helping their projects to avoid bitrot, preserving the value of past investments
- Making more dependencies readily available and keeping them up to date
- Making for a safer, more robust software supply chain
- Further ease self-hosting and customisation of software infrastructure
- Leveraging open source, adopting improvements created by users in a sustainable way

This will increase their productivity, and repeatability and portability of their work, and massively reduce the total cost of adoption and ownership of IT systems for everyone.
It would also make their setups more secure by default and make monitoring and mitigation of threats substantially more comprehensive and timely.

## Please describe a specific scenario for the use of your technology and how this meets the needs of your target groups. 300 words

In the course of their work, all of our target audiences may regularly need to:
- Try out new technology by running programs without disrupting or subtly changing their working setup

  Nix, Nixpkgs, and NixOS support this workflow as a first class use case, and are further supported by an ecosystem of convenience tooling.

- Develop software using pre-existing tools or libraries, possibly using multiple programming languages

  Nixpkgs abstracts over the build process of numerous programming ecosystems, allowing to routinely and seamlessly integrate heterogenous environments.

- Share complex setups with collaborators

  The Nix ecosystem makes it trivial to create reproducible, portable development environments that work the same on each supported system.
  With Nix, "works on my machine" is already "works everywhere, any time".

- Run integration tests

  [NixOS virtual machine testing](https://nix.dev/tutorials/nixos/integration-testing-using-virtual-machines) enable world-class quality assurance capabilities to assert that entire systems and even networked applications work as intended
  This highly convenient technique is ubiquitous in the Nix ecosystem.

- Create executables for multiple platforms

  By transparently supporting cross-compilation, Nixpkgs eliminates almost all of the effort for targeting the most common system types.

- Deploy their products or services with confidence

  The Nix ecosystem promotes [the purely functional software deployment model](https://edolstra.github.io/pubs/phd-thesis.pdf).
  This allows producing artefacts in a variety of formats and typically reducing deployments to adding a line to a configuration file and running one command.

## How was the work on the project made possible so far (structurally, financially, including volunteer work)? If applicable, list others sources of funding that you applied for and/or received. 300 words

By far most contributors are volunteers.
A small number of long-term maintainers contribute to the ecosystem in the context of their employment or business.
Some work is funded by companies paying maintainers, usually to develop substantial features rather than incrementally reducing tech debt.

Some contributors fund their independent work through NLnet research grants.
We also have a partnership with NLnet that provides funding for packaging more software with Nix through the European Commission's NGI program.

The NixOS Foundation receives [donations on Open Collective](https://opencollective.com/nixos) (mostly from individuals, sometimes from businesses), which are used for infrastructure expenses, supporting local meetups, and small-scale development efforts.
Currently the cache storage is sponsored by Amazon, cache traffic is sponsored by Fastly, build machines are sponsored by Equinix.

## What are the challenges you currently face in the maintenance of the technology? 300 words

*Please interpret this question as broadly as you want. A non-conclusive lists of challenge areas we are interested in learning about are:
managing contributions, addressing security vulnerabilites, project governance, licencing and other legal issues, dependency management, issue backlog, long-term planning/roadmapping.*

- Handling security vulnerabilities at the scale of Nixpkgs
  - Dealing with vendored or compiled dependencies
  - Decreasing turnaround time for triaging incidents and deploying patches
- We have only very basic solutions to automatically verify, enforce, and implement licensing compliance
- We lose a lot of friction in the contribution process
  - There is no systematic onboarding of new contributors with experienced maintainers
  - We’re lacking a recommendation system for picking reviewers, ownership is often not evident
  - We have too many communication platforms, most of which cannot be bridged (well or at all)
    - Many discussions take place where only part of the stakeholders are present
    - Moderation is not always catching up with traffic, and incidents repeatedly draw a lot of attention
  - We lack automation for ensuring correctness and avoiding regressions or additional work, and existing automation is slow or incomplete
- The issue backlog is not practically triageable any more at this point and only keeps growing
- The ecosystem and community is still hard to navigate for users and contributors alike
  - There are too many places for documentation, most of which are constantly going out of date and aren't produced from or tested against the source
- Some critical components are only superficially maintained because their code is hard to approach for most contributors
- There are many groups involved in building the Nixpkgs/NixOS distribution, but very little coordination between them
- It's very hard to measure user impact of certain changes
  - We struggle with deprecating interfaces and thus accumulate maintenance overhead
  - This limits our ability to do long-term planning, and many things can't be done without breaking changes
- Overall, we have very little visibility into what things cost in terms of volunteer time and effort
- We currently don’t know how to self-host large repositories such as Nixpkgs, and we’re stuck to GitHub

## What are possible alternatives to your project and how does your project compare to them? (optional) 300 words

- Guix

  Guix is an early fork of Nix using Guile as a configuration and implementation language, and is the only project comparable to the Nix ecosystem.
  Guix provides its own software distribution and operating system configuration framework, with free software exclusively.
  The community is much smaller, the package set is rather focused on scientific applications.
  Guix pioneered full-source bootstrapping, which is now ported to Nixpkgs.

- Debian

  As a software distribution, it has some similarities to Nixpkgs and NixOS in terms of size, and structure.
  Debian does not feature some of the key properties of the Nix ecosystem, such as declarative, composable configurations through uniform functional interfaces.
  [snapshot.debian.org](https://snapshot.debian.org/) can be seen as an equivalent of the [Nix public cache](https://cache.nixos.org)
  A notable difference is that Nixpkgs also has rolling release in addition to stable releases, but does not feature LTS releases.

## What do you plan to implement with the support from STF? 900 words

*Please describe your objectives and the corresponding activities.
State clearly how they contribute to the improvement or maintenance of the technology, especially with regard to security and resilience.*

We understand resilience as the ability to recover from disruptions and to adapt to a changing environment.
Apart from implementing technical measures, having qualified engineers available for ongoing maintenance and various issues as part of their engagement will improve the overall health of the ecosystem by unblocking volunteer efforts more quickly than is currently possible.
We expect this to have a compounding effect on overall productivity, as we estimate that more than 95% of the work is currently done by volunteers, many of whom are slowed down by lack of support and swift decision making.

- Improve the contributor experience (115k)

  Streamlining the contribution process should make it more attractive for newcomers to participate in development, and keep existing people around and motivated.
  Growing the contributor community will make the ecosystem more robust against fluctuation.
  We want to achieve this by making more systemic knowledge explicit and easier to discover, access, and manipulate; minimize the potential for regressions; and reduce contribution turnaround time.

  - Simplify the Nix configuration system (15k)

    - Remove static initialisation and global variables
    - Decouple configuration of separate components
    - Port the Rust installer from Lix

  - Increase coverage of the Nix test suite (15k)

    - Run integration tests on all platforms and distributions
    - Run all tests with and without the daemon
    - Test the evaluator against all stable Nixpkgs releases
    - Run store tests on all store types

  - Reduce duration of Nix functional tests to 10% (30k)

    - Run all store tests in memory
    - Run all evaluator tests in memory

  - Set up monitoring to improve decision-making (15k)

    - Count binary downloads, contributor activity, community activity
    - Expose a public dashboard for the metrics

  - Professional training moderation team volunteers (20k)
  - Investigate tooling to decrease dependence on GitHub (20k)

    We may want to collaborate with GitLab or Forejo to enable migration of Nixpkgs-scale repositories.

- Improve documentation (110k)

  More focused, correct, up-to-date, and well-structured documentation will make the system more learnable.
  This will over time reduce the number and size of blind spots in components that may otherwise end up unmaintained, a problem we are observing for many years now.
  It should also tangibly reduce maintainer workload by making users and contributors more self-sufficient.

  - Allow building Nix documentation independent of the binaries (10k)
  - Render Nix language builtins signatures from declarative specifications (10k)
  - Render all Nixpkgs interface documentation from source (15k)
  - Build testing infrastructure for user guides (20k)
  - Automatically test all code samples (20k)
  - Improve discoverability (35k)
    - Restructure NixOS manual to display tested configuration examples
    - Restructure package search to be oriented around applications instead of derivations
    - Expose SEO-relevant metadata in the reference manuals

- Reduce ongoing costs of continuous integration and distribution (130k)

  Infrastructure expenses are a significant risk for the ecosystem, because they are almost completely sponsored by companies who may end their support any time.
  Reducing these ongoing costs will make it easier to migrate between providers or even self-host.
  Improving CI performance will also contribute to faster workflows, and increase responsiveness to security incidents.
  This will also impact all downstream users and significantly reduce their storage and energy requirements for the forseeable future.

  - Deduplicate the public cache storage (30k)
  - Improve maintainability of the CI setup (45k)
    - Investigate alternatives to maintaining Hydra and ofBorg
    - Separate the frontend and backend of Hydra
    - Remove all Perl code from Hydra
    - Enable local testing of ofBorg
    - Set up an ofBorg staging instance
  - Fix performance bottlenecks in our CI (20k)
    - Improve the Hydra scheduler
    - Optimize `nix-eval-jobs`, porting existing work from Lix
  - Investigate performance improvements (30k)
    - Port Nix language evaluator optimisations from Lix
    - Port format serialiser optimisations from Lix
    - Prototype a scalable evaluation cache
  - Fully automate the release process for Nix (5k)

- Strengthen supply-chain and end-user security (280k)

  At the scale of Nixpkgs, we have many attack surfaces that are currently not being taken care of appropriately.
  The proposed measures will make common interactions with the Nix ecosystem substantially more secure by default.

  - Rootless Nix daemon (50k)
  - Roll out secure boot capabilities (30k)
  - Harden CI checks (35k)
    - Add reproducibility checks for FODs
    - Add an FOD proxy
  - Scriptless system activation (30k)
  - Roll out full-source bootstrapping (50k)
  - Make vulnerability tracking a first-class use case (70k)
  - Monitor build reproducibility (hash collection) (15k)

## How many hours do you estimate for these activities?

*We are interested in a rough estimate.
Please add the hours from all developers who would be involved in this.
It may be helpful to look at the hours you spent on the project in the last years.
Add a number only, please.*

5 500

## Please estimate the cost of the work described in your application. It should be in numbers only, in Euros.

635 000

## In how many months will you perform the activities?

*enter number only*

12

## Who (maintainer, contributor, organization) would be most qualified to implement this work/receive the support and why? 300 words

The NixOS Foundation would be the legal custodian of the project, to be implemented by current maintainers of each of the affected subsystems, who may distribute tasks to experienced contributors where appropriate.
Maintainers are typically senior software developers with years of experience in their domain of responsibility.
