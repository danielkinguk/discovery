---
coding: utf-8

title: Terminology for the Discovery of Agents, Workloads, and Named Entities (DAWN)

abbrev: DAWN Terminology
docname: draft-farrel-dawn-terminology-03
workgroup:
category: info
ipr: trust200902
stream: IETF

stand_alone: yes
pi: [toc, tocompact, tocindent, sortrefs, symrefs, compact]

area: TBD
kw:
  - discovery
  - agents
  - workloads

author:
  -
    ins: A. Farrel
    name: Adrian Farrel
    org: Old Dog Consulting
    country: UK
    email: adrian@olddog.co.uk
  -
    ins: K. Yao
    name: Kehan Yao
    org: China Mobile
    country: China
    email: yaokehan@chinamobile.com
  -
    ins: R. Schott
    name: Roland Schott
    org: Deutsche Telekom
    country: Germany
    email: Roland.Schott@telekom.de
  -
    ins: N. Williams
    name: Nic Williams
    org: Infoblox
    country: USA
    email: nwilliams@infoblox.com

--- abstract

The proliferation of distributed systems, Artificial Intelligence (AI)
agents, cloud workloads, and network services has created a need for
interoperable mechanisms to discover entities. Entities may include AI agents, software services,
compute workloads, and other named resources that need to be found and
characterised before interaction can begin.

This document defines terminology for Discovery of Agents, Workloads,
and Named Entities (DAWN).  The intention is that this common set of
terms can be used by other documents related to DAWN and so achieve
consistency of meaning across the space.

--- middle

{: #sec-intro}
# Introduction

Distributed systems increasingly rely on the dynamic composition
of services, agents, and workloads that may not have pre-configured connectivity
relationships.  For example, an AI agent may need to find another agent
with specific capabilities, a workload orchestrator may need to locate
compute resources in a particular jurisdiction, or a service consumer
may need to discover providers that support a required protocol or a data schema version.
Further use cases and scenarios may be considered, but it is out of scope
to enumerate them.

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

This document defines common terminology for use in documents that discuss
Discovery of Agents, Workloads, and Named Entities (DAWN).

{: #sec-scope}
## Discovery Scope

It will be helpful to understand the broader discovery ecosystem. Information must 
be registered to the discovery system, may be managed and updated, can then be 
discovered by other entities. But the discoverable information must be balanced as
a compromise between too much detail which will overload the discovery process, and
too little information which would make discovery suboptimal.

Additional detailed information may be exchanged between entities and this part of the
process may also include negotiaton of capabilities. 

In the end, this means that the "discovery ecosystem" can be broken down into at least the
following functions:

- Registration and management of an entity to be discovered.
- Search based on a formalised encoding of search criteria.
- Discovery lookup based on a minimum viable data set (protocol, identifying properties) with return of a minimum set of discoverable information (including reachability).
- Reading of additional information.
- Capability exchange and negotiation.

From an implementation perspective, some of these functional components might be included within the same module, and it is possible that some elements might be achieved using the same protocols. However, for the sake of this document and the DAWN work, only the discovery lookup is in scope.

{: #sec-terms}
# Terminology

The terms presented in this section are in alphabetic order for ease of
reference.  For those wishing to read this document to gain an understanding
of the DAWN scenery, if it recommended to read the terms in the order presented
in {{term-table}}.

~~~~

| Core term    | Subsidiary term                  |
|--------------|----------------------------------|
| Entity       |                                  |
|              | Named Entity                     |
|              | Agent                            |
|              | Workload                         |
|              | Task                             |
|              | Discovering Entity               |
|              | Discovered Entity                |
| Discovery    |                                  |
|              | Discovery Information            |
|              | Discoverable Object              |
|              | Minimum Discoverable Information |
|              | Discovery Mechanism              |
|              | Disovery Scope                   |
| Capability   |                                  |
|              | Function                         |
|              | Attributes                       |
|              | Properties                       |
|              | Capability Card                  |
|              | Trust Indicator                  |
| Registration |                                  |
|              | Capability Exposure              |
|              | Registrar                        |
|              | Discoverable Object Validation   |
| Selection    |                                  |
|              | Capability Exchange              |

~~~~
{: #term-table title="Key DAWN Terms in a Readable Order" artwork-align="center"}


Agent:
: A software entity that acts autonomously or semi-autonomously on behalf of a
  user, organisation, or system.  An agent may initiate interactions
  with other entities, make decisions, and perform tasks.
:  AI agents are
  a specific class of agent that employ artificial intelligence
  techniques.

Attributes:
: The properties, features, capabilities, skills, etc., that an entity
  possess or may have access to such as capabilities, skill type,
  communication language, capacity, task description, contact information,
  ID, etc. (See also, properties.)

Capability:
: A description of the functions, services, or actions that an entity
  can perform. Capabilities may be described using structured schemas
  such as capability cards.

Capability Card:
: A structured, machine-readable description of an entity's
  capabilities and interface.  Variants include agent cards, task cards,
  resource cards, tool cards, and skill cards depending on the type of
  entity.

Capability Exposure:
: The processes by which entities expose their capabilities. Such exposure
  may be part of the registration or management of discovery information prior to the discovery processes, or achieved
  through an interaction with an entity. (See also, Capability Exchange.)

Capability Exchange:
: The processes by which entities exchange details between each other of what they can do,
  dynamic status information, and which particular features or functions
  they wish to engage.
  
: Capability exposure, exchange, and negotiation are out of scope for DAWN, but
  will form an essential part of the entity ecosystem enabling the selection and
  operation of entities.

Discoverable Object:
: An information object that is discoverable and includes information that
  defines what an entity is, what attributes it possess, how to reach to the
  associated entity, etc.  May be represented as a capability card.

Discoverable Object Validation:
: The process that verifies a discoverable object, ensures its compliance
  to referenced standards, and makes it available to the discovery substrate.

Discovered Entity:
: An entity whose properties are returned as the result of a discovery
  process. A discovered entity may be a specific instance or a member of
  a class of entities that can perform a desired function.

Discovering Entity:
: An entity (or its operator) that initiates the discovery process in
  order to find other entities to interact with.

Discovery:
: The process by which an entity or its operator locates other entities
  that are capable of performing a desired function or providing a
  desired service, and obtains sufficient information to initiate
  interaction.

Discovery Information:
: The information returned by a discovery mechanism that allows the 
  discovering entity to decide whether later interaction is possible
  and desireable. This should be considered in terms of the Minimum 
  Discoverable Information (q.v.) and compared with the broader set of
  information that forms part of the Capabilities Exchange (q.v.).

Discovery Mechanism:
: A protocol, system, or method used to perform discovery.  Examples
  include Domain Name System (DNS) based service discovery, directory services, and
  distributed registries.

Discovery Scope:
: The explicit domain over which discovery is performed. Discovery scope may be 
  specified in one or more dimensions, including but not limited to administrative
  identifiers (e.g., DNS domain names, AS numbers), trust domains, topological or
  distance metrics, geographic or jurisdictional boundaries, and temporal
  constraints. Discovery scope bounds the search space and supports scalability,
  relevance, and policy enforcement.

Entity:
: A system component that communicates with other entities in a
  peer-to-peer or client-server relationship.  Entities include, but
  are not limited to, AI agents, tools, skills, tasks, compute workloads,
  software services, task owners, network functions, and application endpoints.

Function:
: The functional processing capability that an entity offers. Examples
  include task execution, data transformation, inference, routing, steering,
  storage, and orchestration.

Minimum Discoverable Information (MDI):
: The minimum amount of information an entity needs to provide to become
  discoverable. Think of it as common header of a data structure.

Named Entity:
: An entity that is identified by a stable name within a naming system.
  The naming system may be hierarchical (e.g., DNS) or flat.

Properties:
: The discoverable characteristics of an entity.  Properties include, but
  are not limited to, communication protocols, capability cards, location,
  trust indicators, and operational status.

Registrar:
: An entity or system responsible for accepting and maintaining records
  about entities that wish to be discoverable.

Registration:
: The steps by which agents can register their existence with a registrar.
  This should include attestation and other security mechanisms.
: Registration
  is out of scope for DAWN, but the information that can be discovered and the
  trust with which that information is treated are key to any complete system.

Selection:
: The mechanisms and policies by which an entity determines which
  discovered entities it will interact with.
:  Selection is out of scope
  for DAWN, but depends on information obtained through discovery.

Task:
: A legacy term kept for continuity with earlier work.  A task may be
  considered as software service.

Trust Indicator:
: Information associated with an entity that allows a discovering party
  to assess the trustworthiness or provenance of the entity and its
  advertised properties.  Examples include digital signatures,
  certificates, and attestations.

Workload:
: A unit of compute or processing that is deployed and executed within a
  hosting environment.  Workloads may be transient or long-lived and may
  move between hosting environments.

{: #sec-iana}
# IANA Considerations

This document does not make any requests of IANA.

{: #sec-security}
# Security Considerations

This document only defines a set of terms.  It does not introduce any
issues that require security consideration.

{: #sec-privacy}
# Privacy Considerations

This document only defines a set of terms.  It does not introduce any
issues that require privacy consideration.

{: #sec-operations}
# Operational Considerations

This document only defines a set of terms.  It does not introduce any
issues that require operational consideration.

# Acknowledgements

The authors wish to acknowledge the contributions of participants in
the DAWN discussions that shaped this document.

Jim Mozley, Med Boucadair, and Chenguang Du, and Daniel King provided 
useful reviews of this document.
