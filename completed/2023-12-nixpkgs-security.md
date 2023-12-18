# Nix ecosystem supply chain security - report for STF Phase 1

## Please provide an update for each work package/milestone/deliverable described in your application. Please also include any work that you expect to complete after submitting this report through the end of Round 1 on December 31, 2023. If the actual outcome varies from the original outcomes described in the application, provide an explanation for the variation.

### Boot chain security

Work done for this subproject is captured in a [tracking issue on GitHub](https://github.com/NixOS/nixpkgs/issues/265640).

#### Upstream features

Handling of Portable Executable (PE) binaries is finished, and can be used to [sign and verify](https://github.com/RaitoBezarius/goblin-signing/blob/main/tests/test_snakeoil_sign.rs) PE certificates.

We contributed to systemd release 255, unblocking our two pull requests in review, which will land in systemd 256 in the next weeks.
These features will be consumed by Lanzaboote directly, and don't need to get into NixOS.

#### NixOS UEFI Secure Boot

We can build ISO images that boot via shim on systems with Secure Boot enabled and test keys pre-loaded, verifying the kernel, its command line, the initramfs, and the Nix store of the installer system.
The work is in the [nixos-shim repository](https://github.com/RaitoBezarius/nixos-shim), and a [shim-review application](https://github.com/lheckemann/shim-review) is being finalised for submission.
Once review passes and we have a signed shim build, these images can be booted on machines that only ship with Microsoft keys in their UEFI.

#### "Bootspec v2" RFC

[RFC 165](https://github.com/NixOS/rfcs/pull/165) is published and in the shepherd phase.
A prototype will be presented by end of the year.

#### Lanzaboote TPM2 support

We found a systemd bug in TPM handling, which blocked progress. The bug is now fixed after going through testing.
Implementation of [end-to-end testing](https://github.com/nix-community/lanzaboote/pull/168/#issuecomment-1811747334) will be delivered by end of the year.

#### Safe NixOS updates

This enables automatic rollback if reproducibly booting multiple times fails.
The [implementation is ready](https://github.com/NixOS/nixpkgs/pull/273062) and will be merged by end of the year.

#### Boot-time integrity checks

Integrity checks are [implemented with `nix-store --verify`](https://github.com/NixOS/nixpkgs/pull/273593) as an alternative to the usual `dm-crypt` workflow that relies on disk encryption for verification. This is conceptually simple and safe, but causes significantly longer boot times.

This milestone was largely a research problem. [Detailed assessment of alternative approaches](https://discourse.nixos.org/t/boot-time-integrity-checks-for-the-nix-store/36793) revealed that those are not tenable for the typical NixOS use case. The project work produced an [outline for a technically more ideal solution](https://discourse.nixos.org/t/boot-time-integrity-checks-for-the-nix-store/36793#future-work-9).

We only used 50% of that milestone's budget.

#### NixOS activation without interpreters

NixOS can now [boot without running Perl](https://github.com/NixOS/nixpkgs/issues/267982), with a corresponding configuration option. Some work still needs review, but will be merged by end of the year.

Removing Bash from the boot process is much more involved. An [implementation strategy](https://pad.lassul.us/fLa5ZrHKTiawpYxV5MRtXA#) was produced as part of this milestone.

### Security tracker

The project is maintained in its own [GitHub repository](https://github.com/Nix-Security-WG/nix-security-tracker).

As noted in our communication with STF mid November ("Dealing with project risks"), we had a setback on this subproject's timeline:
The two people responsible for large parts of the implementation were unable to follow through; one for personal reasons, the other had to take care of a [critical piece of Nix ecosystem infrastructure](https://discourse.nixos.org/t/nixos-s3-long-term-resolution-phase-1/36493) that takes priority. At that point only the first milestone was finished, and we lost time in the transition.

As a result, the outcome won't be as polished and smooth as we envisioned. In particular, user testing to incorporate feedback before production deployment won't happen within the timeline. A large part of the business logic is implemented, and we're working on integrating all components.

#### Scaffolding and data ingestion

The web service is running on a test deployment and continuously ingests:
- MITRE CVEs
- Full evaluations of Nixpkgs release branches

Until the end of the year we will add as data sources:
- NIST CVEs
- Status of pull requests for each release branch

#### `label-tracker` improvements

The team implemented a new project, [`pr-tracker`](https://github.com/molybdenumsoftware/pr-tracker), copying some logic from [`label-tracker`](https://git.eno.space/label-tracker.git/).
It allows determining on which of the tracked branches a pull request is merged.
This information can be used by the security tracker and helps refining the output of the local scanner.

Currently the data processing is not complete, but this milestone will be delivered as specified.

#### User story "Security team"

Admin users ("security team") can create advisories and link them up with CVEs and Nixpkgs derivations, displaying responsible maintainers and other metadata.
The filtering and triaging use cases will be finished by end of the year.

The use case for linking metadata (such as mapping affected versions to Nixpkgs derivations) is not started yet, but we're confident to present at least basic functionality on time.

Given the long-term perspective, rather than only focusing on raw features, we're putting in extra effort to make the code easy to iterate on, especially by volunteers.

#### User story "Maintainers"

Work is still in progress, but by end of the year we will:
- Allow maintainers to manage tracker data for their packages
- Display a change history for advisories

We won't be able to create pull requests automatically in phase 1. As a substitute, we will montior GitHub events: new pull requests mentioning issues linked in our advisory database will be captured automatically.

#### User story "End-user"

We implemented a local security scanner that cross-references the given system configuration against security advisories. This [builds on prior art](https://github.com/Nix-Security-WG/nix-security-tracker/issues/15), but is a custom implementation due to time constraints. 
Because this scanner can connect to the security tracker, it can take into account manually-collected Nixpkgs-specific knowledge to produce more accurate reports than existing solutions.

### Bootstrapping Nixpkgs

The full-source bootstrap chain builds 32-bit GCC 13 based on musl. Progress is tracked as [references to the original GitHub pull request](https://github.com/NixOS/nixpkgs/pull/227914).

While the musl route enabled quick progress, the complexity of the very last step, building 64-bit GCC 13 with glibc, turned out to be not surmountable within the timeline. This means we will have a working 32-bit musl `stdenv` by the end of the year, and also a toolchain to bootstrap Rust.

## How has this challenge impacted the open source component(s) you are working on? (450 words)

We got a lot more insight into the limitations of available open source components for implementing the desired security properties.
We made the ongoing work greatly more visible, and shared domain knowledge in the form of discussions and documentation, and by getting more people involved.
For each of the subprojects, there are now outlines for how to proceed rather than having open-ended problems.
Nixpkgs bootstrapping has become a lot more robust and transparent.
NixOS has gained more turn-key hardened configurations and also more essential capabilities required for deployment in security-sensitive settings.
The various approaches to implementing global vulnerability discovery and matching are now unified in one central, actively maintained component.

## How has this challenge impacted the open source community and/or organization you are working with? (450 words)

The challenge enabled long-term contributors to make substantial progress on developments that would otherwise have taken an indefinite amount of time to come to conclusion. In some cases it either provided an opportunity to materially reward outstanding domain experts for their continuous volunteer efforts, or allowed onboarding young talent into a professional setting, boosting career opportunities. 
Work on the project was extraordinarily very well received by the community, and saw noteworthy support through volunteer contributions in the form of code, reviews, and testing.
It was also a valuable stress test for the NixOS Foundation to support such a large project in a timely manner, and revealed both some inefficiencies as well as strengths that were otherwise not evident.

## What difficulties did you face during this first round? What, if anything, have you learned in dealing with these difficulties that you would want to share with people who are facing similar problems? (500 words)

### Difficulties and learnings

- The project kick-off was delayed
    - Learnings:
        - Decide up-front what to do in such a case

- Some project participants had limited availability
    - Domain experts have regular jobs and hence are not available for large projects, but some can help out in a limited capacity
    - It is not a rare exception that people have to stop working during a project, for various reasons
    - Generally, balancing cost of implementation and duration of engagement is quite a challenge
    - Learnings:
        - When proposing a project, have people ready to implement it
        - Ideally establish a talent pool database in the community that shows skills, experience, and availability
        - Ensure that for each sufficiently large part of the project, at least one person is highly available
        - Consider people for backup on each milestone
        - Include re-staffing and other overhead in the estimates

- Unsurprisingly, timelines are hard to coordinate in loosely organised, globally distributed community
    - The few available experts tend to be spread over multiple time zones
    - When real-time meetings are required, only few slots per week are viable 
    - Learnings:
        - Put more effort into project management 
        - Put even more emphasis on coordination overhead in the estimates

- Fulfilling large pre-defined deliverables on time can be very stressful
    - Learnings:
        - Spend more time on reducing unknowns up-front

- Deadlines set perverse incentives
    - If availability of resources is determined by delivering on time, there is a strong temptation to reduce implementation quality (documentation, testing, factoring, user experience) in order to make a deadline
    - Especially when there is only a fixed one-time budget anyway, the detriment to the outcome is compounded (basic game theory)
    - Low implementation quality will substantially increase the cost of maintenance
        - Maintainance of the code will have to rely on volunteer work
        - Therefore maintenance happening is made a lot less likely
    - Learnings:
        - Resist the temptation at all cost
        - Actively discuss cutting scope when communicating risks with the funding organisation

### Recommendations to STF to lower cost and raise quality of implementation

- Set more generous timelines
    - It allows more people (especially high-profile experts or volunteers) to get involved
    - Scheduling is fundamentally hard (i.e. expensive), and loosening the requirements solves most of it
- Set a fixed budget accompanied by high-level goals rather than deliverables with a price tag
    - This is essentially what NLnet is doing successfully - "programs" rather than "projects" - and we made good experience with that
    - Fine-grained deliverables are much easier to implement fully asynchronously, reducing overhead
    - Typical risk mitigation for estimates is to increase them artificially; resources that could be used for more honest development
- Allow for extending the timeline without budget cuts
    - In case this is already how it works, it needs to be communicated more clearly
- Make the long-term and maintenance cost imposed on the open source component a selection criterion
    - If you can't fund ongoing maintenance, which is reasonable, ensure it's not being made more expensive by the work you fund
    - Ideally all funded work should always make maintenance and contributions less expensive, because that's rarely done by volunteers

## In 2-3 sentences, please describe the achievements resulting from your team’s participation in the Contribute Back Challenges for a general audience. Please be aware that your response to this question might be published by STF as part of our external communication strategy. (150 words)

NixOS now has all pieces of the puzzle to offer security features superior to most other Linux distributions and at least en par with commercial offers, while preserving the ease and freedom of customisation NixOS has always been known for.
Completing this project has shifted our concern from purely remediation to prevention of security incidents.
With the proper tooling in place, we can now tap into the collective energy and intellect of thousands of contributors to solve ever larger problems within and outside of our growing and maturing community.

# Credits

This project is carried out by (in ASCIIbetical order):

@DMills27
@ElvishJerricco
@JulienMalka
@RaitoBezarius
@Samyak2
@alejandrosame
@cidkid
@emilytrau
@fricklerhandwerk
@jfly
@lheckemann
@lilyinstarlight
@mightyiam
@modprog
@nikstur
@raboof
@thubrecht
