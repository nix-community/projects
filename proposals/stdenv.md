# Nixpkgs `stdenv` documentation – Sovereign Tech Fund

## What open source infrastructure component would you like to contribute to? Please provide more details.

[Nix](https://nix.dev/) is an open source build system, configuration management system, and mechanism for deploying software, focused on reproducibility. It is the basis of an ecosystem of exceptionally powerful tools – including Nixpkgs, [the largest, most up-to-date software repository in the world](https://repology.org/repositories/graphs), and NixOS, a Linux distribution that can be configured fully declaratively, with unmatched flexibility. For its proponents, Nix embodies technology sovereignty. It is leveraged and relied upon by computer enthusiasts, professionals, and organisations who recognise its value for all steps in the software development lifecycle.

The particular component this project aims to improve is the documentation for the [Standard Environment](https://nixos.org/manual/nixpkgs/unstable/#part-stdenv) and [Build Helpers](https://nixos.org/manual/nixpkgs/unstable/#part-builders) in Nixpkgs. The standard environment forms the technical foundation for the massive package collection, and is augmented by build helpers that allow packaging software from various [language ecosystems](https://nixos.org/manual/nixpkgs/unstable/#chap-language-support) and reliably [cross-compile](https://nixos.org/manual/nixpkgs/unstable/#chap-cross) software. These areas are at the core of Nix’s unique strengths, and the daily driver of developers leveraging Nixpkgs to secure repeatable production of artefacts.

## Why is this technology critical? Please explain to us the relevance of this technology.

This year Nix has seen its 20th anniversary. We estimate the community to consist of 100 mostly volunteer developers, 2 000 contributors, more than 15 000 active users, and 100 companies using and relying on Nix. [Recent social media activity](https://www.youtube.com/watch?v=fuWPuJZ9NcU) reaches on the order of 100 000 people. The Nix ecosystem is on an [exponential growth trajectory](https://ossinsight.io/analyze/NixOS/nixpkgs#overview) in terms of user adoption and development activity at the periphery.

Nix has the potential to become a default in the software development tool stack, by drastically reducing the time required to start working on software development projects – written in any language – and the cost of maintaining and sharing build setups and development environments. These can build on top of Nixpkgs, which today supplies the largest collection of free software in existence ready for use. Packages and services can be configured and deployed through NixOS more flexibly, reliably, efficiently than with any comparable tool. The Nix ecosystem can enable almost indefinite reproducibility of builds and configurations: [Nix and legacy enterprise software development: an unlikely match made in heaven](https://talks.nixcon.org/nixcon-2022/talk/QQPBFW/).

It serves as the platform accelerating and keeping usable countless software experiments that would otherwise be intractable or have long become inaccessible as their environments grow past them.

Moreover, the public [Nix binary cache](http://cache.nixos.org/) provides operational software artefacts from more than a decade back, some of which cannot be obtained otherwise any more.

In short, Nix reduces the global cost of software production and long-term use by a tangible amount.

## Please provide a brief overview over your project’s dependencies, including your own dependencies and projects that rely on your technology.

Dependencies:

- Various C++ compilers
- Bash
- Curl
- OpenSSL
- Various GNU projects
- Rust
- Python
    - Sphinx, Kramdown

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

## Who benefits from this technology and the improvements or contributions? Which target groups does your project address (who are its users?) and how do they benefit from the funding (directly and indirectly)?

Tools in the Nix ecosystem are primarily suited to professional software developers and computer enthusiasts (many of which are students), but are also known to support scientific work, and are used as a foundational technology and force multiplier in a multitude of organisations and commercial enterprises. All these are direct or indirect beneficiaries of improved developer-oriented documentation, through reduced onboarding time, learning effort, and costs of solving common problems, which overall reduces the cost of software development.

The NLnet Foundation is partnering with the NixOS Foundation to leverage Nix’s capabilities for providing sustainably accessible software under the umbrella of the Next Generation Internet initiative of the European Commission. This year, the third instalment of the [Summer of Nix](https://github.com/ngi-nix/summer-of-nix/) program will be held, making even more software available through Nix and upskilling dozens of participants (see also the [website](https://web.archive.org/web/20220927101525/https://summer.nixos.org/) and [documentation program](https://discourse.nixos.org/t/summer-of-nix-documentation-stream/20351) announcement for 2022). Better reference documentation of Nixpkgs build tooling can be expected to also tangibly reduce the cost of training and development work for the next two years’ programs, which are already funded.

## How are decisions regarding this technology’s development made? Please describe the project’s governance model.

Individuals and loosely organised contributor or maintainer teams review each other’s work and discuss technical decisions in public. Despite the principal author technically being a BDFL, there are only weak and implicit power structures that are largely centered around demonstrated achievements, and decisions largely are based on technical merit as judged by those involved.

Self-organised formal [community teams](https://nixos.org/community/#governance-teams) take responsibility for maintaining code in their areas of expertise, and have a more formal communication and permission structure. Otherwise, apart from more regular activity, they operate just like any other group of contributors.

Ecosystem-wide technical decisions are negotiated in an [RFC process](https://github.com/NixOS/rfcs/).

The NixOS Foundation mainly ensures funding for critical assets such as the binary cache, manages permissions in the GitHub organisation, and facilitates community activities. The Foundation board as a legal entity is not involved in technical decisions.

## How does this project handle security risks? Are there policies, procedures, or tools in place to minimize the introduction of vulnerabilities or undesired contributions?

There exists a [security team](https://nixos.org/community/teams/security.html) and an [infrastructure team](https://nixos.org/community/teams/infrastructure.html) tending to critical assets. [Security-relevant issues and pull-requests](https://github.com/NixOS/nixpkgs/labels/1.severity%3A%20security) are automatically tagged by a [vulnerability tracking system](https://github.com/nix-community/vulnix/).

Different components have different ownership structures. For Nix itself, only maintainers have write access, and only the principal author can publish releases. Nixpkgs and NixOS have a much broader committer community with largely implicit rules. There is a high degree of social trust involved, and active developers and maintainers, while culturally and geographically diverse, usually have ongoing working relationships marked by diligent reviews and critical discussions. 

## How will you address the challenge described? Give an overview of your work and why it is significant, specifically addressing the challenge. Explain what the field will learn from your proposed work and how it contributes to the long-term sustainability of the technology.

In the past, Nix gained an unfortunate reputation of having a steep learning curve and unhelpful documentation. The Nix documentation team was [established in mid 2022](https://discourse.nixos.org/t/documentation-team-flattening-the-learning-curve/20003) in order to ease learning Nix for beginners and support community efforts in that direction. In the past months the team has gathered many active contributors following a [call for maintainers](https://discourse.nixos.org/t/documentation-team-call-for-maintainers/25970), and successfully ran a [fundraiser to support a focused project](https://opencollective.com/nixos/projects/documentation-project) aiming to improve the onboarding experience for new users. This is testimony that users are invested in the ecosystem, care for better documentation, and trust maintainers to execute on their plans.

While the mentioned chapters in the Nixpkgs manual are central to the entire ecosystem and critically important early on in user onboarding, they are by far the weakest parts of documentation and a clear hindrance to adoption – well known among new users, contributors, and maintainers for lack of crucial information, poor discoverability, and densely written text full of unfamiliar concepts and terminology (to the point of being the subject of [elaborate mockery](https://ianthehenry.com/posts/how-to-learn-nix/)). Most importantly, this part of documentation is **effectively unmaintained** as currently no one has the resources to take ownership.

Nixpkgs is a large software project, and one of the largest public GitHub repositories. The code itself originated from research projects in [2004](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwi5o8mAwOn_AhWBS_EDHRolCnQQFnoECA4QAQ&url=https%3A%2F%2Fedolstra.github.io%2Fpubs%2Fnspfssd-lisa2004-final.pdf&usg=AOvVaw10O4UewT2sh6kUSXYR3jNC&opi=89978449) and [2006](https://nixos.org/docs/SCR-2005-091.pdf), and albeit always serving its purpose, for various reasons has grown without clear direction since and saw, at best, sparse efforts to provide approachable documentation. It is [notoriously difficult to read and navigate](https://discourse.nixos.org/t/where-is-callpackage-defined-exactly-part-2/12524), only understood well by a few people, and attempts at documenting it appropriately proved extraordinarily difficult: On the one hand, deep contextual knowledge is required to fully grasp it. On the other hand, the existing documentation is ill-structured, but relied-upon by many users and must therefore not change in ways such that important information is lost. The documentation team is now at a crucial point where we have built up enough capacity, expertise, and community support to tackle the skill-based problem of producing correct and helpful documentation and presenting it in appropriate locations; we also have built up enough organisational structures and routines to deal with the coordination problem of incrementally reorganising a large information system in a division of labor.

This project aims for a complete revision of the [Standard Environment](https://nixos.org/manual/nixpkgs/unstable/#part-stdenv) and [Build Helpers](https://nixos.org/manual/nixpkgs/unstable/#part-builders) chapters in the Nixpkgs manual. We will employ techniques and tactics that have proven successful in past activities, and build on our experience with the particularities of the technology and community:

- Diligently survey existing first- and third-party documentation
- Work incrementally on many small changes
- Work in pairs or small teams
- Distribute high-context and low-context tasks according to level of expertise and availability
- Improve processes as we go, so others can follow more easily
- Plan for enough review capacity among project participants
- Involve maintainers and experts for reviews and consultation
- Run usability studies for validation
- Share knowledge and provide opportunities for volunteers to contribute

Specific goals are, roughly in order of importance:

- Survey and take inventory of key issues
- Clarify key concepts, mechanisms, and common use cases
- Improve structure and language
- Ensure that the entire API surface is visible
- Increase discoverability and cross-linking
- Provide examples
- Plan and implement renamings as needed
- Augment contribution guides
- Improve visual presentation
- Improve development infrastructure and workflows for documentation
    - Automatic testing of examples
    - Stable URLs and automatic redirects
    - Better automatic rendering of in-code comments
- Improve contributor experience as the need arises

Since these manual chapters are currently unmaintained and (to our knowledge) there exists no person who knows them completely, a significant part of the initial work will consist of reading source code, mapping out concepts and key use cases, as well as planning and coordinating changes. It will be followed by work on correctly representing concepts (which cannot be parallelised) and improving superficial structure and language (which can be parallelised well). This will likely be accompanied by deep structural changes once the team gets more into the context. This is how we proceed in our ongoing project concerning the learning materials, and this is consistently leading to satisfying results at the pace our funding allows.

Given the situation has many unknowns, the work has characteristics of a research project to the extent that while we are sure to make progress and tangible improvements by doing what we usually do, just a lot more of that, it’s impractical to determine concrete deliverables and we deem it silly to invent artificial success metrics such as “number of cross-links”. While we do have experience with user testing, it is an expensive technique that we would use sparingly.

The Nix documentation team has a track record of achieving substantial improvements over long stretches of time-constrained work, which we document in various reports, for example:

- [This Month in Nix Docs – April 2023](https://discourse.nixos.org/t/this-month-in-nix-docs-2-april-2023/27899)
- [Tweag+Nix dev update #47 (also covering documentation)](https://discourse.nixos.org/t/tweag-nix-dev-update-47/27387#documentation-2)
- [Nix team report 2022-10 — 2023-03 (also covering documentation)](https://discourse.nixos.org/t/nix-team-report-2022-10-2023-03/27486#documentation-14)
- [Four months into the Nix Book](https://www.tweag.io/blog/2022-09-29-the-nix-book-report/)

### What the field will learn from our work

With support of the NixOS Foundation, the Nix documentation team not only works on improving technical documentation and creating educational content, but also continues driving organisational maturity of the ecosystem by setting examples of running community-driven teams [fully in the open](https://discourse.nixos.org/c/dev/documentation/25) and connecting domain experts with new users and contributors. We hope that with carrying out a large project, we can demonstrate

- public collaboration across organisational boundaries on a valuable shared resource
- application of best practices in developer-focused documentation in a realistic setting

to the wider open source and software development community.

### How our work will contribute to sustainability of Nix and Nixpkgs

Software developers are a broadly agreed-upon target audience for Nix community teams: Keeping the ecosystem on a healthy trajectory while keeping to established stability standards requires highly specialised knowledge, and attracting volunteer talent is critical for sustaining maintenance and development of core components. This project will contribute to solving part of the succession problem in the Nix ecosystem, both by reducing effort and friction for existing users and contributors, and by increasing attractiveness to new users who may become contributors and eventually graduate to take on maintainer responsibility. Making Nix and Nixpkgs more approachable and easier to use will also make it more likely for organisations to adopt the technology, and in turn invest resources to support ongoing development, as we have already observed in the past year.

## How will you accomplish the work? Please provide a list of deliverables with associated effort and cost of each deliverable.

- 2 senior engineers, responsible for the project (2\*40h/w = 2\*80 person-days, 128 000 EUR)
- 2 junior engineers (2\*40h/w = 2\*80 person-days, 102 400 EUR)
- Maintainer reviews and consultation (10h/w = 160h, 16 000 EUR)
- Lectorate (9600 EUR)
- Development, execution, and evaluation of usability studies (100h, 6 000 EUR)
- Administrative support (4h/w = 64h, 5 120 EUR)

Explanation:

From our immediate experience, adding more inexperienced contributors does not increase velocity (see [Brooks’s law](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiX44eR4-n_AhXBVvEDHYYsDh0QFnoECA4QAQ&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FBrooks%2527s_law&usg=AOvVaw3VUN9Zx_P-5BEAAKFqcjfK&opi=89978449)). The bottleneck are always reviews for conceptual and technical correctness, and those can only be done effectively by experts, and are made easier with high-quality contributions. We deem it most sensible to let people collaborate on that narrow subject who already have years of practice in their respective domain, know each other well, and can be trusted to autonomously execute according to the project’s goals. The documentation team has close ties with companies involved in the Nix ecosystem, with access to a small pool of experienced developers who would fit the requirements for this task.

While the effort can be scaled down dynamically, we should ensure a team size of 3-4 people and an engagement that is closer to full-time than to half-time. For we also know from experience that it will be almost impossible to staff such a project for a 20h/w engagement, and fewer than 3 fully engaged participants will be blocked on reviewing each others’ and volunteer contributors’ work (which can be expected to continue flowing in).

## Describe your relationship to the maintainers of this technology. Are you yourself the maintainer? Do they know you plan to do this work and do they support it? Please tell us more about how you obtained their support and how you plan to work together to make sure your contributions are accepted.

This project proposal was developed and written collaboratively by the Nix documentation team, which is responsible for all official Nix documentation (but due to resource constraints only maintaining a small part of it in practice). I am founding member and current lead of the documentation team, and also participate in the Nix maintainers team. The problems outlined here are well known to all maintainers, and solutions have been discussed in the past and up to recently without action. Fundraising activities are agreed upon.

Preprations for the grant applications were [announced in the community forum](https://discourse.nixos.org/t/german-federal-funding-for-foss-development/29036/4).

Some Nix maintainers are also on the NixOS Foundation board, who is in general support of fundraising for development activities. I am also contracting for the NixOS Foundation to help with project management. Maintainers and board members are invested in the project through the companies they run or work for, so collaboration can be expected to continue indefinitely.
