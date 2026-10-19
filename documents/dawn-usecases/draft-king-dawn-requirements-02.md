---
coding: utf-8

title: Requirements for the Discovery of Agents With Names (DAWN)

abbrev: DAWN Requirements
docname: draft-king-dawn-requirements-02
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

author:
  -
    ins: D. King
    name: Daniel King
    org: Old Dog Consulting
    country: UK
    email: daniel@olddog.co.uk

  -
    ins: A. Farrel
    name: Adrian Farrel
    org: Old Dog Consulting
    country: UK
    email: adrian@olddog.co.uk

--- abstract

The proliferation of distributed systems, Artificial Intelligence (AI)
agents, and network services has created a need for interoperable
mechanisms to discover entities across administrative and network
boundaries.  Entities may include AI agents, software services, and
other named resources that need to be found and characterised before
interaction can begin.

This document defines the requirements for Discovery of Agents With
Names (DAWN) and sets out the objectives that a discovery mechanism for
such entities must satisfy.  It describes what information
must be discoverable, what properties a discovery mechanism needs to
support, and what constraints apply to discovery in decentralised
environments.

This document does not specify any particular discovery protocol or
solution.

--- middle

{: #sec-intro}
# Introduction

Modern distributed systems increasingly rely on the dynamic composition
of services and agents that may not have pre-configured relationships.
For example, an AI agent may need to find another agent with specific
capabilities, or a service consumer may need to discover providers that
support a required protocol version.
Further use cases and scenarios are described in
{{?I-D.kay-dawn-use-cases}}.

In each case, an entity needs knowledge of remote entities before
interaction can proceed: what they are, what they offer, and whether
they can be trusted.  Such knowledge could be obtained through static
configuration, but this approach is impractical at scale and across
organisational boundaries.  Automated discovery mechanisms are therefore
needed.

Today, where automated discovery exists, it is typically handled through
proprietary directories or platform-specific mechanisms.  These
approaches do not scale across organisational boundaries and create
fragmented ecosystems where entities cannot find entities managed by
other organisations.

An interoperable discovery mechanism is needed that builds on existing
protocols and tools, benefits from an established trust model, supports
proven delegation and federation architectures, and allows organisations
to independently publish discovery information.

This document defines requirements that any Discovery of Agents With
Names (DAWN) mechanism must satisfy.  It is informed by
{{?I-D.akhavain-moussa-dawn-problem-statement}} and
{{?I-D.mozley-aidiscovery}}, and uses the terminology of
{{!I-D.farrel-dawn-terminology}}.

{: #sec-scope}
## Scope of this Document

The requirements in this document address what information must be
discoverable about entities, what properties a discovery mechanism must
support, and what architectural constraints apply.  The detailed
requirements are set out in {{sec-requirements}}.

Discovery, as used here, is the initial step by which a discovering
entity obtains the public Minimum Discoverable Information (MDI) about
an entity.  It applies within a local network, within an organisation,
and between cooperating parties over the public Internet.

These requirements are intended to be solution-neutral.  They do not
require discovery information to be carried in any particular protocol
element or data record.  {{sec-prop}} sets out how information may be
provided by value or by reference.

The following topics are explicitly out of scope of this document:

- Open-ended search, semantic matchmaking, ranking, and selection of
  entities;

- Capability information beyond the MDI, including catalogues of
  capabilities;

- All communication beyond the initial discovery process;

- Indexing and searching of entities across the wider Internet;

- Entity registration processes, including attestation and other
  security mechanisms for registration;

- Design, definition, and governance of naming systems for entities;

- Identity management, authentication, and authorisation of entities
  themselves (as distinct from the integrity of discovery information);

- Trust management and trust evaluation beyond the secure exchange of
  discovery information;

- Capability exchange and negotiation between entities;

- Task management and orchestration.

{: #sec-terms}
# Terminology

This document uses the following terms defined in {{!I-D.farrel-dawn-terminology}}:

- Agent

- Capability

- Capability Card

- Capability Exchange

- Discovered Entity

- Discovering Entity

- Discovery

- Discovery Information

- Discovery Mechanism

- Discovery Scope

- Entity

- Function

- Minimum Discoverable Information (MDI)

- Named Entity

- Properties

- Selection

- Trust Indicator

## Conventions and Definitions

Although this is an informational requirements document, key words in
upper case are used for clarity of stating the requirements. The key
words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in
BCP 14 {{!RFC2119}} {{!RFC8174}} when, and only when, they appear in all
capitals, as shown here.

{: #sec-requirements}
# Requirements

The requirements are organised into the following categories: discovery
scenarios, discovery information, trust and security, scalability and
architecture, discovery protocol, and extensibility.

{: #sec-disc}
## Discovery Scenarios

REQ-DISC-1:
: A discovery mechanism MUST support the discovery of both specific
  entity instances and classes of entities that can perform a desired
  function.

REQ-DISC-2:
: A discovery mechanism MUST be applicable within a local network,
  within an organisation, and between cooperating parties over the
  public Internet.  Different mechanisms MAY be specified for different
  deployment contexts.

REQ-DISC-3:
: A discovery mechanism SHOULD support referral to another entity, such
  as a catalogue or directory service, that can further the discovery
  process.  The information such a service exposes beyond the MDI is
  out of scope.

REQ-DISC-4:
: Discovery is initiated from a name or scope known to the discovering
  entity.  A discovery mechanism MUST allow a discovering entity to
  express the discovery scope of a discovery operation in one or more
  dimensions, and SHOULD indicate whether that scope has been fully
  searched or the results have been truncated.

{: #sec-prop}
## Discovery Information

REQ-PROP-1:
: A discovery mechanism MUST define the Minimum Discoverable Information
  (MDI) that every discoverable entity provides.  The MDI MUST include
  at least the entity's type, the services it offers, its reachability
  information, and the communication protocols and any security
  parameters needed to interact with it.  Properties beyond the MDI are
  optional.

REQ-PROP-2:
: The MDI MUST be available by value.  Information beyond the MDI MAY
  be provided by reference.  A discovery mechanism MUST specify the
  maximum depth of indirection a discovering entity is expected to
  follow, and the behaviour when that depth is exceeded.

REQ-PROP-3:
: A discovery mechanism MUST specify the behaviour of a discovering
  entity when a reference cannot be used, distinguishing at least the
  cases where the reference does not resolve, where resolution is
  prevented by the discovering entity's own retrieval policy, and where
  the reference resolves but the referenced information is absent.  A
  finding of absence MUST be based on a complete result for the
  requested lookup; an incomplete result MUST NOT be reported as
  absence.

REQ-PROP-4:
: A discovery mechanism SHOULD allow a reference to a capability card
  or equivalent machine-readable description of an entity's interface
  and functions.  The format, content, and exchange of such descriptions
  are out of scope.

REQ-PROP-5:
: A discovery mechanism MUST indicate whether discovery information is
  static or dynamic, together with any validity or freshness
  information needed for caching and refresh.

{: #sec-sec}
## Trust and Security

REQ-SEC-1:
: A discovery mechanism MUST provide a means to verify the origin and
  integrity of discovery information, for example through digital
  signatures, and MUST be resilient to attacks that poison, corrupt, or
  replay that information.

REQ-SEC-2:
: A discovery mechanism SHOULD allow an entity to control the
  visibility of its properties to different audiences (e.g., public
  versus organisation-internal discovery), and allow an operator to
  control which entities are discoverable in a given context.

REQ-SEC-3:
: A discovery mechanism MUST be designed to limit its use as a vector
  for abuse, including amplification, scraping, denial-of-service, or
  unauthorised disclosure of discovery information.

{: #sec-arch}
## Scalability and Architecture

REQ-ARCH-1:
: A discovery mechanism MUST be capable of operating in decentralised
  architectures without a single centralised registry, and MUST scale
  across a large number of entities and administrative domains.

REQ-ARCH-2:
: A discovery mechanism SHOULD allow organisations to independently
  publish discovery information without depending on a third-party
  directory.

{: #sec-proto}
## Discovery Protocol

REQ-PROTO-1:
: A discovery mechanism SHOULD be built in a modular way using existing
  Internet Engineering Task Force (IETF) protocols, such as DNS and
  mDNS, where possible, filling gaps only where existing protocols are
  insufficient.

REQ-PROTO-2:
: A discovery mechanism MUST define a predictable entry point for
  discovery that is based on ubiquitous and interoperable mechanisms.

{: #sec-ext}
## Extensibility

REQ-EXT-1:
: A discovery mechanism MUST support the addition of new entity types
  and properties, including domain-specific extensions, through
  structured, versioned schemas that allow backward-compatible
  evolution without changes to the core mechanism.

{: #sec-iana}
# IANA Considerations

This document does not make any requests of IANA.

{: #sec-security}
# Security Considerations

This document defines requirements for entity discovery mechanisms.  It
does not define a protocol and therefore does not introduce specific
security vulnerabilities.  However, the requirements in {{sec-sec}} place
security constraints on any solution that satisfies these requirements.

Implementers of discovery mechanisms that satisfy these requirements
should pay particular attention to the following concerns:

- The integrity and authenticity of discovery information must be
  protected to prevent poisoning attacks that could direct entities to
  malicious endpoints.

- Integrity protection of discovery information does not, by itself,
  authenticate a discovered entity as the live peer in a subsequent
  protocol exchange.

- The security properties that can be provided differ by deployment
  context.  A specification should state which of origin verification,
  integrity, and confidentiality it provides in each context it
  supports.

- Access control mechanisms should be considered to prevent
  unauthorised disclosure of entity properties, particularly in
  environments where entity metadata may be sensitive.

- The discovery mechanism itself must not become a vector for
  denial-of-service attacks against the infrastructure on which it is
  built.

{: #sec-privacy}
# Privacy Considerations

Discovery mechanisms inherently involve the publication of information
about entities.  Implementers should consider the privacy implications
of exposing entity properties, capabilities, and organisational
associations.  In particular:

- Entities should be able to control what information is made publicly
  discoverable versus restricted to specific audiences.

- The discovery mechanism should not require the disclosure of
  information beyond what is necessary for a discovering entity to
  determine whether interaction is appropriate.

- A specification of a discovery mechanism should state whether its
  design resists enumeration of the entities it makes discoverable.
  Unless it does, the set of discoverable entities should be assumed to
  be public.

- Where entities represent individuals or process personal data,
  compliance with applicable data protection regulations should be
  considered.

{: #sec-operational}
# Operational Considerations

Discovery mechanisms that satisfy these requirements will need to be
deployable across public and private networks, across organisational
boundaries, and across heterogeneous operational environments.  Operators
should consider publication workflows, update and withdrawal procedures,
caching and refresh behaviour, observability, operational policy, and
the impact of discovery traffic on the infrastructure used to support
the mechanism.

# Acknowledgements

The authors wish to acknowledge the contributions of participants in the
DAWN discussions that shaped this document, including Jim Mozley,
Balazs Nemethi, Chenguang Du, Francesco Marinoni Moretto, Girish Konda,
Songbo Bu, and Jamal Le Blanc.
