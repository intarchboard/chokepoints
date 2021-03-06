---
title: Internet Choke Points
docname: draft-iab-chokepoints-latest
date:
category: info

ipr: trust200902
area: IAB
workgroup: IAB
keyword: Internet-Draft

stand_alone: yes
pi: [toc, sortrefs, symrefs]

author:
 -
    ins: M. Nottingham
    name: Mark Nottingham
    organization:
    street: made in
    city: Prahran
    region: VIC
    country: Australia
    email: mnot@mnot.net
    uri: https://www.mnot.net/
 -
    ins: B. Trammell
    name: Brian Trammell
    organization:
    email: ietf@trammell.ch
    uri: https://trammell.ch


--- abstract

This memo discusses "choke points" in the Internet architecture and the governance structures surrounding them.

A choke point occurs where one single entity or a small number of entities have the ability to make decisions with wide-ranging or global impact some aspect of the use of the Internet.

We explore the implications these choke points have on the health of the Internet as a global communications infrastructure, and provide guidance for avoiding the creation of future choke points.

--- middle


# Introduction

[EDITOR'S NOTE: bring this up to date. keep the quote below but be a bit more Ripped From Today's Headlines ]

Recent events have caused concern about control of access to the Internet, leading one infrastructure company's CEO to reportedly assert:

> Literally, I woke up in a bad mood and decided someone shouldn’t be allowed on the Internet. No one should have that power.

In fact, the Internet is both architected and administered to preclude any one entity from having this power, through the careful management of “choke points” where such power could be exercised.


# Choke Points on the Internet

A large influence on the architecture of the Internet was [a need to survive nuclear attack](https://www.rand.org/content/dam/rand/pubs/papers/2008/P1995.pdf), so that loss of no one link or node would preclude communication overall. This desire for resilience is reflected in the modern Internet through measures like the [duplication of submarine internet links](https://submarine-cable-map-2018.telegeography.com).

Although in some places Internet access is at risk -- especially when there is not adequate diversity of access available -- the Internet as a whole has proven resilient in the face of such physical disruptions.

However, its resilience not limited to the physical components of the Internet; it also extends to the various services that Internet access depends upon, and the protocols that it uses. For example, there are [multiple DNS root servers](http://root-servers.org/), operated by a number of parties to provide protection from not only physical disruption, but also political and other disruption caused by such a vital service being controlled by one entity.

When any one component -- through its design or the constraints upon its use -- has the ability to deny access to the Internet (accidentally or not) or control its use, we call this a choke point.

Avoiding choke points is both a design goal for both the protocols and the services that make network access and operations possible, as well as an assumption made by each layer and service about its dependencies. The resilience and long-term health of the Internet depends on this assumption.

This does not mean that we can prevent all possible choke points; if a node has only one connection to the Internet, that link will be able to deny access no matter what measures we take. Instead, our aim is to avoid unnecessary choke points, especially when they can influence large portions of the Internet.

## More than Resilience

As John Gilmore said, “the internet interprets censorship as damage and routes around it.” Censorship and other forms of control relies on having an opportunity to exercise that control. Limiting the number of choke points and assuring that any unavoidable points are appropriately administered allows this valuable architectural property to persist.

This emergent property of the Internet has proven to be one of its core features. By providing resilient communication, it also provides [EDITOR'S NOTE: missing sentence end]

At the same time, the Internet’s composition as a network of independent networks is valuable; imposing unnecessary constraints upon them is to be avoided. However, this does not mean that internet infrastructure providers are without guidance; in particular we note that the UN’s [Guiding Principles on Business and Human Rights](http://www.ohchr.org/Documents/Publications/GuidingPrinciplesBusinessHR_EN.pdf) is an already-existing framework for businesses (including Internet infrastructure providers) to make such decisions within while still respecting human rights -- including the right to Internet access.


# Current Internet Choke Points

[EDITOR'S NOTE: IMO (brian) this is more useful if split by why the choke point emerges, not past/future. Not sure the list of subsections below is exhaustive.]

## End User Internet Access

There are now many ways for an end user to connect to the Internet. Mobile access over cellular radio (whether it be 2G, 3G, 4G or the emerging 5G) is extremely common worldwide, and fixed line access is available via multiple technologies -- twisted pair, coaxial cable, fibre -- in many places. Some networks also allow Internet access via point-to-point radio.

Satellite Internet is widely deployed in remote areas, and a number of low earth orbit constellations promise to provide it more universally and at lower latency than previously experienced in this media.

Despite this diversity of potential choices, obtaining access to the Internet remains a significant choke point.

In some jurisdictions, legal controls (whether in primary legislation or regulation) limit the diversity of access available, forming a regulated or de facto monopoly on Internet access at the physical, medium, or network layers.

An actor in control of an access chokepoint can exercise nearly total control over the Internet traffic of end users, and can also use it to gain bargaining power with Internet services that are not directly connected to the access network, because they effectively control some of that service's users.

Avoiding access chokepoints is a key focus of the network neutrality debate, and regulations in some countries to prevent or control the formation of access monopolies.

[Give examples -- e.g., US vs AU?]


## Internet Transit

The Internet is often defined as a 'network of networks'; the access networks that end users use need to connect to other networks (of various kinds, including other access networks) to provide Internet access.

backbones, tiers

Pay for access

Settlement

Peering


## Routing

Traffic between networks needs to be guided to its destination. In the Internet, this function is facilitated by routing protocols, most notably BGP.

BGP works by allowing a network to announce the networks that it can provide access to, so that its peers can choose to route through it if they desire. As such, it is a decentralised protocol; there is no single 'source of truth' for Internet routing.

However, while BGP cannot be used to control the entire Internet, it can be used to control some portion of it. By making false announcements, a network can deny access to or even re-route traffic of other networks illegitimately.

[Examples]

BGP security


## Naming

Most Internet applications use the Domain Name System (DNS) as a naming service. This avoids the need for end users to remember numeric IP addresses, and provides a layer of abstraction that services use for load balancing, failover, and other valuable operational tasks.

By their nature, domain names have a single source of truth; names are only useful if their ownership and control is universal and consistent -- making DNS a common Internet choke point.

This manifests in a few different ways.

The source of truth itself -- the system of authoritative servers -- is a potential and obvious choke point.

Furthermore, DNS can be used as a control point on the path between users and the root server, in the resolvers that the end user requests transit through (e.g., the stub resolver on the system that they are using, or in recursive resolvers, whether explicitly configured or provided by network configuration).

Additionally, DNS requests can be blocked or intercepted on the network.

[examples]

## Trust

A symmertric-key cryptographic protection of the security properties of protocols using requires a method to define and agree upon the roots of trust for the public-key infrastucture (PKI) associated with the protocol. Sometimes, there isa single global root, as in the case with the Root Key Signing Key (KSK) inDNSSEC. Sometimes, roots of trust are regionally distributed, as is the case with the routing public-key infrastructure (RPKI), with one root per Regional Internet Registry (RIR). Still other PKIs have arbitrarily many trust roots: in the case of the Web PKI, each Certificate Authority has its own root, individually trusted on a per-browser or per-platform basis.

Each trust root is associated with a governance structure to ensure proper oversight over control of the root. For example, the DNSSEC root is administered according to ICANN's policy process, the RPKI by each RIR's policy process, and the Web PKI by the CA/Browser Forum.

Creating a new PKI for a protocol unavoidably creates a new chokepoint for the protocol covered by the PKI, represented by the PKI's root, and requires the creation of a new governance  However, reusing an existing PKI for a new related protocol creates a dependency between policies covering the new protocol and those covering the existing protocol, which may or may not be appropriate.


## Content Delivery

performance

resilience



## Service Infrastructure

cloud

third-party services


## Client Platforms

standards-defined platforms

proprietary platforms

stores and ecosystems




# Techniques for Managing Potential Choke Points

There are some cases when there is an unavoidable choke point. For example, as the source of truth regarding naming, administration of domain names is currently a necessary choke point in the Internet architecture.

## Avoiding Choke Points

A choke point can often be avoided through good protocol design.

- distributed
- avoid discriminators
- avoid adding new roles

## Balancing Interests

- create balanced markets
- standards
- federated systems

For example, Content Delivery Networks (CDNs) are sometimes viewed as another emerging choke point, because they are seen as essential in mitigating Distributed Denial-of-Service (DDoS) attacks. While there appears to be a healthy market of CDNs (and similar services) and the costs of using one have been driven down considerably over the years, some suggest that there is a risk of a choke point forming -- as there is wherever a function is critical to the Internet’s operation.

## Multi-Stakeholder Administration

Another technique for mitigating an unavoidable choke point is through formal delegation of its administration to multiple parties with balanced interests, often referred to as the [Multi-Stakeholder Model](https://en.wikipedia.org/wiki/Multistakeholder_governance_model).

For example, in the case of domain names such oversight is performed by ICANN, a multi-stakeholder organisation.

Similarly, the specifications that describe the Internet and the Web form another potential choke point, since they mediate how most people use the Internet. For these, standardization is overseen by the World Wide Web consortium and the IETF, both of whom subscribe to [open standards principles](https://open-stand.org/infographic-the-benefits-of-open-standards/).

Together, these architectural principles and corresponding practices assure that no one person, business or government can control the entire Internet.

## Capture Avoidance

An architectural choke point in the Internet, even if well-protected by a multi-stakeholder governance structure, represents an attractive target to entities that would like to control or disrupt Internet activity. These governance structures should therefore be designed to be resistent to capture by any one entity or set of entities representing a single interest in how the choke point should be administered.

Part of this is simply good governance design, ensuring that oversight functions are sufficiently independent from administrative functions in the operation of a choke point that capture of one does not imply capture of the other. This independence also allows for plausible replaceablilty. The threat that a captured execution function, or a captured function at some point in the oversight chain, could simply be replaced, increases the cost of successful capture.

Each choke point's capture avoidance strategy is dependent on the nature of the choke point. Depending on the choke point, general elements of such a strategy may include:

- the incorporation of legal entities representing each execution and oversight  function in a diversity of legal jurisdictions, to prevent capture by a single  government;
- the selection of members of oversight bodies from diverse jurisdictions and affiliations, to prevent those capture by a small number of government(s)  and/or employer(s);
- the arrangement of funding stream diversity for oversight and execution  functions, to prevent capture by a small number of funders; and/or
- the open publication of any software tooling and/or data necessary to drive an execution function, to the extent possible, in order to increase the  plausibility of replacement.

## External Regulation

Another possible way to counter the ill effects of a choke point is through legal means, for example regulation.  While it may be appropriate as a solution -- especially when a monopoly forms -- the effect of regulation on the architecture need to be evaluated carefully.

For example, near-monopolies on “last-mile” Internet access in some jurisdictions have led to concerns about [network neutrality](http://www.internetsociety.org/net-neutrality), since they act as a choke point.

Historically, the Internet has worked best as a network-of-networks, where each has administrative control to make decisions about local connectivity. Imposing external constraints on how networks select their members and who they communicate with could have far-reaching effects, especially since they are often already subject to a variety of local laws and regulations.

Ensuring that choke points don’t form is preferable to enshrining them in regulation, since they introduce not only points of control, but also increase the risk of failure in that component, concentrate the risk of security vulnerabilities there, and can ultimately limit the scale of the Internet.

Therefore, when there is risk of a choke point forming, we look for other mitigations before considering constraints on the behaviour of infrastructure providers. This might take place through encouraging more diversity at the potential choke point, technical measures that counteract its formation, or other means.



--- back
