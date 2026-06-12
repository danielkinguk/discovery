---
title:
  Gap Analysis and Applicability Statement for Discovery Protocols of
  Agents, Workloads, and Named Entities (DAWN)

abbrev: DAWN Gap Analysis
docname: draft-moussa-dawn-gap-analysis-01
submissiontype: IETF
workgroup:
category: info
ipr: trust200902

stand_alone: yes
pi: [toc, tocompact, tocindent, sortrefs, symrefs, compact]

area: TBD
kw:
  - discovery
  - agents
  - tasks
  - data
  - workloads
  - DAWN

author:
  - ins: H. Moussa
    name: Hesham Moussa
    org: Huawei Technologies Canada
    country: Canada
    email: hesham.moussa@huawei.com

  - ins: A. Akhavain
    name: Arashmid Akhavain
    org: Huawei Technologies Canada
    country: Canada
    email: arashmid.akhavain@huawei.com

normative:

informative:
---

--- abstract

This Internet‑Draft provides a gap analysis and applicability statement
that maps existing Discovery Mechanisms and protocols to the DAWN
problem statement and discovery requirements. The analysis evaluates
security, privacy, applicability, flexibility, and suitability of
existing standardized, non-standardized, and proposed discovery
solutions and protocols to the DAWN problem statement and REQ‑DISC
corpus. It identifies high priority gaps, proposes mitigations and
hybrid patterns, and serves as reference for future prototyping and
development. The intention is for this draft to evolve as new solutions
come to existence.

--- middle

# Introduction

## Purpose

Many distributed processing environments depend on the interaction
between components that do not have pre-configured capability, location,
or reachability relationships. In order for these systems to operate
correctly, the components must be able to discover each other. For
complete generality, we call these components "entities". Entities may
be tasks, workloads, endpoints, services, AI agents, etc. In each case,
an entity needs knowledge of other entities before interaction can
proceed: what they are, what they offer, and whether they can be
trusted. Such knowledge could be obtained via various forms of discovery
ranging from static and passive pre-configuration of the knowledge of
other entities, to more advanced active search and location processes.

DAWN frames the discovery challenge as the need for interoperable,
scalable mechanisms that enable a diverse set of entities to find and
uncover information about one another either within or across
administrative and network boundaries. This document provides a neutral,
actionable assessment of how current discovery mechanisms meet the DAWN
problem statement and requirements, and where gaps remain along areas
including security, privacy, applicability, flexibility, and suitability
for the DAWN use cases.

## Scope {#sec-scope}

This document is expected to continuously evolve as solutions to the
DAWN discovery problem continue to evolve. The following is to set the
scope of the current version of the document as a reference:

- Mechanisms evaluated: DNS family (DNS {{?RFC1123}}, DNS‑SD
  {{?RFC6763}}, SVCB/HTTPS {{?RFC9460}}, TXT), DNS‑AID
  {{?I-D.mozleywilliams-dnsop-dnsaid}}, HTTP/.well‑known {{?RFC8615}}
  and WebFinger {{?RFC7033}}, A2A agent cards and Agntcy, MCP discovery,
  service registries (Consul, Kubernetes), multicast local discovery
  (mDNS {{?RFC6762}}/SSDP), centralized catalogs, P2P/DHT,
  search/crawler and semantic indexes, push/pubsub (LISP {{?RFC9437}})
  channels, CATS (Compute-Aware Traffic Steering). This is an
  exapandable list and shall continue to grow as additional DAWN
  solutions become available.

- Discovery targets: agents, tools, skills, tasks, workloads, datasets,
  and resources.

- Requirements baseline: the DAWN problem statement
  {{?I-D.akhavain-moussa-dawn-problem-statement}}, the REQ‑DISC
  requirements {{?I-D.king-dawn-requirements}}, and use cases
  {{?I-D.kay-dawn-use-cases}} documents.

- Criteria for solution inclusion: Solutions selected for analysis
  within the current document should meet one or more of the following
  criteria:
  - A standardized solution adopted by one or more Standards Development
    Organizations (SDOs), such as IETF, 3GPP, ITU, or similar bodies.
  - A solution proposed as part of an ongoing official standardization
    effort, such as active IETF or 3GPP working groups, ETSI Technical
    Committees (TCs), or Industry Specification Groups (ISGs), and
    showing signs of maturity (for example, having undergone sufficient
    critique, development, and testing).
  - Solutions supported by major open‑source ecosystems, foundations, or
    widely recognized community projects.
  - Solutions with clear adoption or deployment by a broad audience or
    client base, indicating potential to become a de facto standard.

- Primary evaluation focus: security, privacy, applicability to DAWN
  requirements, flexibility for multiple entity types and deployment
  models, operational suitability, and mitigation and development cost.

## Intended audience

IETF communities, working groups, other standard bodies, and developers
(DAWN, DNSOP, Add others???), platform architects, registry operators,
and developer of agent and tool ecosystems.

# Terminology

The following terms are used in this document as defined in
{{!I-D.farrel-dawn-terminology}}.

- Entity

- Attributes

- Discoverable object

- Minimum Discoverable Information (MDI)

- Discovery

- Capability exchange / negotiation

- Selection

- Discovery Mechanism

# Motivation

Many modern distributed systems rely on automated interactions among
components that were not preconfigured to work together. Incomplete,
insecure, or poorly designed discovery undermines automation and can
lead to impersonation, stale or incorrect interactions, large‑scale
privacy exposure, and brittle cross‑domain integrations. The DAWN
Problem Statement and REQ‑DISC requirements identify the need for
interoperable, scalable discovery mechanisms that operate across
administrative and network boundaries; this document responds by
assessing existing discovery methods and Mechanisms against those
requirements and by evaluating and highlighting gaps that most affect
safe, privacy‑respecting, and ease of deployment to meet DAWN discovery
needs.

## Key Motivating Scenarios and Risks

- Operational risk: Discovery that is operationally stale, allows
  unauthenticated entries to participate, or renders incorrect results
  can cause connections to wrong or potentially unsecure endpoints,
  execution of unsafe actions, and unexpected outcomes. This includes
  cases where compromised descriptors/cards or outdated pointers lead to
  impersonation, misrouting (to which entity the request goes to), or
  cascading failures in workflows. Mitigations include strong
  authenticity checks, signed descriptors/cards, and timely revocation
  mechanisms. Another major operation risk lies in queries that
  potentially may result in unbounded searches and could be used to
  invoke denial of service attacks.

- Privacy risk: Public or poorly controlled discovery query, response
  and OAM channels can expose sensitive information about entities,
  their relationships, and intentions. Attackers or unauthorized parties
  can scrape open indexes, correlate query logs, or exploit predictable
  naming to build profiles, infer business plans, or target specific
  systems. Mitigations include minimizing the need for exposing
  sensitive information during the discovery process, gating access to
  rich descriptors/cards, secure transport channels, and proper handling
  of logs, tracking, and history records.

- Interoperability gap: Many discovery solutions are platform‑specific
  or use incompatible formats, which prevents entities from discovering
  one another across administrative domain, vendor boundaries, or even
  within the same organization. This fragmentation increases operational
  and integration costs, slows automation, and encourages siloed
  ecosystems. Mitigations include defining a standardized minimum common
  descriptor schema/cards, being hardware and underlay network agnostic,
  and supports backward compatibility and integration with legacy
  systems.

- Scalability and deployment: Some discovery mechanisms do not scale to
  internet‑wide, federated use or impose heavy operational burdens on
  operators. Problems include excessive indexing costs, high query
  volumes on authoritative servers, lack of a unified solution to
  support discovery of various types of entities, costly monitoring
  mechanisms to maintain up-to-date entity statuses, and complex
  deployment process.

- DAWN suitability: Solution suitability for DAWN refers to its
  practicality to meet DAWN Problem Statement, REQ‑DISC goals, and
  suggested use cases. This includes utilizing strong authentication and
  provenance mechanisms, enabling privacy controls and anti‑disclosure
  measures, representing the full range of entity types, allowing
  extensible and standardized descriptor/card formats, operating at
  internet scale without undue operator burden, and support
  interoperability. When the above criteria cannot be met by existing
  solutions, there will be a need to develop solutions that support at
  least aspects such as standardized descriptor mappings and different
  methods of publication and disclosure to achieve interoperable,
  secure, and deployable discovery.

This document therefore aims to produce actionable outcomes for
implementers and operators by analyzing currently implemented or
proposed Discovery Mechanisms and protocols. The objective is to help
guide standardization efforts by shedding light on potential gaps and
recommending some mitigation measures.

# Analysis Methodology

## Overview

We adopt an itemized analytical approach where each Discovery Mechanism
is examined against the same set of evaluation metrics. Figure 1 of the
problem statement document
{{?I-D.akhavain-moussa-dawn-problem-statement}} serves as the reference
architecture accepted by DAWN. As per this architecture, entities are to
be discovered using their discoverable information registered into the
Discovery Mechanism. Fields of the discoverable information are divided
into mandatory and optional. As an initial baseline, a single
discoverable information model for evaluation is considered for all
types of entities consisting of mandatory fields that cover the
following aspects: entity identifier, standard entity descriptor (what
is it, what can it do, how to interact with it...etc), human summary
(for ease of accessibility by humans), endpoints/pointers, conveying
trust related material, privacy/access indicators, freshness/lifecycle
(i.e. status), operational metadata, indexing hints, current status, and
entity provenance.

## Evaluation steps

- Preparation step:
  - Select, based on the criteria mentioned in section {{sec-scope}},
    the discovey mechanisms to be evaluated.
  - Extract REQ‑DISC items from the requirements document
    {{?I-D.king-dawn-requirements}} and map them to Mechanism evaluation
    criteria.
  - Extract use case-specific discovery requirement as per
    {{?I-D.kay-dawn-use-cases}}

- Evaluate Level of Coverage of REQ-DISC: For each Mechanism, evaluate
  coverage of REQ‑DISC items, use case-specific requirements, and
  discoverable information fields using a three‑level scale: Full,
  Partial, None. Also note native encoding of each Mechanism were, for
  each, record one of: native support, common extension to the
  Mechanism, hybrid pattern, or no practical support without extensive
  redesign.

- Security, privacy, and DAWN suitability evaluation:
  - Conduct informed analysis: Evaluate exposure to assumed adversaries
    (passive observer, on‑path attacker, operator adversary, malicious
    publisher, Sybil);
  - Examine potential information leakage: potential for public metadata
    leakage, enumeration risk, query logging exposure, linkability, and
    stale exposure;
  - Compare against DAWN REQ-DISC and use case-specific criteria.
  - Assign a numeric impact score from 0–3 that reflects how well a
    Mechanism meets the three criteria (security, privacy, DAWN
    suitability): (0) Not suitable:

  High security or privacy risk; does not meet DAWN requirements; (1)
  Low suitability: Requires only minor changes to meet at least one of
  the three criteria; (2) Moderate suitability: Meets one criterion
  natively and can meet at least one of the remaining criteria with
  minor changes; (3) High suitability: Meets at least two criteria
  natively and meets the third either natively or with only minor
  changes. It should be noted here that these measures are intended to
  evaluate how secure and private the discovery process is.

- Operational cost: Study deployment and operation cost of each
  Mechanism. Assign a simple adoption values (low, medium, high) for
  operator reflecting expected operation burden and deployment friction.

- Mitigation cost: First, identify potential gaps by analyzing each
  Discovery Mechanism and determining what features are missing to meet
  security, privacy, and DAWN REQ-DISC items. Accordingly, evaluate cost
  for mitigation by proposing protocol‑level, operational, and/or hybrid
  mitigations and prototype patterns to potentially alleviate Mechanism
  downfalls against the requirements. Assign simple values to reflect
  mitigation costs (low, medium, high).

## Notes for further guidance and considerations

Performance assessment:

- List common extensions or hybrid patterns that fill gaps (e.g., DNS
  pointer → HTTPS descriptor; registry webhook for revocation).

- Mitigations: note whether mitigations are supported natively, via
  extension, or only by operational practice.

- Cache model: document caching semantics (TTL, intermediate caches, CDN
  behavior).

- Revocation channels: identify available mechanisms (short validity,
  push notifications, status endpoints).

- Estimate stale window: provide a worst‑case stale exposure estimate
  and practical mitigations (short TTL, signed timestamps, push).

Inter-operability assessment:

- Round-trip checks: verify that a descriptor encoded in Mechanism A can
  be represented and validated when consumed via Mechanism B; note lossy
  fields.

- Adapter patterns: document minimal adapter logic required to translate
  between formats.

Operational assessment:

- Deployability: list operator requirements (hosting, key management,
  logging, rate limiting).

- Scale considerations: estimate query load, indexing cost, and storage
  needs for representative use cases.

# Summary of REQ-DISC document {#sum-req-disc}

As per the REQ-DISC document {{?I-D.king-dawn-requirements}}, a
discovery solution addressing the DAWN requirements should:

- Support discovery of agents, services, workloads, and other named
  entities by both human users and automated systems across
  organizational and administrative boundaries.

- Enable discovery based on entity identity, attributes, roles, and
  advertised capabilities, allowing requesters to locate entities that
  satisfy specific functional requirements.

- Provide machine-readable metadata describing discovered entities,
  including capabilities, ownership, policy information, security
  characteristics, and references to additional descriptive resources.

- Operate across heterogeneous administrative domains while supporting
  decentralized and federated deployment models that avoid reliance on a
  single centralized registry.

- Establish trust in discovery information through mechanisms that
  support authenticity, integrity validation, provenance, and
  policy-based assessment of discovered entities.

- Support controlled publication and selective disclosure of discovery
  information, allowing organizations to manage visibility of entities
  and associated metadata according to policy and trust relationships.

- Scale to Internet-wide deployment, supporting large numbers of
  entities, frequent updates, and dynamic environments in which entities
  may appear, disappear, or change capabilities over time.

- Accommodate diverse implementation and deployment environments without
  imposing assumptions about underlying communication protocols,
  transport mechanisms, or execution platforms.

- Minimize opportunities for abuse, including unauthorized information
  harvesting, spoofing, tampering, and other attacks that could
  undermine the reliability or trustworthiness of discovery results.

- Provide a foundation upon which higher-layer functions - including
  capability negotiation, service selection, orchestration, and
  agent-to-agent interaction - can be built, while remaining focused on
  discovery itself.

# Summary of use case document

To be completed as per the draft {{?I-D.kay-dawn-use-cases}}

# Discovery Mechanism High-level Descriptions and Evaluation

The following analysis is based on evaluations of the various discovery
solutions, substrates, and protocols against the REQ-DISC summary
provided in section {{sum-req-disc}}. A quick note on DAWN suitability
block within each subsection. A more systematic and rigorous evaluation
approach against the REQ-DISC items is needed. What is included is an
initial high-level evaluation that shall be improved with rounds of
revisions to the current document.

## DNS (including SVCP/HTTPS and TXT)

- **Summary**: DNS provides global, hierarchical name resolution and can
  carry small discovery pointers (TXT, SVCB/HTTPS). It is excellent for
  bootstrapping because it is ubiquitous and highly cached.

- **How it works**: Clients query recursive resolvers for resource
  records (A/AAAA, TXT, SVCB, etc.). SVCB/HTTPS records can encode
  structured service parameters so clients choose endpoints and
  transport parameters before connecting. DNS responses are cached by
  resolvers and intermediate caches according to TTLs.

- **Security, Privacy, and DAWN suitability Considerations:**
  - Security:
    - Strengths: Widely deployed tooling; DNSSEC can provide signed
      RRsets and integrity guarantees; SVCB improves client
      pre‑connection behavior.
    - Weaknesses: Trust is concentrated in authoritative servers and
      resolvers; on‑path or operator adversaries can observe or
      manipulate queries unless additional protections are used.
  - Privacy:
    - Queries and responses are observable by resolvers and on‑path
      observers hence increases the risk of privacy provocation.
    - It also builds caches and public records that are indexable and
      enumerable allowing various privacy attacks.
    - Techniques such as DoH/DoT are used to reduce on‑path exposure but
      do not fully eliminate operator logging which exposes a
      vulnerability.
    - Using such limitations, public pointers can be scraped to build
      maps of entities and activity patterns within DAWN leading to a
      major privacy concern.

  - DAWN suitability: Although DNS is excellent for bootstrap pointers
    (telling a consumer where to look) and for federation/bootstrapping
    at internet scale, its suitability to DAWN is "Partial" for the
    following reasons
    - DNS is fundamentally a lookup system - it assumes the consumer
      knows the name or key to query. That model does not fit DAWN's
      need for high‑level, descriptive search (e.g., "find agents that
      can translate legal contracts and accept a $budget"), which often
      requires indexing, semantic search, or registries that return
      multiple matches for a description;
    - The DNS key-value model struggles to carry complex nested
      capability structures and composite queries, introducing
      limitations in expressiveness.
    - These limitations suggest that DNS-based discovery mechanisms may
      not fully meet the needs of typical DAWN scenarios such as
      cross-domain capability filtering, dynamic resource state queries,
      and global semantic search.
    - However, DNS is suitable as a first hop in DAWN patterns and
      covers a subset of discovery types that shall be supported by
      DAWN.
  - Security, Privacy, and DAWN suitability score: **1/3**
    - Scalability and interoperability are supported. However, security,
      privacy, information rich and semantic searches, multi-cast
      operation, and multi-type of entity support are still missing.

- **Use case fitness**
  - TBC
- **Mitigations grouped by goal**
  - Mitigations for Descriptor hosting and integrity:
    - Mitigation: Host full descriptors on HTTPS endpoints; sign
      descriptors with JWS (include issued_at/expires_at) so consumers
      can verify integrity and provenance.
    - Cost: Medium - requires hosting, key management, and signing
      tooling.
    - Impact: Strong integrity and non‑repudiation; enables gated access
      to rich metadata.

  - Mitigations for Freshness and revocation:
    - Mitigation: Use short validity windows in signed descriptors,
      provide a status/revocation endpoint, and optionally push
      revocation notifications (webhooks or pub/sub).
    - Cost: Medium to High - short expiries increase refresh load; push
      channels add infrastructure.
    - Impact: Reduces stale exposure and limits the window for
      compromised descriptors.

  - Mitigation for Privacy and anti‑enumeration:
    - Mitigation: Publish only minimal public pointers in DNS; keep
      capability/intent fields behind authenticated endpoints; use
      naming entropy or tokenized pointers for private resources;
      enforce rate limits and crawler controls.
    - Cost: Low to Medium - naming and pointer changes are cheap; access
      control and rate limiting add operational work.
    - Impact: Substantially reduces mass scraping and profiling risk.

  - Mitigation for Search and descriptive discovery integration:
    - Mitigation: Combine DNS bootstrap with a separate indexed layer
      (centralized or federated catalog, semantic index) that supports
      descriptive queries and returns candidate names/IDs for DNS
      resolution. Ensure the index enforces access control and privacy.
    - Cost: High - building or integrating an index and maintaining
      privacy controls is substantial.
    - Impact: Fills DNS's descriptive‑search gap and enables DAWN‑style
      high‑level queries.

  - Overall Mitigation score: **HIGH**

## mDNS/DNS‑SD

- **Summary**: mDNS/DNS‑SD provides zero‑configuration, multicast
  service discovery on local networks. It's ideal for quick,
  low‑friction discovery of nearby devices and services but is limited
  to link‑local scope and lacks built‑in authentication or global search
  capabilities.

- **How it works**: Devices announce and browse services using multicast
  DNS on the local link. Service types are advertised with PTR/SRV/TXT
  records; clients listen for announcements or actively query the
  multicast group to discover available instances and connection
  parameters. Announcements are repeated periodically and withdrawn when
  services go away.

- **Security, Privacy, and DAWN suitability Considerations:**
  - Security:
    - Strengths: Simple, low‑overhead; works without central
      infrastructure; good UX for trusted LANs.
    - Weaknesses: No native authentication or integrity guarantees; any
      host on the same link can spoof announcements or impersonate
      services; multicast makes on‑link MitM and injection trivial
      unless application‑level protections are used.

  - Privacy:
    - Announcements are visible to all hosts on the local link, enabling
      easy enumeration and profiling of devices and capabilities.
    - Sensitive attributes in TXT records or predictable instance names
      increase local exposure.
    - There is no built‑in mechanism to gate who can see or query
      service announcements.

  - DAWN suitability: Partial
    - mDNS/DNS‑SD is excellent for local bootstrapping and immediate
      peer discovery but fails DAWN requirements that need:
      authenticated identity, privacy‑protected capability disclosure,
      revocation at scale, and descriptive, multi‑match search across
      administrative boundaries.
    - It is best used as a local layer within a larger DAWN
      architecture, not as the primary cross‑domain Discovery Mechanism.
  - Security, Privacy, and DAWN suitability score: **2/3**
    - Scalability and interoperability and multi-cast operations are
      supported. However, security, privacy, information rich and
      semantic searches, and multi-type of entity support are still
      missing.

- **Use case fitness:**
  - TBC

- **Mitigations grouped by goal**
  - Mitigations for Descriptor hosting and integrity:
    - Mitigation: Host full descriptors on HTTPS endpoints; sign
      descriptors with JWS (include issued_at/expires_at) so consumers
      can verify integrity and provenance.
    - Cost: Medium - requires hosting, key management, and signing
      tooling.
    - Impact: Strong integrity and non‑repudiation; enables gated access
      to rich metadata.
  - Mitigation for Local reliability and safe bridging
    - Mitigation: Use mDNS only for LAN discovery; deploy discovery
      gateways/proxies that vet local announcements and publish vetted
      pointers to external registries or descriptor hosts.
    - Cost: Low to Medium - gateway software deployment and
      configuration.
    - Impact: Preserves zero‑config UX while preventing raw multicast
      data from being exposed externally.

  - Mitigation for Privacy and anti‑enumeration
    - Mitigation: Advertise only minimal identifiers on multicast; move
      capability, intent, and sensitive metadata to gated endpoints. Use
      randomized or tokenized instance names for private services.
    - Cost: Low - change in advertisement content and naming policy.
    - Impact: Reduces casual local scraping and profiling.

  - Mitigation for Freshness and revocation
    - Mitigation: Use short announcement intervals and aggressive
      withdrawal semantics; for cross‑domain exposure, rely on hosted
      signed descriptors with explicit expiry and status endpoints.
    - Cost: Low–Medium - more network chatter for short intervals;
      hosting for descriptors.
    - Impact: Limits stale information and speeds removal of retired or
      compromised services.

  - Mitigation for Cross‑domain descriptive search
    - Mitigation: Do not rely on mDNS for descriptive or semantic
      search. Instead, have gateways publish minimal pointers into a
      controlled index or registry that supports descriptive queries and
      returns candidate identifiers for resolution. Ensure the index
      enforces access control and privacy.
    - Cost: High - building/integrating an index and gateway logic is
      substantial.
    - Impact: Enables DAWN‑style high‑level queries without exposing LAN
      multicast to the internet.

  - Overall Mitigation score: **LOW TO MEDIUM**

## SSDP/UPnP

- **Summary**: SSDP/UPnP provides simple, multicast‑based discovery for
  devices and services on local networks. Devices announce presence and
  a `LOCATION` URL pointing to a device description (usually XML),
  enabling zero‑config discovery and immediate interoperability in home
  and small‑office environments.

- **How it works**: Devices use SSDP (Simple Service Discovery Protocol)
  over UDP multicast to send `NOTIFY` announcements and to respond to
  `M‑SEARCH` queries. Announcements include a `LOCATION` header that
  points to an HTTP URL hosting a device/service description (UPnP XML).
  Clients listen for announcements or actively query the multicast
  group, then fetch the description from the `LOCATION` URL to learn
  capabilities and control endpoints.

- **Security, Privacy, and DAWN suitability Considerations:**
  - Security:
    - Strengths: Very low friction; works without central
      infrastructure; widely implemented in consumer devices.
    - Weaknesses: No built‑in authentication or integrity for
      announcements; multicast on the local link is trivially spoofable
      by any on‑link actor; `LOCATION` URLs are fetched over plain HTTP
      in many deployments, enabling on‑path tampering; SSDP has been
      used in amplification/reflection attacks and can expose devices to
      remote abuse when improperly bridged.

  - Privacy:
    - Announcements are visible to all hosts on the local link, enabling
      easy enumeration and fingerprinting of devices and capabilities.
    - `LOCATION` URLs often expose rich device metadata (model,
      services, control URLs) that enable profiling.
    - There is no native access control or audience restriction for SSDP
      announcements.

  - DAWN suitability: Partial
    - SSDP/UPnP is useful as a local bootstrap for DAWN (discovering
      nearby agents, tools, or gateways) but unsuitable as a
      cross‑domain Discovery Mechanism.
    - Key gaps: no authentication/integrity for announcements, high
      local enumeration risk, weak transport security in many
      deployments, and no support for descriptive, multi‑match search
      across administrative boundaries. SSDP should be treated as a
      local candidate source that must be validated via stronger
      channels before being trusted in DAWN flows.

  - Security, Privacy, and DAWN suitability score: **1/3**
    - Meets the descriptive metadata rich cards that may facilitate
      semantic and capability based searches, and can be expanded to
      cater for other types of entities (flexibility). However,
      security, privacy, interoperability, and scalability are
      questionable.

- **Use case fitness:**
  - TBC
- **Mitigations grouped by goal**:
  - Mitigations for Descriptor hosting and integrity
    - Mitigation: Main issue is security and privacy. Thus mitigation
      for this key gap is to handle these short comings. A possible way
      is to Host device/service descriptors at HTTPS origins (use
      `https://` in `LOCATION` where possible) and publish JWS‑signed
      descriptors or include a signature reference in the XML. Consumers
      must verify signatures and timestamps before trusting descriptor
      fields. Publish verification keys via a stable, verifiable channel
      (JWK, DID, or TLS pin).
    - Cost: Medium - requires HTTPS hosting, signing tooling, and client
      verification logic.
    - Impact: prevents on‑link tampering of descriptors and provides
      provenance even if SSDP announcements are spoofed.

  - Mitigation for Privacy and anti‑enumeration
    - Mitigation: Minimize information in multicast announcements
      (advertise only a short service identifier and a tokenized
      pointer); move capability and intent fields to gated HTTPS
      descriptors. Use tokenized `LOCATION` values for private services
      and enforce local firewall rules to limit who can receive
      announcements.
    - Cost: Low to Medium - changing announcement content is cheap;
      token issuance and firewall rules add operational work.
    - Impact: reduces local mass‑scraping and profiling and limits
      exposure of sensitive metadata.

  - Mitigation for Cross‑domain descriptive search
    - Mitigation: Do not rely on SSDP for descriptive or semantic
      search. Instead, have local gateways or proxies publish vetted
      pointers (or signed attestations) into a controlled index or
      registry that supports descriptive queries. The index returns
      candidate IDs or names which clients then resolve to HTTPS
      descriptors. Ensure the index enforces access control and honors
      publisher privacy flags.
    - Cost: High - building gateway logic and an index/federation is
      substantial.
    - Impact: enables DAWN‑style descriptive discovery without exposing
      raw SSDP multicast to the internet.

  - Mitigation for Freshness and revocation\*\*
    - Mitigation: Use SSDP's `ssdp:alive`/`ssdp:byebye` semantics and
      short announcement intervals for local freshness; for
      cross‑exposed descriptors, require signed descriptors with
      `issued_at`/`expires_at` and a `status_endpoint` for revocation
      checks. Optionally support push revocation from gateways to index
      subscribers.
    - Cost: Medium - shorter intervals increase local traffic; hosted
      revocation endpoints add infra.
    - Impact: reduces stale exposure and shortens the window for
      compromised or retired services.

  - Mitigation for Cross‑domain descriptive search (federation and
    provenance)
    - Mitigation: For federated deployments, exchange signed
      attestations (not raw descriptors) between indexes; indexes return
      candidate IDs and provenance metadata that clients can verify
      against the origin's signed descriptor fetched over HTTPS. Enforce
      privacy flags and access control at each hop.
    - Cost: High - federation, attestation formats, and access controls
      require coordination and infrastructure.
    - Impact: preserves provenance and privacy while enabling
      descriptive, cross‑domain discovery.

  - Overall Mitigation score: **MEDIUM**

## DNS-AID

**To be completed**

## A2A (Agent2Agent)

- **Summary**: A2A defines an Agent Card model and a set of discovery
  paths (well‑known HTTPS URIs, curated registries, local discovery, and
  managed provisioning) to enable interoperable agent‑to‑agent discovery
  and invocation. It is mainly agent‑centric discovery: the metadata and
  discovery flows are designed for locating and evaluating software
  agents, agentic services, and for monitoring agentic workflows, not
  for discovering arbitrary entity types (people, tasks, compute,
  resources, or generic sensors) without additional architectural and
  inherent modifications.

- **How it works**: Agents or operator domains publish an Agent Card (a
  JSON descriptor) at a resolvable HTTPS location or register a pointer
  in a curated registry. Discovery paths include local discovery (e.g.,
  mDNS/DNS‑SD), well‑known HTTPS endpoints, curated
  registries/marketplaces, and locally managed network options
  especially under enterprise settings. A client agent discovers a
  pointer to a server where agent cards are stored, fetches the Agent
  Card of interest from the HTTPS origin (server address), verifies
  signatures or attestations and auth measures, potentially evaluates
  declared capabilities and policies, and then initiates an
  authenticated invocation using the declared endpoint and auth method.

- **Security, Privacy, and DAWN suitability Considerations:**
  - Security:
    - Strengths: A2A is web‑aligned and designed to leverage TLS,
      standard auth schemes (OAuth2, mTLS, token exchange), and signed
      Agent Cards or DID attestations. Curated registries and enterprise
      deployments can control who is allowed to publish or access Agent
      Cards, check that agents are legitimate before listing them, and
      enforce the organization's rules about how agents are used. The
      model lets agents state exactly what they can do and how they
      expect to be authenticated, which helps other agents invoke them
      safely and according to policy.
    - Weaknesses: Discovery methods like local mDNS or public registries
      can be misused if Agent Cards are not signed or protected,
      allowing attackers to impersonate agents or scan for them.
      Registries and trusted operators also become important points of
      control; if a registry, signing key, or hosting service is
      compromised, an attacker could insert fake or harmful agents. When
      agents are discovered on an untrusted local network, extra checks
      are needed to confirm that the agent is real before interacting
      with it.

  - Privacy:
    - Agent Cards and registry listings can reveal what an agent can do,
      how often it is used, who it interacts with, or when it tends to
      run.
    - Telemetry and query logs can also be used to build a profile of an
      agent's behavior.
    - Detailed capability information are published without access
      controls, and hence can expose sensitive operational or commercial
      details.

  - DAWN suitability:
    - A2A works well when the goal is to find and interact with agents,
      agentic services, or to monitor agent‑driven workflows.
    - It is mainly used inside trusted domains or curated marketplaces,
      and so far it has not been deployed commercially at large scale or
      across multiple vendors and domains.
    - The model assumes that agents describe themselves in a standard
      way using Agent Cards, and that discovery is driven mostly by
      keyword‑based queries.
    - A2A is also not designed to serve as a broad, public discovery
      system for many different types of entities, such as data,
      compute, people, devices, or raw content, and it does not provide
      cross‑domain semantic search on its own.
    - Although its scope is limited, the overall structure can be
      extended and strengthened to address its current gaps and better
      meet the broader requirements of DAWN.
    - It should be noted however, that the discovery method implemented
      by A2A runs on top of existing infrastructures and substrates such
      as HTTP, JSONRPC, and DNS and thus is not a full end-to-end
      solution.
    - The main contribution of A2A to the discovery problem is the
      introduction of the agent cards, which are metadata rich
      descriptors or entities.

  - Security, Privacy, and DAWN suitability score: **1/3**
    - Meets the descriptive metadata rich cards that may facilitate
      semantic and capability based searches, and can be expanded to
      cater for other types of entities (flexibility). However,
      security, privacy, interoperability, and scalability are
      questionable.

- **Use case fitness:**
  - TBC

- **Mitigations grouped by goal**
  - Mitigations for Descriptor hosting and integrity
    - Mitigation: Ensure that Agent Cards are cryptographically signed
      and that clients always verify those signatures before trusting
      any capabilities or endpoints. Host cards at secure HTTPS
      locations, publish the verification keys so clients can validate
      them, and require registries to accept only signed cards. This
      strengthens the basic A2A model by making Agent Cards trustworthy
      across domains and preventing spoofing or impersonation.
    - Cost: Low - requires signing tools, key‑hosting, and verification
      logic in clients and registries, but does not require building a
      full cross‑domain PKI.
    - Impact: prevents forged or tampered Agent Cards, ensures
      provenance, and provides a reliable foundation for DAWN‑grade
      discovery.

  - Mitigation for Privacy and anti‑enumeration
    - Mitigation: Protect sensitive parts of the Agent Card by placing
      them behind authenticated endpoints or controlled registry access.
      Add privacy flags so agents can indicate which fields should be
      hidden or shared. Limit who can query the system, use short‑lived
      discovery tokens, apply rate limits, and share only aggregated or
      privacy‑preserving telemetry when exposing metrics outside a
      trusted domain. For catalog use, publish small signed summaries
      instead of full Agent Cards to reduce the amount of sensitive
      information exposed.
    - Cost: Medium - requires access‑control checks, token issuance,
      aggregation pipelines, and enforcement of registry policies.
    - Impact: reduces scraping, profiling, and leakage of sensitive or
      commercially valuable information while still allowing authorized
      discovery.

  - Mitigation for Cross‑domain descriptive search
    - Mitigation: Rather than treating the A2A discovery plane as a
      semantic index, create small signed summaries (attestations)
      derived from Agent Cards and publish those into a separate catalog
      that is designed for descriptive or cross‑domain queries. The
      catalog returns candidate agent IDs or attestations, and clients
      then fetch the authoritative Agent Card and verify its signature
      and provenance before interacting with the agent. This keeps A2A
      focused on secure resolution while allowing richer search to
      happen in a controlled layer above it.
    - Cost: High - requires building or integrating a catalog, defining
      an attestation format, and establishing rules for federation and
      access control.
    - Impact: enables DAWN‑style descriptive discovery while maintaining
      provenance, privacy, and controlled access to sensitive
      information.

  - Mitigation for Freshness and revocation
    - Mitigation: Include issued_at and expires_at in Agent Cards and
      attestations; provide status and revocation endpoints; support
      push notifications (webhooks/pubsub) for card updates and
      de‑registration; enforce short lifetimes for ephemeral offers.
      Require controllers to revalidate before committing long‑running
      interactions.
    - Cost: Medium - revocation/status infrastructure, pub/sub channels,
      and more frequent control‑plane updates.
    - Impact: reduces stale or compromised listings and improves
      correctness for time‑sensitive tasks and agent capabilities.

  - Mitigation for Federation and provenance
    - Mitigation: Exchange signed attestations (not raw cards or
      metrics) between operators and catalogs; require provenance chains
      and trust anchors per federation member; include policy, consent,
      and billing metadata in attestations; enforce verification of
      provenance chains before accepting remote agent invocation.
    - Cost: High - attestation formats, trust management, legal
      agreements, and operational coordination.
    - Impact: preserves provenance and trust across domains and enables
      accountable cross‑domain discovery and invocation.

  - Overall Mitigation score: **MEDIUM**

## CATS (Compute-Aware Traffic Steering) — IETF working group

- **Summary**: CATS defines a control‑plane framework for steering
  traffic to compute locations by combining service announcements,
  compute and network metrics, and policy‑driven selection. It is
  explicitly compute‑centric: the primitives, metrics, and selection
  logic are designed for operators to be able to locate and steer
  traffit to compute sites and service instances, not for discovering
  arbitrary entity types (people, documents, sensors, or generic
  agents).

- **How it works**: For 'discovery' in CATS, service instances and
  contact instances are announced into the CATS control plane. Metric
  agents collect compute (C‑SMA) and network (C‑NMA) telemetry and
  publish metrics to controllers or selectors (C‑PS). A path selector or
  controller queries available sites, evaluates policy and metrics, and
  chooses a target site/instance. Forwarders (CATS‑Forwarders) then
  enforce steering decisions.

- **Security, Privacy, and DAWN suitability Considerations:**
  - Security:
    - Strengths: Designed for authenticated agents and operator trust
      domains; control‑plane messages and metric flows are intended to
      be authenticated and access‑controlled. Selection decisions are
      policy‑driven, enabling fine‑grained operator governance.
    - Weaknesses: Trust is concentrated in operator controllers and
      metric collectors; exposing metrics or announcements beyond
      trusted domains risks manipulation or information leakage.
      Compromise of metric agents or controllers can mislead selection
      and routing.

  - Privacy:
    - Risks: Compute and network metrics can reveal capacity, load,
      topology, and usage patterns; if distributed widely, they enable
      profiling of service placement and demand. While this is
      acceptable as long as the operation is within, CATS does not
      implement specific privacy mechanisms for external intruders
      except gating and authenticity verification. Thus, if such
      measures are bypassed, privacy is compromised.
    - Controls: The model assumes authenticated, limited distribution of
      metrics; without strict access controls and aggregation, metric
      publication can violate privacy or commercial confidentiality.

  - DAWN suitability: Partial (compute‑only)
    - discovery within CATS is well suited for a discovering one type of
      entities that reside within the vicinity of authenticated
      networked elements. That is, CATS is an operator‑centric discovery
      of compute locations and precise selection based on metrics (good
      for low‑latency, policy‑aware steering) within compute
      environment.
    - CATS discovery is not a DAWN‑style public, multi-entity,
      descriptive Discovery Mechanism: it does not provide semantic,
      multi‑match search across administrative boundaries out of the box
      and assumes operator trust and scoped distribution.

  - Security, Privacy, and DAWN suitability score: **1/3**
    - implements a control plane and announcement mechanism that gives a
      flexible structure that can be expanded, however lacks in
      scalability, interoperability, security, and privacy domains.

- **Use case fitness: TBC**

- **Mitigations grouped by goal**
  - Mitigations for Descriptor hosting and integrity
    - Require signed service/site/task descriptors and signed
      announcements; publish verification keys via operator PKI, JWK
      sets, or DID documents; enforce signature verification in
      controllers and selectors before acting on any announcement or
      descriptor.
    - Cost: Medium - Needs signing libraries, descriptor schema work,
      KMS integration, and client verification logic.
    - Impact: Prevents forged announcements, ensures provenance, and
      enables non‑repudiation for placement and steering decisions.

  - Mitigation for Privacy and anti‑enumeration
    - Aggregate and redact metrics, limit audience via RBAC and tokens,
      apply rate limits to discovery APIs, and use differential privacy
      or noise injection for telemetry exported beyond the operator
      domain.
    - Cost: Medium - Requires metric aggregation pipelines, access
      control systems, and policy enforcement.
    - Impact: Reduces profiling, commercial leakage, and mass scraping
      while preserving steering utility.

  - Mitigation for Cross‑domain descriptive search
    - Publish signed, minimal pointers or attestations from CATS into a
      separate indexed or federated catalog that supports descriptive
      queries. The catalog returns candidate IDs or attestations which
      clients resolve back to CATS‑announced sites under controlled
      access and verification.
    - Cost: High - Building a catalog, federation protocols, attestation
      formats, and access controls requires substantial engineering and
      governance.
    - Impact: Enables DAWN‑style descriptive discovery while preserving
      operator control, provenance, and privacy.

  - Mitigation for Freshness and revocation
    - Include explicit validity windows in announcements and
      descriptors, provide status and revocation endpoints, and use push
      pub/sub to propagate revocations and state changes. Enforce short
      lifetimes for highly dynamic metrics and ephemeral offers.
    - Cost: Medium to High - Requires revocation/status infrastructure,
      pub/sub channels, and more frequent control‑plane updates.
    - Impact: Reduces stale placements, limits the window for
      compromised information, and improves correctness for
      time‑sensitive tasks.

  - Mitigation for Cross‑domain descriptive search (federation and
    provenance)
    - Exchange signed attestations (not raw metrics) between operators;
      require provenance chains and trust anchors per federation member;
      enforce policy translation and explicit consent for metric and
      task sharing.
    - Cost: High - Federation requires attestation formats, trust
      management, legal agreements, and operational coordination.
    - Impact: Preserves provenance and trust across domains and enables
      controlled cross‑domain discovery and placement.

- overall mitigation score: **MEDIUM TO HIGH**

## MCP

**To be completed**

## AGNTCY

**To be completed**

## Service registries & orchestration

List includes: Consul, etcd, Eureka, Kubernetes Service DNS, service
meshes.

**To be completed**

## HTTP/.well‑known {{?RFC8615}}

**To be completed**

## WebFinger {{?RFC7033}}

- **Summary**: WebFinger (RFC 7033) is an HTTP‑based mechanism for
  resolving information about a subject identified by a URI, most
  commonly an account‑style identifier such as `acct:alice@example.com`.
  A WebFinger server returns a JSON Resource Descriptor (JRD) containing
  properties and typed links associated with the subject. WebFinger is
  widely used for account and profile resolution in federated systems,
  but it is not a general discovery substrate and does not support
  descriptive or capability‑oriented search.

- **How it works**: A client constructs a query to
  `/.well-known/webfinger` on the domain extracted from the subject
  identifier and includes the subject URI in the `resource` parameter.
  The server responds with a JRD document containing:
  - subject: the canonical identifier
  - aliases: alternative identifiers
  - properties: key–value attributes
  - links: typed links to related services or endpoints

  WebFinger assumes that the client already knows the subject
  identifier. It does not define indexing, search, or mechanisms for
  discovering subjects in the first place. It functions strictly as a
  resolution protocol.

- **Security, Privacy, and DAWN suitability Considerations:**
  - Security
    - Strengths: WebFinger relies on HTTPS for server authentication and
      transport integrity. The protocol is simple, widely deployed, and
      benefits from mature HTTP security practices. Operators may apply
      access control or filtering policies, although these are not
      mandated.

    - Weaknesses: There is no cryptographic signing of JRD responses, no
      per‑field integrity, and no offline verification. Trust is tied
      entirely to the HTTPS endpoint; clients cannot verify provenance
      across domains. Enumeration resistance, rate limiting, and abuse
      controls are deployment specific and not standardised. A
      compromised server can return forged or misleading metadata
      without detection.

  - Privacy
    - Risks: JRD responses may expose personal or sensitive information
      such as profile attributes, service endpoints, or relationships.
      Servers that respond differently for valid and invalid subjects
      may leak account existence. Without strict filtering, WebFinger
      can reveal information that enables profiling or cross‑service
      correlation.

    - Controls: RFC 7033 recommends cautious publication, but does not
      define structured privacy controls, consent mechanisms, or privacy
      flags. Operators must implement their own access control,
      redaction, and rate limiting to avoid leakage. Without these
      measures, WebFinger can compromise privacy or commercial
      confidentiality.

  - DAWN suitability: Partial (identifier‑resolution only)
    - WebFinger is well suited for resolving known identifiers to
      structured metadata within a single administrative domain.
    - It is not a DAWN‑style public, multi‑entity, descriptive Discovery
      Mechanism.
    - It does not provide semantic search, multi‑match discovery,
      cross‑domain ranking, or task‑oriented discovery.
    - It assumes that the client already possesses the subject
      identifier and that the server is authoritative for that
      identifier.
    - WebFinger can serve as a resolution layer in DAWN, but not as a
      general discovery substrate.

  - Security, Privacy, and DAWN suitability score: **1/3**
    - Webfinger implements a lightweight resolution mechanism with a
      flexible JSON‑based structure, but lacks scalability,
      interoperability, security, and privacy features required for
      DAWN‑grade discovery. WebFinger is suitable only for
      identifier‑based lookups and does not provide the protections,
      controls, or semantic capabilities needed for multi‑entity,
      cross‑domain discovery.

- **Mitigations grouped by goal**
  - Mitigations for Descriptor hosting and integrity
    - Require signed JRD responses or signed metadata objects when
      WebFinger is used in cross‑domain or adversarial environments.
      Publish verification keys via operator PKI, JWK sets, or DID
      documents, and enforce signature verification in clients before
      trusting any returned properties or links.
    - Cost: Medium – Requires signing libraries, schema adjustments,
      key‑management integration, and client‑side verification logic.
    - Impact: Prevents forged responses, ensures provenance, and enables
      non‑repudiation for downstream selection or resolution decisions.

  - Mitigation for Privacy and anti‑enumeration
    - Mitigation: Limit information returned to unauthenticated queries,
      apply RBAC and token‑based access for sensitive fields, enforce
      rate limits, and avoid response patterns that reveal account
      existence. Use aggregation or redaction when exposing metrics or
      relationship data.
    - Cost: Medium – Requires access‑control enforcement, rate‑limiting
      infrastructure, and privacy‑aware response policies.
    - Impact: Reduces profiling, enumeration, and leakage of personal or
      sensitive information while preserving legitimate resolution
      functionality.

  - Mitigation for Cross‑domain descriptive search
    - Mitigation: Do not overload WebFinger as a search substrate.
      Publish minimal signed pointers or attestations into a separate
      catalog that supports descriptive queries. The catalog returns
      candidate identifiers, which clients then resolve via WebFinger
      under controlled access and verification.
    - Cost: High – Requires catalog construction, attestation formats,
      federation rules, and access‑control mechanisms.
    - Impact: Enables DAWN‑style descriptive discovery while preserving
      provenance, privacy, and operator control.

  - Mitigation for Freshness and revocation
    - Include explicit validity windows in published metadata, provide
      status and revocation endpoints, and use push‑based mechanisms to
      propagate updates. Enforce short lifetimes for dynamic attributes
      or ephemeral offers.
    - Cost: Medium to High – Requires revocation infrastructure, update
      channels, and more frequent metadata refresh.
    - Impact: Reduces stale or incorrect metadata, limits exposure to
      compromised information, and improves correctness for
      time‑sensitive discovery.

  - Mitigation for Cross‑domain descriptive search (federation and
    provenance)
    - Exchange signed attestations rather than raw metadata between
      operators. Require provenance chains and trust anchors for each
      federation member, and enforce policy translation and explicit
      consent for sharing subject metadata.
    - Cost: High – Requires attestation formats, trust‑management
      systems, governance agreements, and operational coordination.
    - Impact: Preserves provenance and trust across domains and enables
      controlled cross‑domain discovery and resolution.

  - overall mitigation score: **MEDIUM TO HIGH**

## Search & crawling

List includes: Web crawlers, site indexes, capability search engines,
and Vector indexes and semantic matchers for capability search.

**To be completed**

## Centralized marketplaces

List includes: Vendor app stores, plugin registries, dataset catalogs.

**To be completed**

## P2P/DHT and decentralized registries

**To be completed**

## Manual/configuration-based discovery

- **Summary**: Manual or configuration‑based discovery refers to
  environments where entities, endpoints, or services are discovered
  through static configuration rather than automated mechanisms.
  Examples include manually entering IP addresses, URLs, service
  endpoints, credentials, or metadata into configuration files,
  orchestration systems, or device settings. This approach is common in
  tightly controlled deployments, legacy systems, embedded environments,
  and small‑scale networks where automation is unnecessary or
  undesirable.

- **How it works**: Operators or administrators explicitly configure
  discovery parameters depending on the scenario under consideration.
  These parameters may include static addresses or identifiers, service
  endpoints or URLs, credentials or tokens, routing or workflow rules,
  and metadata describing capabilities or roles. Manual configuration is
  typically used in environments where entities are known in advance and
  where dynamic discovery is unnecessary or intentionally avoided. If
  physical or logical connectivity changes, operators must update the
  configuration accordingly. The resulting discovery information is
  embedded into static structures such as lookup tables, configuration
  files, orchestration manifests, or device‑level settings. Clients do
  not perform discovery; they simply read the configured information and
  act on it.

- **Security, Privacy, and DAWN suitability Considerations:**
  - Security
    - Strengths:
      - Manual configuration avoids many attack surfaces associated with
        automated discovery protocols.
      - Operators maintain full control over what is reachable, reducing
        exposure to unsolicited or untrusted entities.
      - Static configurations can be protected through existing
        access‑control and configuration‑management systems.

    - Weaknesses:
      - Stale or incorrect configurations can persist indefinitely and
        misroute traffic or expose sensitive endpoints.
      - Manual errors can introduce vulnerabilities, misconfigurations,
        or unintended trust relationships.
      - No built‑in authentication, integrity, or provenance for
        configured entries; trust is entirely operator‑dependent.
      - Does not scale to dynamic or adversarial environments where
        entities appear, disappear, or change frequently.

  - Privacy
    - Risks:
      - Static lists can leak operational structure if shared or
        replicated across domains.
      - Manual distribution of configuration files increases the risk of
        accidental disclosure.
      - Entrusting configuration of private information into the hands
        of operators reduces control over information leakage.
    - Controls:
      - Strong access control on configuration repositories and
        deployment pipelines.
      - Regular audits to remove stale entries and sensitive metadata.
      - Encryption of configuration files at rest and in transit and
        while updating configurations.
  - DAWN suitability: Minimal (static and non‑scalable)
    - Manual discovery is suitable only for small, static,
      operator‑controlled environments where entities are known in
      advance.
    - It does not support DAWN‑style public, multi‑entity, descriptive
      discovery.
    - It lacks semantic search, capability matching, cross‑domain
      interoperability, and dynamic updates.
    - It assumes a trusted operator domain and does not provide
      mechanisms for discovery across administrative boundaries.
    - It lacks flexibility, ease of operation, and is costly to maintain
      information freshness.
    - Manual discovery may serve as a fallback or bootstrap mechanism to
      discovery substrate componenets and fixed elements, but it cannot
      function as a general discovery mechanism for DAWN to provide its
      intended discovery services.

  - Security, Privacy, and DAWN suitability score: **1/3**
    - Manual or configuration‑based discovery provides predictable,
      operator‑controlled behavior, but it lacks scalability,
      interoperability, and dynamic adaptability. It offers minimal
      built‑in security or privacy protections and does not support
      DAWN‑style multi‑entity as it is often used within small networks,
      lacks descriptive and/or cross‑domain discovery. It is suitable
      only for small, static, trusted environments and cannot serve as a
      general discovery mechanism for DAWN.

- **Mitigations grouped by goal**
  - Mitigations for Descriptor hosting and integrity
    - Mitigation: Requires signed configuration bundles or signed
      metadata files. Store verification keys in operator PKI or
      configuration‑management systems, and enforce signature
      verification before applying any configuration.
    - Cost: Medium - Requires signing tools, key‑management integration,
      and validation logic in deployment pipelines.
    - Impact: Prevents tampering, ensures provenance, and reduces the
      risk of misconfiguration due to unauthorized edits.

  - Mitigation for Privacy and anti‑enumeration
    - Mitigation: Redact sensitive metadata, apply RBAC to configuration
      repositories, enforce least‑privilege access, and avoid
      distributing full topology or endpoint lists to unnecessary
      components.
    - Cost: Medium - Requires access‑control systems, audit processes,
      and policy enforcement.
    - Impact: Reduces leakage of internal structure and prevents
      unauthorized enumeration of services.

  - Mitigation for Cross‑domain descriptive search
    - Mitigation: Do not rely on manual configuration for cross‑domain
      discovery. Instead, publish minimal signed pointers or references
      into a catalog that supports descriptive queries. Manual entries
      should only reference catalog endpoints, not full service lists.
    - Cost: High - Requires catalog infrastructure, attestation formats,
      and federation rules.
    - Impact: Enables DAWN‑style discovery while keeping manual
      configuration limited to trusted bootstrap information.

  - Mitigation for Freshness and revocation
    - Mitigation: Include explicit validity periods in configuration
      bundles, require periodic refresh, and use automated alerts when
      configurations become stale. Provide revocation channels for
      compromised or outdated entries.
    - Cost: Medium to High - Requires monitoring, versioning, and
      revocation infrastructure.
    - Impact: Reduces stale configurations, improves correctness, and
      limits exposure to outdated or compromised information.

  - Mitigation for Cross‑domain descriptive search (federation and
    provenance)
    - Mitigation: Exchange signed attestations rather than raw
      configuration data between operators. Require provenance chains
      and trust anchors for each federation member, and enforce explicit
      consent for sharing configuration‑derived metadata.
    - Cost: High - Requires attestation formats, trust‑management
      systems, and governance agreements.
    - Impact: Preserves provenance and trust across domains and enables
      controlled cross‑domain discovery.

  - Overall mitigation score: **MEDIUM TO HIGH**

# Security Considerations

TBC

# Operational Considerations

TBC

# IANA Considerations

This document makes no requests of IANA.

# Acknowledgements

TBC
