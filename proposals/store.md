# Nix Store - Sovereign Tech Fund

## What open source infrastructure component would you like to contribute to? Please provide more details.

[Nix](https://nix.dev/) is an open source build system, configuration management system, and mechanism for deploying software, focused on reproducibility.
It is the basis of an ecosystem of exceptionally powerful tools – including Nixpkgs, [the largest, most up-to-date software repository in the world](https://repology.org/repositories/graphs), and NixOS, a Linux distribution that can be configured fully declaratively, with unmatched flexibility.
For its proponents, Nix embodies technology sovereignty.
It is leveraged and relied upon by computer enthusiasts, professionals, and organisations who recognise its value for all steps in the software development lifecycle.

This project’s goal is to systematically expose to application developers the very core of the Nix ecosystem: the Nix store.
The store implements the [purely functional software deployment model](https://edolstra.github.io/pubs/phd-thesis.pdf):
It deals with files in a file system like a modern computer program deals with objects in memory, by ensuring [referential integrity](https://en.m.wikipedia.org/wiki/Referential_integrity), and enabling garbage collection and transparent caching.
It allows handling software builds like pure (that is, side-effect-free) computations in a declarative programming language.

The store is the oldest and central component of Nix, and is written in C++.
Today it has some involved machinery like a build scheduler, a daemon for clients to interact with, and multiple custom communication and data transfer protocols.
Over time it has evolved into an abstract interface with multiple implementations for different use cases (such as a store that only serves as a remote binary cache that cannot perform builds).
Yet, it was always closely tied to the other layers of Nix, and cannot be used in isolation or interfaced with programmatically except through the command line and undocumented binary protocols.
This project aims to change that, enable developers to conveniently build independent applications that are compatible with the existing Nix ecosystem, and get [the powerful idea behind Nix](https://www.tweag.io/blog/2022-07-14-taming-unix-with-nix/) into the hands of even more computer users.

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

The Nix store is what all of that builds upon, and the entire ecosystem relies almost exclusively on the C++ implementation bundled with the Nix binaries.
Guix, an early fork of Nix which is more popular than Nix in the scientific community these days, has [its own store](https://guix.gnu.org/manual/en/html_node/The-Store.html) that follows the same paradigm but is not fully compatible.
A group of developers is actively working on a fully compatible Nix re-implementation called [Tvix](https://code.tvl.fyi/tree/tvix).

## Please provide a brief overview over your project’s dependencies, including your own dependencies and projects that rely on your technology.

Nix dependencies (see [all dependencies](https://nixos.org/manual/nix/unstable/installation/prerequisites-source.html)):

- GCC, Clang
- GNU Autoconf, GNU Make
- Bash
- cURL
- OpenSSL
- SQLite
- Boost
- Brotli
- Bison, Flex
- GoogleTest, RapidCheck
- Rust, mdBook

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

The Nix store in particular is largely invisible infrastructure for all these users.
But there is a significant untapped potential for application developers that currently cannot effectively leverage the store without buying into all of Nix and working around its outer layers and their accidental complexities.
The Nix store is a very generic mechanism that could be used for a broad spectrum of applications.
Examples include language-specific package managers or continuous integration pipelines – anything that could make use of persisting data in a file system and transforming it with Unix processes in a tightly controlled manner, with all the benefits of the development effort put into Nix, such as distributed builds, caching, deduplication, compatible services and infrastructure, etc.

Exposing and documenting the store APIs and protocols would also allow steps to get closer to compatibility with Guix (which would allow the projects to share build recipes and artefacts) and eventually other systems that have similar approaches to working with immutable linked data, such as IPFS or Git.

The NLnet Foundation is partnering with the NixOS Foundation to leverage Nix’s capabilities for providing sustainably accessible software under the umbrella of the Next Generation Internet initiative of the European Commission.
It also funds numerous projects building on top of Nix to provide better tools for FOSS developers.
A separately accessible Nix store could serve as a reliable building block for the software innovation efforts fostered in that program.

## How are decisions regarding this technology’s development made? Please describe the project’s governance model.

Individuals and loosely organised contributor or maintainer teams review each other’s work and discuss technical decisions in public.
Despite the principal author technically being a [BDFL](https://en.wikipedia.org/wiki/Benevolent_dictator_for_life), there are only weak and implicit power structures that are largely centered around demonstrated achievements, and decisions largely are based on technical merit as judged by those involved.

Self-organised formal [community teams](https://nixos.org/community/#governance-teams) take responsibility for maintaining code in their areas of expertise, and have a more formal communication and permission structure.
Otherwise, apart from more regular activity, they operate just like any other group of contributors.

Nix itself is currently [maintained by a team of six people](https://github.com/NixOS/nix/tree/master/maintainers#members) including principal author, who meet twice a week to discuss technical decisions and review contributions.

Ecosystem-wide technical decisions are negotiated in an [RFC process](https://github.com/NixOS/rfcs/).

The NixOS Foundation mainly ensures funding for critical assets such as the binary cache, manages permissions in the GitHub organisation, and facilitates community activities.
The Foundation board as a legal entity is not involved in technical decisions.

Project governance has immensely gained in structure lately: In the past year, four of the eleven currently active community teams were formed, the NixOS Foundation board was restructured, and there exist plans for setting up paid support functions to ensure continued operations.

## How does this project handle security risks? Are there policies, procedures, or tools in place to minimize the introduction of vulnerabilities or undesired contributions?

There exists a [security team](https://nixos.org/community/teams/security.html) and an [infrastructure team](https://nixos.org/community/teams/infrastructure.html) tending to critical assets.
[Security-relevant issues and pull-requests](https://github.com/NixOS/nixpkgs/labels/1.severity%3A%20security) are automatically tagged by a [vulnerability tracking system](https://github.com/nix-community/vulnix/).

Different components have different ownership structures.
For Nix itself, only maintainers have write access, and only the principal author can publish releases.
Nixpkgs and NixOS have a much broader committer community with largely implicit rules.
There is a high degree of social trust involved, and active developers and maintainers, while culturally and geographically diverse, usually have ongoing working relationships marked by diligent reviews and critical discussions.

## How will you address the challenge described? Give an overview of your work and why it is significant, specifically addressing the challenge.

Explain what the field will learn from your proposed work and how it contributes to the long-term sustainability of the technology.

Among Nix contributors, the C++ codebase is known to be labyrinthene.
It has grown over 20 years after starting out as a research project and then being extended incrementally, subject to many different interests, and always under severe resource constraints.
Yet, it supports an entire ecosystem that is quickly growing, and most its users perceive Nix itself and its development as essentially inaccessible.

Improving factoring, testing, and documentation of the Nix store, the core component, will substantially ease the contributor experience, by

- Easing code navigation
- Making changes, especially large ones, less risky
- Reducing build times
- Clarifying behavior and intent, decoupled from the concrete implementation

Already the very fact of a concerted effort with multiple people involved will act as a forcing function to share and document tacit knowledge, and to communicate activities and outcomes with a broader audience of potential contributors.

The primary benefit we see is that better test coverage will enable future refactorings to address long-standing technical issues.
Those are currently impractical due to the risks of breaking widely used interfaces in subtle ways, which is unacceptable given the reliance on Nix’s reproducibility guarantees.

Providing the Nix store as a building block to application developers will allow for experimentation and innovation, both in the Nix ecosystem as well as in the wider software development community.
Being able to build on top of the Nix store will allow software projects (with a suitable architecture) to plug it as a highly reliable and well-supported backend for common tasks around dependency management and data persistence, reducing duplication of work at low risk.

Finally, broader adoption and better understanding of the underlying ideas will likely spur yet-unknown approaches to significant problems in practical software development.

### What the field will learn from our work

Nix puts forward a unique (indeed, we claim, revolutionary) approach to software development to begin with.
One can argue that it is still somewhat obscured for various reasons, and one of them is that the core mechanisms are hidden away as an implementation detail.

Clarifying concepts by formalising and documenting interfaces would enable others to build on top of, reimplement, or innovate over what Nix has to offer, and help spread its ideas beyond the currently entrenched but limited notion of a package manager and beyond the particular implementation angle the Nix ecosystem has taken.

### How our work will contribute to sustainability of Nix, the Nix ecosystem, and FOSS more generally

Opening up the Nix store specification for alternative implementations will foster competition for code quality and performance, make the ecosystem less reliant on any one implementation, and drive innovation while incentivising keeping existing interfaces stable.
Both aspects are major concerns for Nix users: Nix is well-known for its stability guarantees but also has some notorious performance bottlenecks.

Well-defined interfaces, accompanying documentation, and a more comprehensive test suite will ease learning and adoption for developers, making quality contributions more likely.
That would reduce maintainers’ work load and contribute to making the maintainer role more appealing; having a separate component as a domain of ownership would also help with managing responsibilities and expectations in the long run.

## How will you accomplish the work? Please provide a list of deliverables with associated effort and cost of each deliverable.

- Inventorise and document the intent of existing tests (2w, 8 000 EUR)
- Set up CI to report on test coverage (2w, 8 000 EUR)
- Split out `libstore` to be self-contained (3w, 12 000 EUR)
- Provide a separate installer (3w, 12 000 EUR)
- Rework the documentation infrastructure to produce a separate reference manual (3w, 12 000 EUR)
- Add C bindings to the store API (3w, 12 000 EUR)
- Add Python, Rust, Go, and Haskell bindings around the C API (3w, 12 000 EUR)
- Derive unit tests from existing integration test cases (4w, 16 000 EUR)
- Set up a maintainable integration testing framework for daemon interactions (4w, 16 000 EUR)
- Document the test setup, such that it is easy to extend even for drive-by contributors (4w, 16 000 EUR)
- Document architecture, formats, and protocols in the manual (4w, 16 000 EUR)
- Set up a test suite for backend protocols (2w, 8 000 EUR)
    - Wire format (NAR, daemon)
    - NAR parser
    - `.narinfo` parser/encoder
- Add/finish Rust implementation of protocols to test against the C++ implementation (4w, 16 000 EUR)
- Implement an HTTP binary cache service in Rust as a demonstrator (3w, 12 000 EUR)
- Add a Nix store backend to [Haskell Cabal](https://hackage.haskell.org/package/Cabal) as a demonstrator (4w, 16 000 EUR)
- Administrative support (8000 EUR)

Explanation: 240 person days, 200 000 EUR

The working mode we envision based on experience is to allocate a significant portion of time for reviews – for code quality and consistency, as a vehicle for knowledge sharing, and to ensure high standards for documentation.
This is incorporated in the estimates.

Nix maintainers essentially have to buy their employers’ time or take compensation that can compete with other engagements; known contributors who could do the bulk of the work are in a similar situation or otherwise would need substantial time for onboarding.
Therefore we have to assume consultancy rates to be able to keep to the time frame, with the option to trade budget for velocity to some extent.

We expect multiple contributors to work in parallel where possible.

## Describe your relationship to the maintainers of this technology. Are you yourself the maintainer? Do they know you plan to do this work and do they support it? Please tell us more about how you obtained their support and how you plan to work together to make sure your contributions are accepted.

I am a member of the [Nix maintainers team](https://discourse.nixos.org/t/nix-team-creation/22228).
This project proposal was developed and written collaboratively by Nix maintainers and Tvix developers.
It aims to implement [RFC 134](https://github.com/nixos/rfcs/blob/master/rfcs/0134-nix-store-layer.md), which met broad consensus as crucial for maintaining and developing the Nix ecosystem at scale, but currently has no perspective of being implemented due to lack of resources we can allocate to sustainability measures such as testing, refactoring, and contributor-oriented documentation.
Maintainers only have capacity to review and shepherd contributions following settled design decisions, and are committed to that task as is evidenced by our [meeting minutes](https://discourse.nixos.org/search?q=Nix%20team%20meeting%20minutes%20%23%20%23dev%3Anix%20order%3Alatest_topic) and our [first half-yearly report](https://discourse.nixos.org/t/nix-team-report-2022-10-2023-03/27486).

We have explicit support by Cabal maintainers to add the Nix store backend, and the Nix community has a lot of ties and overlap with the Haskell community.
The demonstrators and protocol implementations can live independently of the Nix codebase.

Preparations for the grant applications were [announced in the community forum](https://discourse.nixos.org/t/german-federal-funding-for-foss-development/29036/4).

We plan to follow our established routine to review and merge contributions, with three maintainers who can allocate dedicated time when paid, specialising in the store implementation and documentation, and three available in the maintainer meetings for consultation.
Work that can get merged outside of the Nix repository can move more quickly and would be accompanied by cross-team communication efforts as needed.
