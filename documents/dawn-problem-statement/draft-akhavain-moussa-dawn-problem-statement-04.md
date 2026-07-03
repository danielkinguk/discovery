---
title:
  Problem Statement for the Discovery of Agents, Workloads, and Named
  Entities (DAWN)

abbrev: DAWN problem statement
docname: draft-akhavain-moussa-dawn-problem-statement-04
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

author:
  - ins: A. Akhavain
    name: Arashmid Akhavain
    org: Huawei Technologies Canada
    country: Canada
    email: arashmid.akhavain@huawei.com

  - ins: H. Moussa
    name: Hesham Moussa
    org: Huawei Technologies Canada
    country: Canada
    email: hesham.moussa@huawei.com

  - ins: D. King
    name: Daniel King
    org: Old Dog Consulting
    country: UK
    email: daniel@olddog.co.uk

contributor:
  - ins: K. Yao
    name: Kehan Yao
    org: China Mobile
    country: China
    email: yaokehan@chinamobile.com
  -

normative:

informative:
---

--- abstract

Interacting entities such as agents, tasks, users, workloads, data,
compute, etc., in AI ecosystem/network are proliferating, yet there is
no standardised way to discover what entities exist, what attributes
such as skills, capabilities, physical characteristics, etc., they
posses, what services they offer, or how to reach them across
organisational boundaries.

Discovery today relies on proprietary directories or manual
configuration, creating fragmented ecosystems that prevent cross-domain
collaboration.

This document describes the problem space that motivates Discovery of
Agents, Workloads, and Named Entities (DAWN). It clarifies the scope of
work within entity ecosystems, identifies why current approaches are
insufficient, and outlines the challenges a standardised discovery
mechanism must address. It does not propose a specific solution or
protocol.

--- middle

# Introduction {#sec-intro}

Entities in entity ecosystem collaborate to render services and follow
the lifecycle shown in {{fig-lifecycle}}.

~~~~
+------------------------+     +-------------------------------+
| Entity                 |     |          Entity system        |
| (e.g., AI agent, task) |---->|       registration process    |
+------------------------+     | +---------------------------+ |
                               | |   Identity Provisioning   | |
                               | +---------------------------+ |
                               |               |               |
                               |               v               |
                               | +---------------------------+ |
                               | |      Authentication       | |
                               | +---------------------------+ |
                               |               |               |
                               |               v               |
                               | +---------------------------+ |
                               | |      Authorisation        | |
                               | +---------------------------+ |
                               +-------------------------------+
                                               |
                                               v
                            **************************************
                            | Discovery substrate access point   |
                            **************************************
                            |       Discovery substrate          |
                            **************************************
                                               |
                                               v
                            +------------------------------------+
                            | Communication/Invocation/Operation |
                            +------------------------------------+
                                               |
                                               v
                            +------------------------------------+
                            |             Monitoring             |
                            +------------------------------------+

~~~~
{: #fig-lifecycle title="An example of Entity Lifecycle" artwork-align="center"}

As shown in {{fig-lifecycle}}, an entity will pass through a set of
important functional blocks before it becomes active and start
interacting with other entities in the ecosystem. This document focuses
on the discovery problem space in the above diagram namely: "Discovery
substrate access point" and "Discovery substrate".

Entities increasingly need to discover, connect with, and collaborate
with one another to deliver services. This discovery process is driven
by the need to identify the most suitable set of entities that satisfy
the requirements of a particular service. To achieve this, an entity
must be able to find others based on attributes such as skills,
capabilities, physical characteristics, names, and other relevant
qualities they possess. Obviously, as static configuration is
impractical at scale, an automated discovery of entities, their skills,
and their capabilities becomes essential.

Discovery within an AI ecosystem can be multi-dimensional and complex. A
discovery request may trigger a cascade of subsequent discovery requests
by other AI entities, occurring either sequentially or in parallel and
the process might become unbounded. In addition, the discovery step can
be interactive. For example, an entity might be looking for another
entity that might not be available at the time of request (e.g., the
desired entity might be busy). Furthermore, entities might be looking
for a variety of other entities with different cards/descriptors.
Discovery might also be subjected to either a system wide or local
policy and might span cross organisation. There also challenges w.r.t
the nature of discovery request itself as will be explained later in
this document.

Assuming that trust has already been established between entities and
within the ecosystem in the steps prior to the discovery stage, the
discovering entity must learn what the remote entity does, what
attributes it posses, how to communicate with it, etc.

This document describes the problem space and informs the development of
requirements set out in {{?I-D.king-dawn-requirements}} and future
solution proposals for Discovery of Agents, Workloads, and Named
Entities (DAWN).

# Terminology {#sec-terms}

This document uses the following terms defined in
{{!I-D.farrel-dawn-terminology}}:

- Attributes

- Discoverable Object

- Discovery

- Discovery Mechanism

- Entity

- Minimum Discoverable Information

# Motivation {#sec-motives}

The main motivation behind DAWN is to tackle the discovery problem space
within the entity ecosystem. It is driven by a few factors:

- Discovery use cases in real‑world
  - Many practical scenarios require discovery, not only for
    agent‑to‑agent, but also agent‑to‑tools, agent‑to‑task,
    task-to-agent, and other forms of entity interaction.

- Limitations of traditional discovery methods
  - Existing discovery mechanisms are not designed to natively handle
    scenarios where entities are dynamic, mobile, cross-domain, or when
    they have complex attributes.

- Current approaches are ad-hoc, entity specific, and and do not scale:
  - Even in today's implementations (e.g., MCP‑based systems or
    A2A‑based systems), discovery tends to be contained and handled
    through simple mechanisms such as name lookup, search engines, or
    static agent cards/tool cards. These approaches work only in small,
    closed environments. They do not address challenges such as
    inter‑domain discovery, dynamic endpoint association, chained
    discovery queries, blind or exploratory search sessions, or
    large‑scale environments. In addition, they do not address the need
    of other discoverable entities such as task, workloads, etc.

- Emergence of discoverable entities, discoverable objects, and
  discovery mechanism:
  - Entities may have associated MDIs (e.g., task , capabilities,
    endpoints, policies), and that a discovery
    substrate/mechanism/vehicle is needed. The discovery substrate may
    implement unified mechanism or may support multiple discovery
    strategies depending on the scenario.

## Example of Discovery Lifecycle in AI Ecosystem {#sec-lifecycle}

Consider a task owner (e.g., an entity such as an end user, AI agent,
model, data owner, resource/compute owner) which intends to submit a
task to the ecosystem and, as shown in Figure 1, has already been
processed and accepted by the entity registration block. The following
describes the steps after which the entity becomes available for
discovery.

1. Discovery substrate access point validates the task owner's
   credentials and verifies that its associated discoverable object
   meets compliance requirements. The discoverable object is what the
   discovery substrate makes available/visible to system participants.
   It contains the minimum discoverable information (MDI) needed by
   discovering entities in the system to decide whether selection,
   authorisation, capability exchange, or communication should be
   attempted.

2. Validated task owners may submit their tasks to the system. Submitted
   tasks are discoverable entities themselves. They have their own
   discoverable objects (task card in this case) which the discovery
   substrates makes available/visible to other entities in the ecosystem
   once they pass through the entity registration block.

3. Registered discovering entities (e.g., an AI agent) may issue
   discovery queries to identify and/or locate discoverable objects. For
   example a validate task owner has a task that needs to be fulfilled
   by an AI agent. The task owner submits the discoverable object of its
   task (e.g., task card), the discovery substrate makes the task card
   visible and discoverable, various registered AI agents launch task
   discovery queries to locate suitable tasks to perform, a registered
   AI agent discovers the discoverable task card and determines
   suitability. The register AI agent can also launch other discovery
   queries to find other entities (e.g., other AI agents, compute
   resources, or inference data) that can participate in fulfilling the
   discovered task.

4. The discovery substrate processes discovery queries and returns the
   relevant validated discoverable objects such as tasks, agents,
   resources, etc., to the discovering entity that issued the query. It
   must be noted that the nature and structure of the query, the format
   of the discoverable objects (e.g., standardised object cards), and
   the discovery mechanism employed (e.g., simple name lookup or
   semantic matching) are key factors influencing the accuracy, volume,
   timeliness, etc., of the results. For example, the discovering entity
   may need to provide details about its skills, capabilities, pricing,
   or other relevant attributes so the discovery substrate can match its
   request with an appropriate subset of registered discoverable
   entities in the system.

5. Upon receiving the discovery results (e.g., a list of suitable
   entities), the discovering entity might need additional information
   before initiating its interaction with the discovered entities. For
   example, it might need to know more about the parent entity of the
   discovered entity whose name/ID can be potentially found in the
   discovered entity's discoverable object.

The example above illustrates the broader concept of discovery within an
ecosystem. Other factors such as entity's mobility can further
complicate the problem space. The example underscores the significance
and complexity of the problem space that DAWN aims to address. It
highlights why a structured problem definition, clear requirements, and
well‑designed solutions are essential for enabling robust, scalable, and
interoperable discovery across diverse entities and use cases.

# Applicability {#sec-applicability}

The challenges outlined in the Motivation section underscore the need
for mechanisms that allow discovering and discoverable entities to
dynamically locate and interact within a decentralised ecosystem. DAWN
is applicable in scenarios where discovery serves as a key enabler for
autonomous operation, collaboration, and adaptive decision-making. In
such systems, various discovery modes should be supported. For example,
there needs to be support for entities that lunch discovery queries to
find other entities, while also supporting scenarios where task owners
including agents, users, or services may advertise needs (e.g., tasks to
be completed) that suitable entities can discover and execute.

Some discovery examples include Data sources can that make their
datasets discoverable to support reasoning or training features needed
by AI agents and models, compute resources may advertise their
capabilities, serving as rendezvous points for entities, models, and
datasets to facilitate training workflows, or models may advertise their
functionality to allow users or entities to discover them for inference
tasks.

The following subsections provides more details, illustrating the
contexts in which DAWN provides value and a consistent foundation for
the functional requirements and design considerations.

## Entities discovering Entities

Entities frequently need to locate other entities to coordinate actions,
share information, or engage in collaborative workflows. In some
situations, an entity may already be aware of a counterpart possessing
the required skills or capabilities. In other cases, entities must
actively query the system to discover suitable peers by specifying the
skills or attributes they are looking for. DAWN provides a framework to
support both modes of discovery, enabling dynamic, capability-driven
interactions in decentralised and heterogeneous environments.

DAWN enables entities to advertise their presence, capabilities, and
status, facilitating peer-to-peer interactions in ecosystems that are
dynamic and hosts various types of entities. This is particularly
relevant in large-scale deployments, cross-domain environments, or
systems where entities may join or leave unpredictably.

## Entities discovering needs

In addition to discovering other entities, entities may also desire to
locate needs advertised by other entities (e.g. Tasks) that require
attention or contribution within a system. Needs can be advertised by
users, other entities, or services, along with information such as
required skills, priority, or dependencies. Since entities are aware of
their own capabilities, they can match their skill sets against
advertised needs and proactively apply for or claim the opportunity to
fulfull the need for which they are suitable. DAWN provides mechanisms
to make needs (e.g., Tasks) discoverable, enabling entities to query,
filter, and select tasks efficiently, supporting autonomous
orchestration, dynamic workflow formation, and load distribution across
heterogeneous environments.

## Entities/models discovering data

Entities and models often require access to data distributed across
multiple systems or administrative domains to perform training,
inference, or reasoning tasks. This includes datasets, knowledge bases,
or document repositories that may be advertised as discoverable entities
with information such as format, availability, and access requirements.
In Retrieval-Augmented Generation (RAG) scenarios, entities or models
need to dynamically locate relevant external knowledge sources or
documents to supplement generative reasoning, enabling more accurate and
context-aware responses. Additionally, data in these environments may be
dynamic, changing over time as new information is added or existing data
is updated. DAWN provides mechanisms for discovering, tracking, and
querying such evolving data sources, allowing entities and models to
identify relevant information in real time while respecting access
controls and provenance information.

## Entities/models and data discovering compute

Entities and models often require access to compute resources to perform
tasks such as training, fine-tuning, or indexing. These resources may be
distributed across multiple systems or administrative domains, and their
availability, capacity, or configuration can change over time. In this
context, compute resources can serve as rendezvous points, allowing
entities, models, and datasets to converge and interact efficiently.
DAWN provides mechanisms for entities, models, and data sources to
discover compute resources that meet their requirements, including
hardware capabilities, scheduling constraints, and current availability.
By enabling dynamic identification of suitable compute nodes, DAWN
supports elastic scaling of training workloads, efficient utilisation of
heterogeneous infrastructure, and adaptive collaboration in
decentralised and changing environments.

## Discovering models for inference

Users, agents, and services (i.e., entities) may need to leverage
pre-trained models for inference in tasks such as prediction,
recommendation, or decision-making. Models may be distributed across
various systems or administrative domains, and their availability,
capabilities, or performance characteristics can evolve over time. DAWN
supports mechanisms to discover models that are most suitable for
different contexts. This enables users, agents, services, etc. to
dynamically adapt to newly available models, take advantage of
improvements, and ensure interoperability in heterogeneous and evolving
environments.

## Taxonomy of Entities {#sec-taxonomy}

Classifying entities along multiple dimensions helps derive common as
well as specific requirements in discovery processes and protocols for
different types of entities.

The following aspects are listed. This is not an exclusive list and it
is expected that the list will evolve iteratively as new use cases are
developed. Primary dimensions include:

- Identity Binding: Describes the relationship between an entity's
  identifier and its runtime deployment artifact (e.g., a single
  instance, cluster, physical device, IP/port, etc.). This determines
  the persistence of the identifier as well as the lifecycle and
  reachability characteristics of the resolved target object. Discovery
  mechanisms need to consider these characteristics when designing
  caching policies, refresh frequencies, and re-discovery conditions.

  For example: An AI agent may be bound to a dynamic service instance in
  a cloud computing environment, or it may be bound to a specific
  physical mobile device. The former may have an ephemeral identifier
  that changes across sessions, while the latter has a persistent
  identifier.

- Control Ownership: The administrative entity that has authority over
  the entity's lifecycle, configuration, and policy. This determines who
  publishes discovery information and who can update or withdraw it.

  For example: A computing workload may be owned by the user who submits
  it (control ownership lies with the user), while a network function
  deployed by a service provider is owned by that provider's
  organization.

- Responsible Party: The party that is operationally accountable for the
  entity's behaviour, including security, correctness, and policy
  compliance. This may differ from the control owner. This dimension
  relates to trust and attestation requirements in discovery.

  For example: In a Retrieval-Augmented Generation (RAG) scenario, the
  data source that is discovered and retrieved is the responsibility of
  its data owner. Meanwhile, the AI agent that consumes that data and
  generates new results is the responsibility of its agent provider.

- Dynamic Characteristic: The rate and predictability of change in the
  entity's discoverable properties (e.g., location, availability, load).
  This influences how discovery information should be published and
  cached.

  For example: The current load of a computing workload changes rapidly
  (high dynamism). In contrast, a deployed network function change
  rarely (low dynamism), allowing long-lived caching.

- Discovery Payload Richness: The level of detail and structure of
  discovery information that an entity can publish or that a query can
  expect to retrieve. This determines whether discovery information is
  embedded directly in the response or provided via references, and it
  also affects query language capabilities and caching granularity.

  For example: A simple network function may only advertise its IP
  address and port (minimal). An AI agent may publish a full capability
  card listing its skills, input/output schemas, and authentication
  method (rich).

- Cross-domain Visibility: The level of access control, entity discovery
  permissions, amount of information exposed, and selective publication
  of information are aspects that need to be considered when operating
  in multi-administrative domain environements.

For example: An AI agent's capabilities may be discoverable across
domains to enable collaboration, but the backend computing services that
execute the agent's tasks are only discoverable within the same
administrative domain for security or policy reasons.

The following presents a table of entity types. This is not an exclusive
list and it is expected that more entity types will continue to be added
as new use cases are developed. The table shows:

~~~~
+-----------+----------+------------+-------------+--------------+
|  Entity   | Identity |  Control   | Responsible |   Dynamic    |
|   Type    | Binding  |  Ownership |    Party    |Characteristic|
+-----------+----------+------------+-------------+--------------+
|    AI     |End device|Organization| Developer&  |    High      |
|   Agent   |/Instance |    /User   |Deployer&User|              |
+-----------+----------+------------+-------------+--------------+
|  Software | Instance |  Provider  |  Developer  |    Medium    |
|  Service  | /Cluster |Organization| & Deployer  |              |
+-----------+----------+------------+-------------+--------------+
|  Compute  | Variable |Submitter & |  Submitter  |    High      |
|  Workload |    ID    |Orchestrator| & Deployer  |              |
+-----------+----------+------------+-------------+--------------+
|  Network  | Node     | Provider   |   Operator  |    Low       |
|  Function | /Instance|Organization|             |              |
+-----------+----------+------------+-------------+--------------+
|Application| IP/Port  |   Owning   |  Developer  |    Medium    |
|  Endpoint | /Instance|Organization| & Deployer  |              |
+-----------+----------+------------+-------------+--------------+
~~~~
{: #taxonomy title="Taxonomy of Entities" artwork-align="center"}


# Functional Requirements {#sec-func-req}

## Discovering Entities and Query Granularity {#sec-disco-entity}

Discovery in ecosystem should support different levels of granularity.
Queries may range from broad capability-based searches (such as
identifying all models with mathematical abilities) to more specific
lookups (such as retrieve details about wolfram alpha math-expert
agent). The discovery system should also enable entities to be found
through the attributes reflected in their discoverable objects that
capture aspects like their skill sets, functionality, name/ID, ratings,
regional associations, and more.

## Discovering Response and Minimum Discoverable Information {#sec-disco-rsp}

Information an entity discovers about another entity must be meaningful
and useful for delivering the required service. Accordingly, a response
to a discovery query should include attributes that describe the
discovered entity: such as what it can do, the skills it possesses, the
protocols it supports, the security guarantees it claims to offer, the
policies it can potentially enforce, its pricing for services, its
current operational status (e.g., available, busy, or offline),
communication means, etc.

Such information can be either embedded within the entity's discoverable
object or retrieved through a subsequent interaction outside the
discovery substrate (for example, after discovery, an interview‑style
exchange may be conducted using the communication method indicated by
the entity - outside the scope of DAWN).

In either case, there is a need for a standardized structure for
discoverable objects that provides the minimum set of information (i.e.,
MDI) needed for the discovery substrate to return results that
meaningfully support service delivery within the AI ecosystem.

## Cross-Domain Collaboration {#sec-cross-domain}

Entities operating across organisational boundaries need to discover
counterparts without depending on a shared infrastructure. For example,
a customer-service agent in one organisation may need to find a
logistics-tracking agent in another. Models in one administrative domain
may need to find compute resources in another administrative domain for
training. Similarly, a model or agent in one domain might need to use
data in another domain for retrieval-augmented generation (RAG) based
inference. Current platform-specific mechanisms do not interoperate, so
entities remain invisible outside their own ecosystem.

Administrative domains are typically unwilling to disclose their
internal structures or detailed operational information to one another.
In traditional networking, for instance, they use abstraction and
aggregation techniques to share only high‑level insights about their
operations. A standards‑based mechanism to support controlled
information sharing while ensuring administrative domain
interoperability without exposing sensitive internal details is
potentially desirable.

## Discovery and Dynamic Attributes in Discoverable Objects {#sec-disco-dyanmic}

Entities whose discoverable objects contain dynamic attributes introduce
distinct challenges for discovery. Dynamic attributes such as location
information, dataset samples, compute capacity, etc., can change at
different rates. These dynamics introduce variability that static
discovery systems are not designed to handle. Such dynamic attributes
complicate the assumptions in traditional discovery approaches and
demand careful consideration when defining the problem space.

## Broker and Aggregator Discovery {#sec-broker}

In large‑scale networks, entities may need to discover intermediary
broker nodes. These brokers often operate across multiple administrative
domains with different jurisdictions. They also provide dynamic
operational information, such as availability, capabilities, or decision
guidance. In these scenarios, the intermediary brokers might need to
discover other brokers. This makes the broker nodes another type of
entity with its own discoverable object in an ecosystem. Discovery
substrate needs to provide support for this capability via
standards‑compliant procedures.

## Human-Initiated Discovery {#sec-human}

Operators need to discover and inspect entities for operational
purposes: auditing deployed agents, verifying capability claims, or
troubleshooting failures. Discovery must be usable by humans through
standard tooling, not only by automated systems.

## Discovery and OAM {#sec-oam}

Discovery systems require operational visibility, management, and
diagnostic capabilities to ensure reliable operation across potentially
distributed and cross-domain environments. Operators should be able to
determine the behaviour of the discovery system and understand the
reasons for discovery outcomes, failures, and policy decisions. The
following outlines some of the operational aspects that need to be
considered.

- Discovery Infrastructure Observability and Diagnostics: Operational
  managers require visibility into the availability, health,
  performance, and reachability of discovery system components, as well
  as the ability to determine whether discovery transactions can be
  successfully completed. Operational managers should also be able to
  observe discovery activity and determine the reasons for discovery
  outcomes, failures, performance degradation, and other system
  behaviours.

- Policy and Security Visibility: Discovery behaviour may be influenced
  by policies, trust relationships, authorisation decisions, and
  security mechanisms. Operational managers need visibility into how
  these factors affect discovery outcomes and the ability to identify
  abnormal or unauthorised activity.

- Discovery Information Tracking Management: Operational managers need
  to be able to monitor the status of discoverable objects and
  information in the system including its creation, modification,
  propagation, expiration, and removal. Operators might also need to
  access different statistics about the discoverable objects and
  optionally make reports available to authorised organisations (e.g
  owners, authorities, etc.).

- Discovery Chains and cross-Domain Operations: Discovery may involve a
  sequence of dependent discovery operations, potentially spanning
  multiple systems and administrative domains. Operational managers
  require visibility into discovery chains, dependencies, and
  interactions in order to understand discovery outcomes and to monitor
  and troubleshoot failures or performance issues that may occur along
  the discovery path.

Tooling to enable this function should be integral to the design of any
solution and specific requirements for operational considerations can be
found in {{?I-D.king-dawn-requirements}}.

# Current Approaches and Their Limitations {#sec-limits}

There are a few available approaches to discovery some of which are
standardized and are in operations (e.g., DNS, DNS-SD, SSDP, and
Webfinger), others are proposed in different venues and are still under
development (e.g., DNS-AID and CATS), and others are designed to address
certain needs and are packed by open source developers (e.g., A2A, MCP,
and AGNTCY). A careful analysis and evaluation of these approaches to
assess their suitability to meet the DAWN problem space and
requirements, and to identify key gaps that shall be considered by
future solutions is needed.

# Core Challenges {#sec-challenges}

## Discovering Skills and Capabilities at Scale {#sec-skills}

The central challenge is enabling entities to discover other entities
based on some of their characteristics such as:

- Functions
- Skills
- Capabilities
- Services
- Requirements
- etc.

A discovery mechanism that supports structured, scalable discovery of an
entity's capabilities across organisational boundaries is therefore
required.

## Fragmented Discovery Ecosystem {#sec-fragments}

Each platform develops its own discovery approach. This fragmentation
prevents entities from being discoverable across boundaries and limits
the value of interoperable protocols such as A2A and MCP.

## Trust in Discovery Information {#sec-trust}

When discovery crosses organisational boundaries, the discovering entity
must verify that the information is authentic. Without authenticated
discovery, entities are vulnerable to poisoning attacks directing them
to malicious endpoints.

## Scalability and Decentralisation {#sec-scale}

Discovery must operate at Internet scale without a single centralised
registry. Each organisation must be able to have governance over its
published discoverable objects associated with its entities', enabling
features such as independently adding new entities, updating information
of currently published entities, removing discoverable objects of its
pubished entities, monitoring status of published entities, retriving
utility statistics...etc.

## Static Versus Dynamic Properties {#sec-static}

Entity properties range from static (type, supported protocols, skills)
to dynamic (availability, load, capacity). A discovery mechanism must
handle both without causing stale results or excessive query load and
shall be able to keep published information fresh and always up-to-date.

## Extensibility {#sec-extensible}

New entity types, entity taxonomies, and entity description formats will
emerge. Discovery must accommodate them without changes to the core
mechanism.

# Security Considerations {#sec-security}

This document describes a problem space, not a protocol.

Discovery information is a high-value target. Poisoned responses could
direct entities to malicious endpoints. Any mechanism must provide
integrity and authenticity guarantees. Specific security-related
requirements for any solution are captured in
{{?I-D.king-dawn-requirements}}.

Cross-domain discovery raises two distinct trust questions: whether the
discovery source is authoritative, and whether the registered entity is
what it claims to be.

Discovery may expose sensitive information about an organisation's
entities and capabilities. Selective visibility mechanisms are needed.

# Privacy Considerations {#sec-privacy}

Privacy in discovering  Agents, Workloads and Named entities is 
inherently a two-sided problem. On the one hand, the party seeking an
entity should be able to discover providers without unnecessarily 
revealing its identity, interests, or intent. On the other hand, 
the entity offering a service, a workload, etc., should be 
able to control what information about its capabilities, 
existence, and availability is exposed to potential discoverers.

In line with guidelines provided in {{?RFC6973}}, discovery 
architecture and related protocols should treat privacy as 
a mutual property rather than a client-only concern. Both 
discoverers and discovered entities are potential sources 
and targets of information leakage, requiring mechanisms 
that minimize data exposure, limit observability, and 
support policy-based selective disclosure on both sides.

Further discussion and analysis about privacy considerations 
in the context of DAWN can be found in 
{{?I-D.iannone-dawn-privacy-considerations}}.

# Operational Consideration {#sec-opcon}

## Observability and Troubleshooting {#sec-Observability}

Providing sufficient visibility to understand discovery behaviour and
diagnose failures are essential features for operations particularly in
large-scale and cross-domain deployments. Operational personnel may need
to determine:

- Whether a discoverable object is registered and reachable.
- Why a discovery query succeeded or failed.
- Which attributes influenced discovery results.
- Whether stale, inconsistent, or conflicting information exists.
- What causes delay in disocvery responses.

Discovery information can change over time as entities are created,
modified, relocated, become unavailable, or are removed. This may cause
many discoverable properties to be dynamic, such as availability, load,
capacity, trust level, or operational status. Operators may also require
tracking information such as:

- Registration and deregistration events.
- Attribute updates.
- Expiration and refresh status.
- Propagation delays.
- Historical state changes for audit and troubleshooting purposes.

Operators should be ableto monitor the freshness and propagation of such
information while balancing update frequency against operational
overhead.

## Cross-Domain Operations {#sec-CrossDomOp}

Discovery is expected to occur across organisational boundaries.
Operators may need visibility into:

- Discovery paths that span multiple domains.
- Delegation relationships.
- Failure points within a discovery chain.

Operational procedures should support troubleshooting when discovery
outcomes depend on information obtained from multiple administrative
domains.

## Scalability and Performance Management {#sec-ScaleMan}

Discovery may operate at Internet scale and support large numbers of
entities and queries. Some operational considerations include:

- Query volume and rate management.
- Caching effectiveness.
- Discovery latency and propagation of information.
- Load distribution.
- Resource consumption of discovery services.
- Employing hierarchy.

Operators should be able to monitor and manage the performance
characteristics of discovery systems under varying workloads.

## Policy and Security Visibility {#sec-PolSec}

Discovery results may be influenced by authorisation, trust policies,
administrative restrictions, and security controls. Operators may
require visibility into:

- Policy decisions affecting discovery outcomes.
- Authentication and authorisation failures.
- Detection of suspicious discovery activity, including abuse of
  discovery mechanisms or attempts to obtain or manipulate information
  beyond intended policy scope.

Such visibility is important for maintaining confidence in discovery
information and supporting incident response activities.

## Audit and Compliance {#sec-Audit}

Organisations may need records of discovery-related activities for
governance, security investigations, or regulatory compliance. Examples
include:

- Discovery requests.
- Attribute modifications.
- Administrative actions.
- Cross-domain information exchanges.

The extent of audit requirements will vary by deployment environment.

# IANA Considerations {#sec-IANA}

This document makes no requests of IANA.

# Potential Topics for the Use Case Document {#sec-usecases}

- pre-configured static discovery, where entities have set relationships
  and only need to discover each other once in the beginning.
- Capability-Oriented Discovery, where an entity needs to discover
  another entity that can provide a function or capability.
- Chained Discovery, where a task requires the discovery of multiple
  entites either in pararell or in series.
- Resource-Oriented Discovery, where discovery identifies resources
  needed such as agents, workloads, compute, functions, applications, or
  users, to fulfill a given task.
- Closed-system Discovery, where the discover mechanims runs within a
  bounded controlled network of entities
- Open-system Discovery, where entities to be discovered may belong to
  different administrative domains.
- Interactive-discovery, where the discovery mechanims require
  additional rounds of interactions with the discovery query generating
  entitiy before the discovery request can be fulfilled.
- Reversed discovery, where a discovering entity published its needs in
  the form of discoverable objects that can be discovered by entities
  looking for offering their services.
- Operational Discovery, where discovery supports operation, audit,
  troubleshooting, compliance, or automation.

# Acknowledgements {#sec-ack}
{:numbered="false"}

Thanks to Adrian Farrel and Linda Dunbar for review comments.
