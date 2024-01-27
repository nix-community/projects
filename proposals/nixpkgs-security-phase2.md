# Nix ecosystem supply chain security (STF phase 2)

## Please describe what you would like to work on. Explain how this work builds on top of what you accomplished in Round 1. (900 words)

Primarily we would like to finish and round off the projects started in Round 1 to make them more immediately useful, and as an addition close a major gap in the software distribution lifecycle in the Nix ecosystem.

## Boot chain security

- Follow up on Secure Boot via shim.

  Its current state allows booting the installer, but installing from there will not yet provide a system that can be booted with Secure Boot enabled. Implement support for Machine Owner Keys in Lanzaboote, and provide a reasonable user experience for installation.
  
- Add code to NixOS image generators to create `dm-verity`-style images for appliance use cases.

  Although we determined that `dm-verity` is not ideal in the general case for NixOS, it’s still a good option for embedded deployments. (We could not confirm a timeline or budget for the "Signed System Volume" approach in time, which requires a ZFS expert.)

- Enable building a NixOS system without Bash, Python or any other interpreter.

  The work done in Round 1 laid the foundation for this to be feasible and sensible. Removing the other interpreters will focus only on the “critical path”, i.e., the system closure without customisations.

- Add end-user and contributor documentation.

  The overall setup is quite complex and the constitutent parts are neither particularly well known even among software developers, nor easily discoverable. Bootspec and Lanzaboote are two novel major components that are unique to the Nix ecosystem, and how they integrate with existing technologies is largely undocumented. Write an architecture overview to inform and orient users, and onboarding documentation for contributors.
 
## Security tracker

- Refine results and improve performance for the local scanner.

  Because CVE data is course-grained compared to Nixpkgs derivations, we need to obtain additional information from the online tracker and match it up with local data, such as relevant patches, to significantly reduce the number of false-positives and display more actionable reports. 
  To be applicable for day-to-day use, the tool needs a background service to run scans and fetch advisory information asynchronously, and performance optimisations in processing the data.

- Add hash collection infrastructure.

  Nix-based builds are highly repeatable, but not necessarily bit-for-bit reproducible. They are mostly indexed by their inputs rather than outputs, which requires post-factum verification of build results. Add a web service for community members to compile a transparency log of build output hashes and independently check build reproducibility.

- Improve user experience and performance for the online tracker.

  Since the online tracker is supposed to be an important touchpoint for maintainers, we need to design workflows around their needs, such that the tool stays out of the way as far as possible. Otherwise it won't be used or will scare away potential contributors. Another aspect of that is improving query performance to support both fluent interaction and deployment on frugal infrastructure.

## Full-source bootstrap

- Make fully bootstrapped Nixpkgs the default.

  Due to the difficulties encountered in with building 64-bit GCC with glibc, and the fact that a fundamental change such as swapping out `stdenv` and the Rust build will fall under substantial scrutiny, we would like to take the time required to see the project and the anticipated lenghty review process through to the end. The outcome should be entirely transparent to consumers of Nixpkgs, but will finally remove major single-points-of-failure where large binaries have to be supplied manually, and therefore greatly improve process transparency and possibilities for disaster recovery.

- Add end-user and contributor documentation.

  Being able to understand how things work is a key security property in this domain, and documentation is the entry point to discovering the details of the setup. Write an architecture guide to orient end-users and extend in-code documentation to ease onboarding contributors.

## Going full-circle: Securing and optimising Nixpkgs continuous integration

In addition to the previous improvements, we want to shift our focus from mitigation to prevention.

All changes to Nixpkgs go through continuous integration, and we have two systems for that: ofborg and Hydra. They operate at two security levels; ofborg processes all inbound pull requests and runs tests in a disposable environment, whereas Hydra is responsible for building, persisting, and signing the final artifacts of all accepted changes.


Because ofborg works on untrusted code, it can't provide guarantees that maintainers aren't fooled by attackers manipulating its outputs. We want to harden it against uninentional and intentional mistakes, that is, bugdoors.
On top of that, for more than a year we're observing that Nixpkgs is scaling faster than ofborg can keep up in terms of performance, leading to a situation where CI checks become prohibitively expensive, thus incentivising to skip them altogether.

Therefore, we propose to:

- Unblock contributions to ofborg, and harden build isolation.

  ofborg also happens to be a complicated piece of software that is unique to the Nix ecosystem, and currently cannot be tested outside of production. Hardening the sandboxing of pull request builds will, as a first measure, prevent trivial poisoning of input artifacts and decrease the potency of visual spoofing.
  

- Apply the principle of least privileges to the Nix daemon

  Right now, the security benefits the Nix paradigm provides are only fully realised when using Nixpkgs.
  The Nix daemon, the background process managing builds, performs all privileged operations, making it a central component for which it's imperative to provide defense in depth. Constrain the opportunities for attacks across the board, including for ofborg, and beyond the core Nix ecosystem by decreasing the reliance on the administrator account for the Nix daemon.

## What is the total amount you are requesting (in Euros)?

## Will the team composition be different for Round 2? If so, please explain.

The team has grown over the course of Round 1 from 5 to 15 members as work progressed and requirements got more refined. It will stay the same as at the end of Round 1, with the following exceptions:
- John Ericson (@Ericson2314) and Lily Foster (@lilyinstarlight), maintainers of Nix and ofBorg respectively, are added as domain specialists to lead work on the "continuous integration" milestones
- Alexander Groleau (@proofconstruction) will replace Valentin Gagarin (@fricklerhandwerk) in the administrative role for availability reasons

## Please include a list of milestones with their timeline and costs. Keep in mind that if your plan for Round 2 is accepted, this plan will serve as the binding terms for the annex to your participation agreement.

## Boot chain security

- Boot security integration
    - Add support for Machine Owner Keys in Lanzaboote and enable complete installation (20d, 20 000 EUR)
    - Make NixOS image generators create dm-verity-style images for appliance use cases (10d, 8 000 EUR)
    - End-user and contributor documentation (4d, 3 200 EUR)
- Bash-less activation
    - Replace bespoke scripts with generic functionality (10d, 8 000 EUR)
    - Replace incorrect usages of script with ExecStart (10d, 8 000 EUR)
    - Add custom tools to replace scripts (10d, 8 000 EUR)
    - Add configuration options (5d, 4 000 EUR)
    - Add a configuration profile (2d, 1 600 EUR)

Subtotal: 71d, 60 800 EUR

## Security tracker

- Hash collection infrastructure
  - Create service to store and query signed hashes (6d, 6 000 EUR)
  - Ingestion from post-build-hook and from Hydra (6d, 6 000 EUR)

- Security tracker improvements
  - User testing and UI/UX improvements (30d, 30 000 EUR)
  - Improve Nixpkgs evaluation performance (10d, 10 000 EUR)
  - Optimise database queries (10d, 10 000 EUR)
  - Improve PR tracker performance (10d, 10 000 EUR)
   
- Local scanner improvements
  - Show more details on Nixpkgs issues (2d, 2 000 EUR)
  - Improve package matching (2d, 2 000 EUR)
  - Check which patches are applied (3d, 3 000 EUR)
  - Daemonise the local scanner (2d, 2 000 EUR)
  - Performance improvements (2d, 2 000 EUR)

Subtotal: 83d, 83 000 EUR

## Full-source bootstrap

  - Cross-compile the 64-bit glibc toolchain from the 32-bit musl one (24d, 19 200 EUR)
  - Build the default stdenv and swap it over in Nixpkgs (20d, 16 000 EUR)
  - Turn on Go bootstrapping (1d, 800 EUR)
  - Upstream the Rust bootstrap prototype (5d, 4 000 EUR)
  - In-code and end-user documentation (12d, 9 600 EUR)

Subtotal: 62d, 49 600 EUR

## Nixpkgs continuous integration

- Nixpkgs continuous integration
  - Enable ofBorg for local testing (10d, 10 000 EUR)
  - Set up ofBorg on staging to enable code changes (10d, 10 000 EUR)
  - Add FOD reproducibility checks (15d, 15 000 EUR)
  - Add a FOD proxy (20d, 20 000 EUR)
- Rootless Nix daemon
  - Swappable security/sandboxing policies for Nix build processes (20d, 22 400 EUR)
  - Create turn-key configuration for Nix running with existing limited rootless daemon (5d, 5 600 EUR)
  - Allow multi-user garbage collection with a rootless Nix daemon (5d, 5 600 EUR)
  - Allow for separate builders to use the same store (15d, 16 800 EUR)

Subtotal: 100d, 105 400 EUR

Total: 316d, 298 800 EUR

## How will this work impact the technology you are working on beyond the timeline of Round 2?

The main long-term impact of the proposed work is in making a greater number of security improvements and process optimisations available by default or as turn-key options to Nixpkgs and NixOS users and contributors:
- Swapping a fully bootstrapped Standard Environment will remove a single point of failure where an individual has to supply a blob, and greatly increase our capabilities of disaster recovery.
- Improving boot security component-wise brings us closer to a fully integrated solution en par with or superior to other distributions or  commercial offerings.
- Decreasing turnaround time on continuous integration will make changes land faster, including security updates, and eventually enable us to make the checks more reliable and mandatory *before* accepting a change rather than just releasing it.
- Communicating the work done in a coordinated fashion will make the components in question more accessible to volunteer contributions than ever.

This proposal was developed by (in ASCIIbetical order):

@ElvishJerricco
@Ericson2314
@JulienMalka
@Mic92
@RaitoBezarius
@cidkid
@emilytrau
@fricklerhandwerk
@jeremiahs
@lassulus
@lheckemann
@lilyinstarlight
@nikstur
@raboof
@t184256
