---
coding: utf-8

title: Terminology for the Discovery of Agents With Names (DAWN)

abbrev: DAWN Terminology
docname: draft-farrel-dawn-terminology-06
workgroup:
category: info
ipr: trust200902
stream: IETF

stand_alone: yes
pi: [toc, tocompact, tocindent, sortrefs, symrefs, compact]

area: INT
kw:
  - discovery
  - agents
  - AI

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

The proliferation of distributed Artificial Intelligence (AI) systems and 
agents has created a need for interoperable mechanisms for components of AI 
systems to discover each other.

This document defines terminology for Discovery of Agents With Names (DAWN), focusing
on the terms necessary to describe the discovery of information about AI systems and
resources (e.g., AI agents).  The intention is that this common set of
terms can be used by other documents related to DAWN and so achieve
consistency of meaning across the space.

--- middle

{: #sec-intro}
# Introduction

Distributed systems increasingly rely on the dynamic composition
of services, agents, and workloads that may not have pre-configured connectivity
relationships.  In an AI-based system, an AI agent may need to find another agent
with specific capabilities.

In these cases an AI agent needs knowledge of remote agents before
interaction can proceed: what they are, what they offer, and whether
they can be trusted.  Such knowledge could be obtained through static
configuration, but this approach is impractical at scale and across
organisational boundaries.  Automated discovery mechanisms are therefore
needed.

Today, where automated discovery of AI agents exists, it is typically handled through
proprietary directories or platform-specific mechanisms.  These
approaches do not scale across organisational boundaries and create
fragmented ecosystems where entities cannot find entities managed by
other organisations.

An interoperable mechanism for the discovery of AI systems and
resources (e.g., AI agents) is needed that builds on existing
protocols and tools, benefits from an established trust model, supports
proven delegation and federation architectures, and allows organisations
to independently publish discovery information.

This document defines common terminology for use in documents that discuss
Discovery of Agents With Names (DAWN).

{: #sec-scope}
## Discovery Scope

[Editor's Note: This section probably belongs in an Architecture document and not here.]

It will be helpful to understand the broader discovery ecosystem. Information must 
be registered to the discovery system, may be managed and updated, can then be 
discovered by other AI agents. But the discoverable information must be balanced as
a compromise between too much detail which will overload the discovery process or
be duplicative and thus cause maintenance issues, and too little information which
would make discovery suboptimal.

Additional detailed information may be exchanged following initial discovery,
and this part of the process may also include negotiation of capabilities.

In the end, this means that the "discovery ecosystem" can be broken down into at least the
following functions:

- Registration and management of an entity to be discovered.
- Search based on a formalised encoding of search criteria.
- Discovery lookup based on a minimum viable dataset (protocol, identifying properties) with return of a set of minimum discoverable information (including reachability).
- Reading of additional information.
- Capability exchange and negotiation.

From an implementation perspective, some of these functional components might be included within the same module, and it is possible that some elements might be achieved using the same protocols. However, for the sake of this document and the DAWN work, only the discovery lookup is in scope.

{: #sec-terms}
# Terminology

The terms presented in this section are in alphabetic order for ease of
reference.  For those wishing to read this document to gain an understanding
of the DAWN scenery, it is recommended to read the terms in the order presented
in {{term-table}}.

~~~~

| Core term    | Subsidiary term                  |
|--------------|----------------------------------|
| Entity       |                                  |
|              | Named Entity                     |
|              | Agent                            |
|              | AI Agent                         |
|              | AI Resource                      |
|              | AI System                        |
|              | Discovering Entity               |
|              | Discovered Entity                |
| Discovery    |                                  |
|              | Discovery Information            |
|              | Discoverable Object              |
|              | Minimum Viable Dataset           |
|              | Minimum Discoverable Information |
|              | Discovery Mechanism              |
|              | Discovery Scope                  |
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

AI Agents:
: A specific class of agent that employ artificial intelligence
  techniques.

AI Resource:
: An identifiable entity or service that provides AI-related functionality, enables
  access to such functionality, or facilitates the discovery of other AI resources. Examples 
  include AI agents, AI models, and AI inference services.  An AI resource does
  not necessarily perform AI processing itself and may represent an entire AI system or an
  individually accessible component of one.

AI system: 
: A system that uses AI to process inputs and generate outputs such as predictions, 
  content generation, recommendations, or decisions, to achieve objectives.  An AI system may
  comprise multiple interacting components such as AI agents or AI resources.

Attributes:
: The properties, features, capabilities, skills, etc., that an entity
  possesses or may have access to, such as skill type,
  communication language, capacity, task description, contact information,
  ID, etc. The attributes of an entity form a full detailed set of information
  about the entity not all of which is necessarily available to be discovered
  or communicated to other entities. (See also, properties and capability.)

Capability:
: A description of the functions, services, or actions that an entity
  can perform. Capabilities may be described using structured schemas
  such as capability cards.

Capability Card:
: A structured, machine-readable description of an entity's
  capabilities and interface.  Variants include agent cards, task cards,
  resource cards, tool cards, and skill cards depending on the type of
  entity. A capability card may also include human-readable information
  as well as authentication/security certification data.

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
  defines what an entity is, what attributes it possesses, how to reach the
  associated entity, etc.  May be represented as a capability card.

Discoverable Object Validation:
: The process that verifies a discoverable object, ensures its compliance
  to referenced standards, and makes it available to be discovered.

Discovered Entity:
: An entity whose properties are returned as the result of a discovery
  process. A discovered entity may be a specific instance or a member of
  a class of entities that can perform a desired function. In the context of
  DAWN, a discovered entity is an AI system or AI resource (e.g., an AI agent).

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
  and desirable. This should be considered in terms of the Minimum 
  Discoverable Information (q.v.) of which Discovery Information is a 
  subset, and compared with the broader set of information that forms
  part of the Capability Exchange (q.v.).

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
  peer-to-peer or client-server relationship.  In the context of DAWN, entities
  include, but are not limited to, AI agents and AI resources.  However,
  see the definition of "Discovered Entity."

Function:
: The functional processing capability that an entity offers. Examples
  include task execution, data transformation, inference, routing, steering,
  storage, and orchestration.

Minimum Discoverable Information (MDI):
: The minimum amount of information an entity needs to provide to become
  discoverable.

Minimum Viable Dataset (MVD):
: The data that must be provided to the discovery mechanism to enable it to return 
  indications of Discovered Entities.

Named Entity:
: An entity that is identified by a stable name within a naming system.
  The naming system may be hierarchical (e.g., DNS) or flat.

Properties:
: The discoverable characteristics of an entity.  Properties include, but
  are not limited to, communication protocols, capability cards, location,
  trust indicators, and operational status. (Compare with attributes.)

Registrar:
: An entity or system responsible for accepting and maintaining records
  about entities that wish to be discoverable. Acts as a go-between for
  registrants and registries through the process of registration.  Note
  that not all registrations require the use of a registrar, and that the
  registrar in a DAWN system is not necessarily the DNS registrar {{?RFC9499}}.

Registration:
: The steps by which agents can register their existence via a registrar.
  This should include attestation and other security mechanisms.
: Registration
  is out of scope for DAWN, but the information that can be discovered and the
  trust with which that information is treated are key to any complete system.

Selection:
: The mechanisms and policies by which an entity determines which
  discovered entities it will interact with.
:  Selection is out of scope
  for DAWN, but depends on information obtained through discovery.

Trust Indicator:
: Information associated with an entity that allows a discovering party
  to assess the trustworthiness or provenance of the entity and its
  advertised properties.  Examples include digital signatures,
  certificates, and attestations.

{: #sec-iana}
# IANA Considerations

This document does not make any requests of IANA.

{: #sec-security}
# Security Considerations

This document only defines a set of terms.  It does not introduce any
issues that require security consideration.

However, this document does define Trust Indicator, attestation-dependent Registration,
and scope-based policy enforcement, and so it should be clear that discovery has significant
security and privacy implications.  It is anticipated that these will be addressed
in the DAWN solution/architecture documents.

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

Jim Mozley, Med Boucadair, Chenguang Du, Daniel King, Benoit Claise,
Kaveh Ranjbar, Muhammad Awais Jadoon, and Aditya Dogra provided useful reviews
of this document.
