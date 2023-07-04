# Frequently Asked Questions

## What is Nix?

Asked by:
- [Sovereign Tech Fund](https://sovereigntechfund.de/en/challenges/)

[Nix](https://nix.dev/) is an open source build system, configuration management system, and mechanism for deploying software, focused on reproducibility.
It is the basis of an ecosystem of exceptionally powerful tools – including Nixpkgs, [the largest, most up-to-date software repository in the world](https://repology.org/repositories/graphs), and NixOS, a Linux distribution that can be configured fully declaratively, with unmatched flexibility.
For its proponents, Nix embodies technology sovereignty.
It is leveraged and relied upon by computer enthusiasts, professionals, and organisations who recognise its value for all steps in the software development lifecycle.

## Why is Nix relevant?

Asked by:
- [Sovereign Tech Fund](https://sovereigntechfund.de/en/challenges/)

This year Nix has seen its 20th anniversary.
We estimate the community to consist of 100 mostly volunteer developers, 2 000 contributors, more than 15 000 active users, and 100 companies using and relying on Nix.
[Recent social media activity](https://www.youtube.com/watch?v=fuWPuJZ9NcU) reaches on the order of 100 000 people.
The Nix ecosystem is on an [exponential growth trajectory](https://ossinsight.io/analyze/NixOS/nixpkgs#overview) in terms of user adoption and development activity at the periphery.

Nix has the potential to become a default in the software development tool stack, by drastically reducing the time required to start working on software development projects – written in any language – and the cost of maintaining and sharing build setups and development environments.
These can build on top of Nixpkgs, which today supplies the largest collection of free software in existence ready for use.
Packages and services can configured and deployed through NixOS more flexibly, reliably, efficiently than with any comparable tool.
The Nix ecosystem can enable almost indefinite reproducibility of builds and configurations:
[Nix and legacy enterprise software development: an unlikely match made in heaven](https://talks.nixcon.org/nixcon-2022/talk/QQPBFW/).

It serves as the platform accelerating and keeping usable countless software experiments that would otherwise be intractable or have long become inaccessible as their environments grow past them.

Moreover, the public [Nix binary cache](http://cache.nixos.org/) provides operational software artefacts from more than a decade back, some of which cannot be obtained otherwise any more.

In short, Nix reduces the global cost of software production and long-term use by a tangible amount.

## Who uses Nix?

Asked by:
- [Sovereign Tech Fund](https://sovereigntechfund.de/en/challenges/)

A selection of projects and companies depending on Nix, Nixpkgs, or NixOS:

- [Replit](https://blog.replit.com/nix)
- [Shopify](https://shopify.engineering/shipit-presents-how-shopify-uses-nix)
- [Cachix](https://www.cachix.org/)
- [flox](https://floxdev.com/)
- [INRIA’s Grid’5000 computing cluster](https://nix-tutorial.gitlabpages.inria.fr/nix-tutorial/index.html)
- [Haskell Stack](https://docs.haskellstack.org/en/stable/nix_integration/)
- [The European Commission’s IT department](https://www.youtube.com/watch?v=I7wdcJ3YhoU)
- Various [scientific projects](https://www.youtube.com/watch?v=SjjEDTccpQA)
- A plethora of [community projects around Nix](https://github.com/nix-community/)

## Who benefits from improvements and contributions to the Nix ecosystem?

Asked by:
- [Sovereign Tech Fund](https://sovereigntechfund.de/en/challenges/)

Tools in the Nix ecosystem are primarily suited to professional software developers and computer enthusiasts (many of which are students), but are also known to support scientific work, and are used as a foundational technology and force multiplier in a multitude of organisations and commercial enterprises.
All these are direct or indirect beneficiaries of improved developer-oriented documentation, through reduced onboarding time, learning effort, and costs of solving common problems, which overall reduces the cost of software development.

The NLnet Foundation is partnering with the NixOS Foundation to leverage Nix’s capabilities for providing sustainably accessible software under the umbrella of the Next Generation Internet initiative of the European Commission.
This year, the third instalment of the [Summer of Nix](https://github.com/ngi-nix/summer-of-nix/) program will be held, making even more software available through Nix and upskilling dozens of participants (see also the [website](https://web.archive.org/web/20220927101525/https://summer.nixos.org/) and [documentation program](https://discourse.nixos.org/t/summer-of-nix-documentation-stream/20351) announcement for 2022).
Better reference documentation of Nixpkgs build tooling can be expected to also tangibly reduce the cost of training and development work for the next two years’ programs, which are already funded.

## What is the governance model in the Nix ecosystem?

Asked by:
- [Sovereign Tech Fund](https://sovereigntechfund.de/en/challenges/)

Individuals and loosely organised contributor or maintainer teams review each other’s work and discuss technical decisions in public.
Despite the principal author technically being a BDFL, there are only weak and implicit power structures that are largely centered around demonstrated achievements, and decisions largely are based on technical merit as judged by those involved.

Self-organised formal [community teams](https://nixos.org/community/#governance-teams) take responsibility for maintaining code in their areas of expertise, and have a more formal communication and permission structure. Otherwise, apart from more regular activity, they operate just like any other group of contributors.

Ecosystem-wide technical decisions are negotiated in an [RFC process](https://github.com/NixOS/rfcs/).

The NixOS Foundation mainly ensures funding for critical assets such as the binary cache, manages permissions in the GitHub organisation, and facilitates community activities. The Foundation board as a legal entity is not involved in technical decisions.

## How does the project handle security risks? Are there policies, procedures, or tools in place to minimize the introduction of vulnerabilities or undesired contributions?

Asked by:
- [Sovereign Tech Fund](https://sovereigntechfund.de/en/challenges/)

There exists a [security team](https://nixos.org/community/teams/security.html) and an [infrastructure team](https://nixos.org/community/teams/infrastructure.html) tending to critical assets. [Security-relevant issues and pull-requests](https://github.com/NixOS/nixpkgs/labels/1.severity%3A%20security) are automatically tagged by a [vulnerability tracking system](https://github.com/nix-community/vulnix/).

Different components have different ownership structures.
For Nix itself, only maintainers have write access, and only the principal author can publish releases.
Nixpkgs and NixOS have a much broader committer community with largely implicit rules.
There is a high degree of social trust involved, and active developers and maintainers, while culturally and geographically diverse, usually have ongoing working relationships marked by diligent reviews and critical discussions.
