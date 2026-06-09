---
title: "Use Cases for the Discovery of Agents, Workloads, and Named Entities"
abbrev: "DAWN Use Cases"
category: info
docname: draft-kay-dawn-use-cases-00
submissiontype: IETF
number:
date:
consensus: false
v: 3
area: "Applications and Real-Time"
workgroup: "Individual Submission"
keyword:
  - discovery
  - agents
  - workloads
  - named entities
  - DAWN
venue:
  group: "Individual Submission"
  type: "Individual"
  mail: "dawn@ietf.org"
author:
  -
    name: Daniel King
    org: Old Dog Consulting
    email: "daniel@olddog.co.uk"
  -
    name: Kehan Yao
    org: China Mobile
    email: "yaokehan@chinamobile.com"
  -
    name: Ken Adler
    org: Indeed
    email: "kadler@indeed.com"
normative:
  I-D.farrel-dawn-terminology:
informative:
  I-D.akhavain-moussa-dawn-problem-statement:
  I-D.king-dawn-requirements:
  I-D.mozley-aidiscovery:
  I-D.agentic-ai-usecases-requirements:
  I-D.scrm-aiproto-usecases:

--- abstract

This document describes broad categories of use cases for the Discovery of
Agents, Workloads, and Named Entities (DAWN). The purpose of the document is to
illustrate situations in which entities need to discover other entities.

This document does not define a discovery protocol, a registration procedure, a
selection algorithm, or an agent-to-agent communication protocol.

--- middle

# Introduction

Distributed processing environments depend on interaction between
components that are often configured using static capability, location, or
reachability relationships. In order for these systems to operate efficiently,
components need to be capable of discovering other components that can provide a
function, service, resource, or capability.

For generality, Discovery of Agents, Workloads, and Named Entities (DAWN) uses
the term "entity" for the components that may be discovered. Entities may
include Artificial Intelligence (AI) agents, workloads, tasks, tools, services,
application endpoints, data sources, models, inference services, brokers, and
other named resources. Skills may also be among the discoverable attributes of
those entities.

The DAWN problem statement {{I-D.akhavain-moussa-dawn-problem-statement}}
describes the general discovery problem. The DAWN requirements document
{{I-D.king-dawn-requirements}} describes solution-neutral requirements for a
discovery mechanism. This document provides use cases that sit between those
documents: they show where discovery is needed and what information is needed
in representative scenarios.

This document defines the following categories of entity discovery:

1. Capability-Oriented Discovery, where an entity needs to discover another
   entity that can provide a function or capability.
2. Resource-Oriented Discovery, where discovery identifies resources
   used by agents, workloads, applications, or users.
3. Administrative Scope Extensions, where discovery crosses organisational,
   delegation, or tenancy boundaries.
4. Operational Discovery, where discovery supports operation, audit,
   troubleshooting, compliance, or automation.

The first two categories are base cases. The others describe common extensions
or deployments of those base cases.

Other Internet-Drafts describe agentic AI discovery use cases and communication
protocol requirements, including {{I-D.mozley-aidiscovery}},
{{I-D.agentic-ai-usecases-requirements}}, and
{{I-D.scrm-aiproto-usecases}}.

# Limitations of this Document

This document describes categories of discovery and associated use cases. It
does not describe the full lifecycle of an entity.

The following are in scope:

* discovery of a specific named entity;
* discovery of a class of entities that can provide a requested function;
* discovery of tasks that can be performed by suitable entities;
* discovery initiated by an agent, workload, service, application, or human
  operator;
* discovery of agents, workloads, tools, tasks, data sources, models, services,
  brokers, and other named entities;
* information that needs to be discovered before selection, negotiation, or
  communication can take place.

The following are out of scope:

* registration of entities for discovery;
* authentication or attestation of registrations;
* design, definition, or governance of naming systems;
* selection among candidate entities returned by discovery;
* capability negotiation after discovery;
* task orchestration;
* certificate or key lookup;
* search, ranking, or marketplace discovery.

The boundary between discovery and adjacent functions is important. A discovery
mechanism may return information that is used by later functions, but those
later functions are not themselves part of discovery.

Credential, key, certificate, or attestation references may still appear as
optional discovery information, but DAWN does not define their lookup or
validation.

# Terminology

Terminology for DAWN is defined in
{{I-D.farrel-dawn-terminology}}. This document uses the term "entity" in the
same broad sense as the DAWN terminology document.

Attention is drawn to the following specific terms defined in
{{I-D.farrel-dawn-terminology}} that are key to this document:

* discovering entity
* discovered entity
* discoverable object
* discovery information
* minimum discoverable information

# Discovery Characteristics

The categories of discovery and use cases discussed in this document share a
number of characteristics.

The common question is what minimum information about an entity needs to be
discoverable before later selection, negotiation, or communication can take
place.

* Discovery may be initiated by autonomous software or by a human operator.
* The discovered target may be a specific named entity or a set of entities
  determined by properties or classification.
* Discovery may happen within one administrative domain or across several
  administrative domains.
* Capability is often an important discovery input, but it is not the only one.
  Organisation, jurisdiction, locality, protocol, policy, and responsible party
  also appear in several use cases.
* Discovery information may include static, mainly static, and dynamic
  properties. This raises questions about freshness and
  caching when properties change frequently.
* Discovery may need to account for entities that are dynamic, mobile, or
  available only in a particular context.
* Trust in discovery information is different from trust in the discovered
  entity. A discovery mechanism can help protect discovery metadata, but it
  does not decide whether the discovered entity should be used.
* Brokers and aggregators may be useful in some environments, but DAWN ought
  not to require a single central registry.

# Discovery Pattern

The use cases in this document follow a common pattern.

1. A discovering entity has a task, intent, policy requirement, or operational
   need.
2. The discovering entity needs to find an entity, or class of entities, that
   can satisfy that need.
3. The discovering entity forms a discovery request using information such as
   a name, organisation, entity type, capability, location, jurisdiction,
   communication protocol, or policy constraint.
4. The discovery mechanism returns information about one or more candidate
   entities.
5. The discovering entity uses that information to decide whether selection,
   authorisation, capability exchange, or communication should be attempted.

The last step is outside the scope of discovery. However, discovery has to
return enough information for this step to be possible.

# Categories of Discovery {#categories-of-discovery}

Each discovery category includes assumptions, possible discovery impacts, and
illustrative examples.

## Capability-Oriented Discovery

In this discovery category, a discovering entity needs to find another entity
that can provide a specific function or capability. The discovered entity might
be an AI agent, a tool, a task, a service, an application endpoint, or a
model-serving function.

### Assumptions

This discovery category assumes that the discovering entity can describe the
required function in a form that can be used for discovery. It also assumes
that discoverable entities can publish, or point to, enough information about
their function and communication methods to allow a later decision about whether
to interact.

The capability description may be simple, such as a service type, or more
structured, such as a capability card or schema reference. DAWN does not define
the runtime invocation of the discovered capability.

### Discovery Impacts

Capability-oriented discovery suggests support for discovery by function,
capability, skill, entity type, and protocol. The returned discovery information
needs to include enough information to allow later selection, authorisation,
capability exchange, or communication to be attempted.

Discovery is not a statement that the discovered entity is safe,
competent, or authorised for a particular use. It provides discovery
information and associated trust indicators, while policy and selection are
later functions.

### Examples

A scheduling application is asked to arrange a meeting with people in another
organisation. It needs to discover whether that organisation exposes an entity
for calendar coordination, and what information is needed to contact it. The
discovery result might include the responsible organisation, supported
communication methods, and a reference to the entity's published capabilities.

An agentic workflow decomposes a user request into several subtasks. The
workflow needs to discover agents, tools, services, or tasks that can
participate in the work. Discovery provides candidate entities and their
published properties; the workflow then performs selection and orchestration
outside DAWN.

## Resource-Oriented Discovery

In this discovery category, an entity needs to discover resources that are not
simply peer agents or services. These resources may include data sources,
datasets, knowledge bases, compute resources, accelerator pools, models,
inference services, or similar resource-bound entities.

### Assumptions

This discovery category assumes that the discovered resource may have
properties that are partly static and partly dynamic. For example, a dataset
description may be relatively stable, while freshness or access policy may
change. A compute resource may have stable hardware properties but rapidly
changing availability, load, price, or locality.

It also assumes that some discovery information may be sensitive. Data
classification, model provenance, jurisdiction, permitted use, and operational
capacity may need visibility controls.

### Discovery Impacts

DAWN discovery needs a way to distinguish information that is appropriate for a
general discovery mechanism from information that should be obtained from a more
dynamic or restricted source. Discovery may return stable metadata and a pointer
to another service for current state, detailed policy, or authorisation.

The discovery result may need to include provenance, jurisdiction, freshness,
format, access method, safety classification, or other properties relevant to
later selection and policy checks.

### Examples

An agent needs to find a data source for retrieval-augmented generation. The
discovery input includes the data domain, freshness requirement, jurisdiction,
format, and access policy. The discovery result includes a description of the
data source, access method, policy information, and provenance references.

A workload scheduler needs to find compute with a particular accelerator type
and jurisdictional constraint. Discovery returns relatively stable compute
properties and information about how to obtain current availability.

An application needs to find an inference service for a particular modality and
safety classification. Discovery provides a service description, supported
protocols, policy constraints, version or provenance information, and trust
indicators.

A user or agent needs to discover a model for inference. Discovery provides
information about the model's function, supported use, access method, and
relevant policy constraints.

## Administrative Scope Extensions

In this discovery category, capability-oriented or resource-oriented discovery
crosses organisational, administrative, or tenancy boundaries. An entity may
need to discover another entity in a different organisation, or a provider may
need to expose different discovery views for different tenants, customers,
departments, or policy realms.

### Assumptions

This discovery category assumes that organisations need to control what they
publish and to whom it is visible. It also assumes that an entity may act on
behalf of a user, enterprise, tenant, department, or service, but that proof of
that authority is separate from discovery unless explicitly represented as
discovery information.

The discovery category also assumes that discovery information may need to carry
administrative-domain, responsible-party, policy, or trust-boundary
information. This information can help later authorisation, audit, or policy
functions, but DAWN does not define those functions.

### Discovery Impacts

DAWN discovery needs to support discovery across administrative domains without
requiring a single central registry. It also needs to support scoped discovery
where the information returned depends on tenant, customer, department, network,
or policy context.

Discovery information may need to include the responsible organisation, scope
of authority, policy constraints, and trust indicators associated with the
published metadata. Care is needed so that discovery does not expose sensitive
tenant or organisational structure to unauthorised parties.

### Examples

An enterprise agent acting for an employee needs to discover an authorised
agent at a supplier. The discovery result indicates how to contact the
supplier's agent and provides information needed by later authorisation and
policy checks.

A software-as-a-service provider hosts agents or tools for multiple customers.
Each customer needs discovery information scoped to its own tenancy. The same
provider may also need a different discovery view for internal operators,
external customers, and public users.

A research consortium spans several institutions. Each institution publishes
information about its own agents, data services, and tools. Collaborators need
to discover entities by capability while respecting institutional boundaries
and trust models.

## Operational Discovery

In this discovery category, discovery supports operation, audit,
troubleshooting, incident response, compliance review, or network and service
automation. The discovering entity may be a human operator, management system,
controller, or AI-assisted operations agent.

### Assumptions

This discovery category assumes that discovery is useful for both autonomous
systems and human-operated tools. It also assumes that operational environments
may be multi-vendor, multi-domain, and partly private.

Operational discovery may need to expose information about scope, owner,
responsible party, operational state, observability, or compliance status.
Some of this information may be restricted.

### Discovery Impacts

DAWN discovery may need to support tooling and operational inspection, not only
agent-to-agent workflows. Discovery metadata may need to be logged, auditable,
and understandable by operators.

Management and diagnostics for the discovery system itself may also be needed
so that operators can understand discovery behaviour and failures.

Intermediaries such as brokers, aggregators, directory services, telemetry
services, topology services, policy systems, or control functions may also be
discoverable entities.

### Examples

A human operator needs to find all entities owned by a team that expose a
particular function. Discovery provides inspectable metadata, a responsible
party, communication information, and trust indicators.

An AI-assisted network operations system needs to discover telemetry sources,
topology systems, control points, and remediation tools across a heterogeneous
network. DAWN can help identify the relevant entities. Diagnosis, correlation,
action recommendation, and remediation remain outside discovery.

An edge deployment includes lightweight agents that need fast and cacheable
discovery because local connectivity is constrained. Discovery provides enough
stable information for connection bootstrapping while avoiding reliance on
rapidly changing operational state.

# Classes of Use Case

{{I-D.akhavain-moussa-dawn-problem-statement}} introduces a taxonomy of entity
types in its Figure 2. These entity types provide a useful broad classification
of use cases that is expanded upon here. References are made back to the
categories of discovery discussed in {{categories-of-discovery}}, and
specifically the examples set out in the subsections of that section.

## AI Agent

TBD

## Software Service

TBD

## Compute Workload

TBD

## Network Function

TBD

## Application Endpoint

TBD

# Security Considerations

The use cases in this document involve discovery information that may affect
which entity is contacted, what protocol is used, and what trust indicators are
presented. Incorrect or malicious discovery information could cause a
discovering entity to contact the wrong entity, disclose information to an
attacker, or use an unsuitable service.

We suggest that any DAWN discovery mechanism will need to consider
authenticity, integrity, freshness, and authorisation to access discovery
information.

Security of discovery metadata is distinct from trust in the discovered entity.
Authentication, authorisation, attestation, and policy checks for later
interaction are outside discovery.

# Privacy Considerations

Discovery queries may reveal information about the intent, capability needs, or
operational state of the discovering entity. Published discovery information may
also reveal information about deployed services, agents, data sources, models,
or organisational relationships.

This suggests that a DAWN discovery mechanism will need to consider what
information is public, what information is restricted, and what information
should not be exposed through discovery.

Privacy-sensitive information can include proprietary capabilities, deployment
location, capacity, runtime state, model or dataset metadata, requester
identity, search history, and query intent.

# Operational Considerations

The use cases include public networks, private networks, enterprise
environments, cloud deployments, edge deployments, and cross-domain interaction.
Different environments may have different expectations for publication,
caching, freshness, authorisation, observability, and operational control.

Dynamic information such as current load, availability, price, or status may
change too frequently to be carried directly in a general discovery mechanism.
A DAWN discovery mechanism may need to return stable information that points to
more dynamic sources.

Across administrative domains, operational considerations include publication
authority, caching, freshness, visibility controls, logging, abuse handling, and
failure behaviour.

# IANA Considerations

This document has no IANA actions.

--- back

# Acknowledgments
{:numbered="false"}

The authors thank Adrian Farrel and Jim Mozley for their review and comments.
