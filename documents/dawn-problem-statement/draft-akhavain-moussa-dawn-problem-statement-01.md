---
title: Problem Statement for the Discovery of Agents, Workloads, and Named Entities (DAWN)

abbrev: DAWN problem statement
docname: draft-akhavain-moussa-dawn-problem-statement-00
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
  -
    ins: A. Akhavain
    name: Arashmid Akhavain
    org: Huawei Technologies Canada
    country: Canada
    email: arashmid.akhavain@huawei.com

  -
    ins: H. Moussa
    name: Hesham Moussa
    org: Huawei Technologies Canada
    country: Canada
    email: hesham.moussa@huawei.com

  -
    ins: D. King
    name: Daniel King
    org: Old Dog Consulting
    country: UK
    email: daniel@olddog.co.uk

normative:

informative:
---

--- abstract

Interacting entities such as agents, tasks, users, workloads, data, compute, etc., in AI ecosystem/network are proliferating, yet there is no standardised way to discover what entities exist, what attributes such as skills, capabilities, physical characteristics, etc., they posses, what services they offer, or how to reach them across organisational boundaries.
   
Discovery today relies on proprietary directories or manual configuration, creating fragmented ecosystems that prevent cross-domain collaboration. 

This document describes the problem space that motivates Discovery of Agents, Workloads, and Named Entities (DAWN).  It clarifies the scope of work within entity ecosystems, identifies why current approaches are insufficient, and outlines the challenges a standardised discovery mechanism must address. It does not propose a specific solution or protocol.

--- middle

# Introduction {#sec-intro}

Entities in entity ecosystem collaborate to render services and follow the lifecycle shown in {{fig-lifecycle}}.

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

As shown in {{fig-lifecycle}}, an entity will pass through a set of important functional blocks before it becomes active and start interacting with other entities in the ecosystem. This document focuses on the discovery problem space in the above diagram namely:
"Discovery substrate access point" and "Discovery substrate".

Entities increasingly need to discover, connect with, and collaborate with one another to deliver services. This discovery process is driven by the need to identify the most suitable set of entities that satisfy the requirements of a particular service. To achieve this, an entity must be able to find others based on attributes such as skills, capabilities, physical characteristics, names, and other relevant qualities they possess. Obviously, as static configuration is impractical at scale, an automated discovery of entities, their skills, and their capabilities becomes essential.

Discovery within an AI ecosystem can be multi-dimensional and complex. A discovery request may trigger a cascade of subsequent discovery requests by other AI entities, occurring either sequentially or in parallel and the process might become unbounded. In addition, the discovery step can be interactive. For example, an entity might be looking for another entity that might not be available at the time of request (e.g., the desired entity might be busy). Furthermore, entities might be looking for a variety of other entities with different cards/descriptors. Discovery might also be subjected to either a system wide or local policy and might span cross organisation. There also challenges w.r.t the nature of discovery request itself as will be explained later in this document.

Assuming that trust has already been established between entities and within the ecosystem in the steps prior to the discovery stage, the discovering entity must learn what the remote entity does, what attributes it posses, how to communicate with it, etc.

This document describes the problem space and informs the development of requirements set out in {{?I-D.king-dawn-requirements}} and future solution proposals for Discovery of Agents, Workloads, and Named Entities (DAWN).

# Terminology {sec-terms}

This document uses the following terms defined in {{!I-D.farrel-dawn-terminology}}:

- Attributes

- Discoverable Object

- Discovery

- Discovery Mechanism

- Entity

- Minimum Discoverable Information
  
# Motivation {#sec-motives}

The main motivation behind DAWN is to tackle the discovery problem space within the entity ecosystem. It is driven by a few factors:

- Discovery use cases in real‑world

   - Many practical scenarios require discovery, not only for agent‑to‑agent, but also agent‑to‑tools, agent‑to‑task, task-to-agent, and other forms of entity interaction.

- Limitations of traditional discovery methods  

   - Existing discovery mechanisms are not designed to natively handle scenarios where entities are dynamic, mobile, cross-domain, or when they have complex attributes.

- Current approaches are ad-hoc, entity specific, and and do not scale:  

   - Even in today's implementations (e.g., MCP‑based systems or A2A‑based systems), discovery tends to be contained and handled through simple mechanisms such as name lookup, search engines, or static agent cards/tool cards. These approaches work only in small, closed environments. They do not address challenges such as inter‑domain discovery, dynamic endpoint association, chained discovery queries, blind or exploratory search sessions, or large‑scale environments. In addition, they do not address the need of other discoverable entities such as task, workloads, etc.

- Emergence of discoverable entities, discoverable objects, and discovery mechanism:  

   - Entities may have associated MDIs (e.g., task , capabilities, endpoints, policies), and that a discovery substrate/mechanism/vehicle is needed. The discovery substrate may implement unified mechanism or may support multiple discovery strategies depending on the scenario.

## Example of Discovery Lifecycle in AI Ecosystem {#sec-lifecycle}

Consider a task owner (e.g., an entity such as an end user, AI agent, model, data owner, resource/compute owner) which intends to submit a task to the ecosystem and, as shown in Figure 1, has already been processed and accepted by the entity registration block. The following describes the steps after which the entity becomes available for discovery.

1. Discovery substrate access point validates the task owner's credentials and verifies that its associated discoverable object meets compliance requirements. The discoverable object is what the discovery substrate makes available/visible to system participants. It contains entity's different attributes and information that others need to initiate an interaction session with it once they discover the entity.

2. Task owner submits its tasks to the system. Submitted tasks are entities themselves. They have their own discoverable object (task card in this case) which the discovery substrates makes available/visible to other entities in the ecosystem once submitted tasks pass through the entity registration block.

3. A registered entity (e.g., an AI agent) then issues a discovery query to identify and/or locate suitable tasks it can perform, or to find other agents, resources, etc., it must interact with to complete a given task.

4. The discovery substrate processes the above query and returns the relevant discoverable objects such as tasks, agents, resources, etc., to the entity that issued the query. It must be noted that the nature and structure of the query, the format of the discoverable objects (e.g., standardised object cards), and the discovery mechanism employed (e.g., simple name lookup or semantic matching) are key factors influencing the accuracy, volume, timeliness, etc., of the results.

   For example, the querying entity may need to provide details about its skills, capabilities, pricing, or other relevant attributes so the discovery substrate can match its request with an appropriate subset of registered entities in the system.

5. Upon receiving the discovery results (e.g., a list of suitable entities), the querying entity (e.g., an AI agent) might need additional information before initiating its interaction with the discovered entities. For example, it might need to know more about the parent entity of the discovered entity whose name/ID can be potentially found in the discovered entity's discoverable object.

The example above illustrates the broader concept of discovery within an ecosystem. Other factors such as entity's mobility can further complicate the problem space. The example, underscore the significance and complexity of the problem space that DAWN aims to address. It highlights why a structured problem definition, clear requirements, and well‑designed solutions are essential for enabling robust, scalable, and interoperable discovery across diverse entities and use cases. 

# Functional Requirements {sec-func-req}

## Discovering Entities and Query Granularity {#sec-disco-entity}

Discovery in ecosystem should support different levels of granularity. Queries may range from broad capability-based searches (such as identifying all models with mathematical abilities) to more specific lookups. The discovery system should also enable entities to be found through the attributes reflected in their discoverable objects that capture aspects like their skill sets, functionality, name/ID, ratings, regional associations, and more.

## Discovering Response and Minimum Discoverable Information {#sec-disco-rsp}

Information an entity discovers about another entity must be meaningful and useful for delivering the required service. Accordingly, a response to a discovery query should include attributes that describe the discovered entity: such as what it can do, the skills it possesses, the protocols it supports, the security guarantees it claims to offer, the policies it can potentially enforce, its pricing for services, its current operational status (e.g., available, busy, or offline), communication means, etc.

Such information can be either embedded within the entity's discoverable object or retrieved through a subsequent interaction outside the discovery substrate (for example, after discovery, an interview‑style exchange may be conducted using the communication method indicated by the entity). 

In either case, there is a need for a standardized structure for discoverable objects that provides the minimum set of information needed for the discovery substrate to return results that meaningfully support service delivery within the AI ecosystem.
   
## Cross-Domain Collaboration {#sec-cross-domain}

Entities operating across organisational boundaries need to discover counterparts without depending on a shared infrastructure. For example, a customer-service agent in one organisation may need to find a logistics-tracking agent in another. Models in one administrative domain may need to find compute resources in another administrative domain for training. Similarly, a model or agent in one domain might need to use data in another domain for retrieval-augmented generation (RAG) based inference. Current platform-specific mechanisms do not interoperate, so entities remain invisible outside their own ecosystem.

Administrative domains are typically unwilling to disclose their internal structures or detailed operational information to one another. In traditional networking, for instance, they use abstraction and aggregation techniques to share only high‑level insights about their operations. A standards‑based mechanism to support controlled information sharing while ensuring administrative domain interoperability without exposing sensitive internal details is potentially desirable.

## Discovery and Dynamic Attributes in Discoverable Objects {#sec-disco-dyanmic}

Entities whose discoverable objects contain dynamic attributes introduce distinct challenges for discovery.  Dynamic attributes such as location information, dataset samples, compute capacity, etc., can change at different rates. These dynamics introduce variability that static discovery systems are not designed to handle. Such dynamic attributes complicate the assumptions in traditional discovery approaches and demand careful consideration when defining the problem space.

## Broker and Aggregator Discovery {#sec-broker}

In large‑scale networks, entities may need to discover intermediary broker nodes that operate across multiple administrative domains and provide dynamic operational information such as availability, capabilities, or decision guidance via the use of mechanisms that support interoperable and standards‑compliant discovery procedures.

In large‑scale networks, entities may need to discover intermediary broker nodes. These brokers often operate across multiple administrative domains with different jurisdictions. They also provide dynamic operational information, such as availability, capabilities, or decision guidance. In these scenarios, the intermediary brokers might need to discover other brokers. This makes the broker nodes another type of entity with its own discoverable object in an ecosystem. Discovery substrate needs to provide support for this capability via standards‑compliant procedures.

## Human-Initiated Discovery {#sec-human}

Operators need to discover and inspect entities for operational purposes: auditing deployed agents, verifying capability claims, or troubleshooting failures.  Discovery must be usable by humans through standard tooling, not only by automated systems.

## Discovery and OAM {#sec-oam}

TBD

# Current Approaches and Their Limitations {#sec-limits}

## Proprietary Directories {#sec-proprietary}

Cloud providers, AI platforms, and other entity systems maintain their own registries, tightly coupled to their ecosystem.  Entities registered in one platform are invisible to another, creating walled gardens.

## Static Configuration {#sec-config}

Manually configured endpoint lists cannot scale, cannot adapt to dynamic environments, and cannot convey the capability and trust metadata needed for cross-domain discovery.

## DNS-SD and SRV Records {#sec-DNS}

TBD

## Well-Known URIs {#sec-URI}

TBD

## Ad Hoc Agent Discovery Proposals {#sec-adhoc}

TBD

# Core Challenges {#sec-challenges}

## Discovering Skills and Capabilities at Scale {#sec-skills}

The central challenge is enabling entities to discover other entities based on what they can do, such as:

- Agents
- Skills
- Capabilities
- TBA

A discovery mechanism that supports structured, scalable discovery of an entity's capabilities across organisational boundaries is therefore required.

## Fragmented Discovery Ecosystem {#sec-fragments}

Each platform develops its own discovery approach.  This fragmentation prevents entities from being discoverable across boundaries and limits the value of interoperable protocols such as A2A and MCP.

## Trust in Discovery Information {#sec-trust}

When discovery crosses organisational boundaries, the discovering entity must verify that the information is authentic.  Without authenticated discovery, entities are vulnerable to poisoning attacks directing them to malicious endpoints.  DNSSEC provides a foundation, but discovery mechanisms must be designed to use it.

## Scalability and Decentralisation {#sec-scale}

Discovery must operate at Internet scale without a single centralised registry.  Each organisation must be able to publish its entities' capabilities independently, mirroring the DNS delegation model.

## Static Versus Dynamic Properties {#sec-static}

Entity properties range from static (type, supported protocols, skills) to dynamic (availability, load, capacity).  A discovery mechanism must handle both without causing stale results or excessive query load.

## Extensibility {#sec-extensible}

New agent types, skill taxonomies, and capability formats will emerge.  Discovery must accommodate them without changes to the core mechanism.

# Relationship to Existing Work {#sec-existing}

TBD

# Security Considerations {#sec-security}

This document describes a problem space, not a protocol.

Discovery information is a high-value target.  Poisoned responses could direct entities to malicious endpoints. Any mechanism must provide integrity and authenticity guarantees.

Cross-domain discovery raises two distinct trust questions: whether the discovery source is authoritative, and whether the registered entity is what it claims to be.

Discovery may expose sensitive information about an organisation's entities and capabilities.  Selective visibility mechanisms are needed.

# Privacy Considerations {#sec-privacy}

Querying for entities may reveal the discovering entity's intentions or interests.  Discovery should minimise information leakage through the query process.

Published entity properties, such as skills, capabilities, and organisational affiliations, may be sensitive. Entities and their operators should control the granularity and audience of published information.

# Operational Consideration {#sec-opcon}

TBD

# IANA Considerations {#sec-IANA}

This document makes no requests of IANA.

# Potential Topics for the Use Case Document {#sec-usecases}

TBD

#  Acknowledgements {#sec-ack}
{:numbered="false"}

Thanks to Adrian Farrel for review comments.
