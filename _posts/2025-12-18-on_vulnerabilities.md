---
layout: default
title: On Vulnerabilities
permalink: /vulnerabilities
---

# On Vulnerabilities

Computer vulnerabilities are all around us, largely by design. The entire infrastructure that powers modern computing and the digital environment is built on legacy systems that prioritized connectivity, often at the expense of security. In other words, security was never a priority - it was secondary to the goal of connecting computer systems.

The internet as we know it today was first an intranet, called ARPANET. It was built in the late 1960s, with funding from the US Department of Defense's Advanced Research Projects Agency, by academics, for academics and military planners, in order to provide some kind of redundancy if the USA were nuked by its enemies. Thus a distributed communication system was born which connected massive computers, originally housed in universities and military installations across the USA, together.

It’s here, in 1969, that researchers began to develop the protocols that underlie and direct the internet today. One could not simply develop and proliferate a new protocol, even with the consensus of peers and the support of the academic community - there was also oversight from ARPA, and the workaround here was to set up a working group and publish technical documents that were theoretically meant to be approved by senior officials. The irony is that there was a gulf of knowledge between these researchers and senior officials, thus there was little way of judging the efficacy of proposed changes to the early internet. So the working group came up with a workaround: push forward the changes, but provide senior officials a way to voice an objection; this took the form of RFC’s (Requests For Comment) - a series of documents submitted to senior officials by which they could ‘comment’ on any proposed changes. This was of course exceedingly rare, and most of the time the proposed changes would proceed with no objections.

There are some further considerations. Hardware was prohibitively expensive in the 70s and 80s, and this had a number of second-order effects:

1. Personal computers weren’t exactly a thing, at least not for the layman, so the internet was a smaller tight-knit community i.e. a high-trust environment, obviating the need for security.

2. Security solutions for networking relied on cryptographic operations, but these were far too computationally intensive and often required dedicated hardware accelerators that were expensive and niche, thus it rendered security impractical amid the priority for fast and effective communication.

It was in this environment, with these constraints, that the legacy protocols such as TCP/IP, UDP, DNS, and others were built. The most pressing issue is that these protocols assume a trusted environment; they do not really have any built-in security. Security solutions developed in later decades such as TLS, IPsec, DNSSEC, and so on are simply add-ons retrofitted on to these old protocols. This works, but all these technical layers and integrations massively increase complexity, which translated to new, sophisticated vulnerabilities like Log4Shell.

One abstraction that will serve to explain this further is the OSI model - a conceptual framework academics use to understand network protocols and how their interact with one another.

| Layer | Name | Common Vulnerabilities/Attacks |
|-------|-------------------|------------------------------------------------------------------------------------------------|
| 7 | Application | SQL injection, cross-site scripting (XSS), buffer overflows, application-level exploits |
| 6 | Presentation | Data format manipulation, encryption mismatches, MIME type exploits |
| 5 | Session | Session hijacking, man-in-the-middle (MITM) attacks |
| 4 | Transport | SYN flooding, TCP/UDP port scanning, connection hijacking |
| 3 | Network | IP spoofing, ICMP attacks (e.g., ping of death), routing attacks (e.g., BGP hijacking) |
| 2 | Data Link | ARP spoofing/poisoning, MAC flooding, VLAN hopping |
| 1 | Physical | Wiretapping, hardware tampering, supply chain backdoors, electromagnetic interference |

This framework illustrates how, at every layer, there exist vulnerabilities. Packets can be intercepted, potentially decrypted/read, modified, copied and stored (to be decrypted later), and so on. Modified packets, or modification of the behavior of unmodified packets, can be used to materially affect layers - even the physical (hardware) layer!

The issue with layering tools, technologies, protocols, and systems on top of one another is that it assumes that the layers above and below are working as intended - that is, that they are secure. This assumption is often proven wrong. The physical layer is a frequent target by nation state actors - the NSA (USA) wire taps under sea cables, China builds backdoors into hardware that they sell abroad, and so on.
But the widest attack surface, and also the most accessible, is found in Layers 2 through 7. There are many creative feats of engineering to bring about Layer 1 (Physical i.e. hardware) vulnerabilities, but these often require specialist knowledge, advanced cross-team functionality and, for all the best exploits, for governments to coerce manufacturers. In short - there exist, at every level, opportunities for vulnerabilities to be discovered and chained together. 
One mental image that helps me think about vulnerabilities is a brick wall - the larger the wall, the larger the attack surface, and the more chance that you’ll find a missing brick, or be able to chip away at some of the cement, or plant a false removable brick; and that chaining these vulnerabilities is like knocking down small parts of the wall one at a time until it collapses.

Human factors play a part, too. All these things are ultimately built and put together by people. These people may be fatigued, lack sufficient technical understanding, misunderstand or misinterpret instructions, or quite simply ignore them in lieu of ‘getting things done’ due to management pressure or a simple desire to achieve their design objectives no matter how, at the expense of security. That is to say, we often exacerbate existing issues, and create an opportunity for novel vulnerabilities, particularly those that are chained and leverage misconfigurations or, as mentioned earlier, rely on the false assumption of all supporting infrastructure being secure.

And so it came to be that vulnerabilities are unavoidable. They are structural, systemic, systematic, in the sense that they always have been, and always will be. This despite our best efforts, despite the millions of man hours put into securing these systems, despite the neverending deluge of vulnerabilities exploited every year, both small and large, both known and unknown. This isn’t something that can be avoided - it can be mitigated, but mitigations expand complexity and introduce new risks. This is not to suggest that we should accept things as they are, no; we should strive towards security while being mindful of the harsh truth that perfect security is unattainable, and that we all share the inherited burden of legacy systems. Nonetheless, we should all play our part and do our best to contribute to a more secure future.
