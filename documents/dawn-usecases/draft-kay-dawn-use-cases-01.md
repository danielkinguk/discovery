---
title: "Use Cases and Applicability for Discovery of Agents With Names"
abbrev: "DAWN Use Cases"
category: info
docname: draft-kay-dawn-use-cases-latest
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
    org: Lancaster University
    email: "d.king@lancaster.ac.uk"
  -
    name: Kehan Yao
    org: China Mobile
    email: "yaokehan@chinamobile.com"
  -
    name: Ken Adler
    org: Indeed
    email: "kadler@indeed.com"
  -
    name: Rajiv Ramdhany
    org: BBC
    email: "rajiv.ramdhany@bbc.co.uk"
normative:
  I-D.farrel-dawn-terminology:
informative:
  I-D.akhavain-moussa-dawn-problem-statement:
  I-D.king-dawn-requirements:
  I-D.mozley-aidiscovery:
  I-D.agentic-ai-usecases-requirements:
  I-D.scrm-aiproto-usecases:

--- abstract

This document describes use cases and applicability for Discovery of Agents
With Names (DAWN). It illustrates how clients discover AI resources and obtain
the minimum information needed for subsequent interaction within a local
network, within an organisation, or between cooperating organisations with
trust relationships.

This document does not define a discovery protocol, a registration procedure, a
selection algorithm, or an agent-to-agent communication protocol.

--- middle

# Introduction

Artificial Intelligence (AI) systems may depend on resources whose capabilities,
locations, or communication methods are not configured in advance. Discovery
allows a client to locate a resource and obtain the minimum information needed
to attempt a subsequent interaction.

Discovery of Agents With Names (DAWN) initially focuses on AI agents and their
capabilities, including discovery of other resources used in AI systems. This
document uses "entity" for a discoverable component in that context. Such
entities may include agents, tools, services, tasks, data sources, models,
inference services, workloads, brokers, and application endpoints. Skills may be
discoverable attributes of those entities. Reuse in other discovery contexts is
desirable, but does not extend the initial scope to general resource discovery.

The DAWN problem statement {{I-D.akhavain-moussa-dawn-problem-statement}}
and the DAWN requirements document {{I-D.king-dawn-requirements}} provide
background for this work. These use cases inform the Discovery Architecture,
which will define the requirements and minimum discovery information.

This document defines the following categories of entity discovery:

1. Capability-Oriented Discovery, where an entity needs to discover another
   entity that can provide a function or capability.
2. Resource-Oriented Discovery, where discovery identifies resources
   used in AI systems.
3. Administrative Scope Extensions, where discovery crosses organisational,
   delegation, or tenancy boundaries within the applicable trust relationships.
4. Operational Discovery, where discovery supports operation, audit,
   troubleshooting, compliance, or automation.

The first two categories are base cases. The others describe common extensions
or deployments of those base cases.

Other Internet-Drafts describe agentic AI discovery use cases and communication
protocol requirements, including {{I-D.mozley-aidiscovery}},
{{I-D.agentic-ai-usecases-requirements}}, and
{{I-D.scrm-aiproto-usecases}}.

# Limitations of this Document

This document describes discovery within a local network, within an
organisation, or between cooperating organisations with trust relationships
over the public Internet. It does not describe the full lifecycle of an entity
or establish those trust relationships.

The following are in scope:

* discovery of a specific named AI resource;
* discovery of candidate AI resources by capability or other discovery
  properties within the applicable deployment;
* discovery of tasks as resources in an AI system;
* discovery initiated by an agent, workload, service, application, or human
  operator;
* discovery of supporting resources used by AI agents and applications;
* exchange of the minimum discovery information, directly or by indirection,
  before selection, invocation, or communication can take place.

The following are out of scope:

* registration of entities for discovery;
* authentication or attestation of registrations;
* design, definition, or governance of naming systems;
* identity management of AI agents, tools, and skills;
* trust management and trust evaluation beyond protecting content exchanged
  between discovery participants;
* selection among candidate entities returned by discovery;
* exchange of capability information beyond the minimum discovery information
  defined by the Architecture work;
* capability negotiation after discovery;
* all application communication beyond the discovery process;
* task orchestration;
* standalone certificate or key lookup services; and
* AI resource indexing across the wider Internet, general search, ranking,
  or marketplace discovery.

Clients may query an organisation's catalogue or a cooperating discovery
service within these boundaries. They may follow references to obtain minimum
discovery information. Fetching a richer capability description is a subsequent
application exchange, even when discovery supplies its reference.

# Terminology

Terminology for DAWN is defined in {{I-D.farrel-dawn-terminology}}.

Attention is drawn to the following specific terms defined in
{{I-D.farrel-dawn-terminology}} that are key to this document:

* discovering entity
* discovered entity
* discoverable object
* discovery information
* minimum discoverable information

The client initiating discovery is the discovering entity. In this document,
"minimum discovery information" refers to the minimum discoverable information
whose content is to be defined by the Architecture requirements.

The appendix also uses the following implementation term:

Agent harness
: Software that supports an AI agent's execution, such as interaction with
  models, invocation of tools, management of context and state, and application
  of execution controls. It may support discovery on behalf of the agent. This
  document does not specify its internal operation. Opensource examples of an agent harness 
  include: OpenClaw and Hermes.

# Applicability {#applicability}

The categories in {{categories-of-discovery}} apply in three settings:

| Deployment | Illustrative discovery need | Applicability condition |
| --- | --- | --- |
| Local network | An assistant finds a nearby inference service advertised on its local network. | Discovery visibility is local; using the service remains subject to application permissions. |
| Within an organisation | An enterprise assistant finds an internal data source or tool. | Publication and access follow the organisation's existing administrative and trust arrangements. |
| Between cooperating organisations | An assistant finds a partner's calendar-coordination agent. | The organisations have a trust relationship; discovery finds resources within that relationship. |

Organisations publish independently and may use delegation or federation under
existing trust arrangements. Knowing an organisation's name does not establish
trust. Conversely, a partner's agents and endpoints may be unknown even when
the organisational relationship is established.

DNS and mDNS are possible discovery mechanisms; others may also be suitable.
Protocol work should reuse existing IETF mechanisms where possible.

# Discovery Characteristics

The use cases share a common question: what must a client discover before it
can attempt interaction with an entity?

* Discovery may be initiated by autonomous software or by a human operator.
* The discovered target may be a specific named entity or a set of entities
  determined by properties or classification.
* Capability is often an important discovery input, but it is not the only one.
  Organisation, jurisdiction, locality, protocol, policy, and responsible party
  also appear in several use cases.
* The minimum discovery information may change over time. Freshness and caching
  therefore matter even when detailed runtime properties are obtained later
  through application interaction.
* Discovery may need to account for entities that are dynamic, mobile, or
  available only in a particular context.
* Trust in discovery information is different from trust in the discovered
  entity. A discovery mechanism can help protect discovery metadata, but it
  does not decide whether the discovered entity should be used.
* Brokers and aggregators may serve an organisation or cooperating group.
  Discovery supports independent publication rather than requiring a single
  central registry or an index of resources across the wider Internet.

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

The Architecture determines which query properties belong in minimum discovery
information. Other constraints are evaluated by the application.

Discovery may take several steps. A client may follow a reference, refresh a
cached result, or repeat a query when the information is no longer sufficient.

# Categories of Discovery {#categories-of-discovery}

Each category includes assumptions, discovery impacts, and examples within
the settings in {{applicability}}.

## Capability-Oriented Discovery

A client needs to find an entity that provides a particular function or
capability, such as an agent, tool, task, service, or model-serving endpoint.

### Assumptions

The client can express the required function using the discovery properties
supported by the architecture. A service type or capability identifier may be
sufficient. The result identifies the function and how to reach the entity,
and may include a reference to a capability card.

### Discovery Impacts

Capability-oriented discovery suggests support for discovery by function,
capability, skill, entity type, and protocol. The returned discovery information
needs to include enough information to allow later selection, authorisation,
capability exchange, or communication to be attempted.

### Examples

A scheduling assistant needs to find a calendar-coordination agent at a
partner organisation and learn how to contact it. The appendix develops this
example in {{appointment-coordination}}.

An agentic workflow decomposes a user request into several subtasks. The
workflow needs to discover agents, tools, services, or tasks that can
participate in the work. Discovery provides candidate entities and their
published properties; the workflow then performs selection and orchestration
outside DAWN.

## Resource-Oriented Discovery

A client needs to discover resources supporting an AI system, such as data
sources, knowledge bases, models, inference services, or compute services.

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

Discovery returns the minimum information needed to locate and contact the
resource. It may return a pointer to an application service for current state,
detailed policy, or authorisation. Accessing an already known data source to
read its contents is an application query, not resource discovery.

Properties such as jurisdiction, format, freshness, and access method may
motivate discovery requirements. The Architecture work determines which belong
in the minimum discovery information. Richer descriptions, live availability,
and detailed policy information are obtained outside the discovery process.

### Examples

An enterprise agent needs to find a data source for retrieval-augmented
generation. Discovery identifies a relevant internal source and how to contact
it. The application subsequently checks detailed freshness, format, and access
conditions and retrieves data through the source's native interface.

A scheduler for an AI workload needs to find a compute service within its
organisation or a cooperating provider. Discovery identifies the service and
its contact information. Checking accelerator availability, jurisdictional
constraints, and allocation policy can require subsequent application queries.

An AI application needs to find an inference service for a particular modality.
Discovery supplies the relevant service type and communication information.
Detailed model provenance, safety classification, and permitted use are assessed
outside discovery where they exceed the minimum information.

A user or agent needs to discover a model-serving resource for inference.
Discovery supplies its function and access method; subsequent interaction
obtains richer model information when needed.

## Administrative Scope Extensions

Discovery crosses organisational, administrative, or tenancy boundaries.
A client may need to find a partner's resource, or a provider may expose
different discovery views to its tenants, customers, or departments.

### Assumptions

Organisations control what they publish and who can see it. Cooperation and
authority to act for a user rely on existing arrangements. Discovery information
may identify the publishing domain or responsible party to support later checks.

### Discovery Impacts

DAWN discovery needs to support discovery across administrative domains without
requiring a single central registry. It also needs to support scoped discovery
where the information returned depends on tenant, customer, department, network,
or policy context.

Publication scope helps the client interpret a result. Discovery must also
avoid exposing sensitive tenant or organisational structure to unauthorised
parties.

### Examples

An enterprise agent acting for an employee needs to discover an agent at a
cooperating supplier. The discovery result indicates how to contact the
supplier's agent and provides information needed by later authorisation and
policy checks.

A software-as-a-service provider hosts agents or tools for multiple customers.
Each customer needs discovery information scoped to its own tenancy. The same
provider may also need different discovery views for internal operators and
cooperating customers.

A research consortium operates AI services across several cooperating
institutions with established trust relationships. Each institution publishes
information about its own agents, data services, and tools. Collaborators need
to discover entities by capability while respecting institutional boundaries
and trust models.

## Operational Discovery

A human operator, management system, or AI operations agent needs to locate
AI resources and supporting tools for troubleshooting, audit, incident response,
or compliance review.

### Assumptions

This discovery category assumes that discovery is useful for both autonomous
systems and human-operated tools. It also assumes that operational environments
may be multi-vendor, multi-domain, and partly private.

Operational discovery needs to identify relevant resources and how to contact
them. An operational client may subsequently obtain detailed runtime state,
observability data, or compliance information. Those exchanges are outside
discovery and may require separate permissions.

### Discovery Impacts

DAWN discovery may need to support tooling and operational inspection, not only
agent-to-agent workflows. Discovery metadata may need to be logged, auditable,
and understandable by operators.

Management and diagnostics for the discovery system itself may also be needed
so that operators can understand discovery behaviour and failures.

Brokers, directory services, and operational tools may themselves be discovery
targets when they support an AI system.

Observability of the discovery process is a separate operational consideration.
Recording a discovery result or logging a later action does not itself
constitute discovery of an operational resource.

### Examples

A human operator needs to locate the AI agents maintained by a team within an
organisation. Discovery provides their service types and communication
information. Inspection of their runtime behaviour occurs subsequently.

An AI-assisted network operations system needs to discover telemetry sources,
topology systems, control points, and remediation tools within an organisation
or cooperating group. DAWN can help identify these supporting AI resources and
their communication methods. Diagnosis, correlation, action recommendation,
and remediation remain outside discovery.

An edge deployment includes lightweight agents that need fast and cacheable
discovery because local connectivity is constrained. Discovery provides enough
stable information for connection bootstrapping while avoiding reliance on
rapidly changing operational state.

# Classes of Use Case

The taxonomy in {{I-D.akhavain-moussa-dawn-problem-statement}} provides
background for classifying AI resources and their supporting entities.

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

Outside a local network, all discovery information exchanged between DAWN
participants requires integrity protection. Local deployments may also provide
such protection. Where it is absent, the deployment needs to account for the
risks of unprotected discovery information; locality alone does not establish
trust.

Discovery mechanisms also need to address authenticity, freshness, and access
controls using established security mechanisms and trust arrangements. A
cached digest or version comparison detects change but does not independently
authenticate discovery content. This document does not select a protection
mechanism or define new trust-evaluation methods.

Security of discovery metadata is distinct from trust in the discovered entity.
Authentication, authorisation, attestation, and policy checks for later
interaction are outside discovery.

Identity management and establishing trust relationships are also outside
DAWN's initial scope; an authentic publication does not establish authority to
act for a particular person.

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

Enterprise, cloud, and edge deployments have different needs for publication,
caching, freshness, authorisation, observability, and operational control.

Dynamic information such as current load, availability, price, or status may
change too frequently to be carried directly in a general discovery mechanism.
Such application state can be obtained outside discovery through a referenced
service. The minimum discovery information has its own freshness needs: an
endpoint or supported protocol may also change.

A client may refresh retained information or repeat discovery when it is no
longer sufficient. A changed description need not imply a different entity, and
a temporary communication failure need not imply withdrawal. Recovery of
application state or transfer of an existing task to a replacement is outside
discovery.

Across administrative domains, operational considerations include publication
authority, caching, freshness, visibility controls, logging, abuse handling, and
failure behaviour.

# IANA Considerations

This document has no IANA actions.

--- back

# Cross-Organisation Appointment Coordination {#appointment-coordination}

Alice asks her AI assistant, Hermes, to review her schedule and arrange lunch
with Bob at another organisation, including a restaurant table for two near
the office. Later, she asks to move both the appointment and the reservation
to a different day.

The example combines capability and resource discovery across an organisational
boundary, then shows how Hermes can reuse what it has learned.

## Actors and Assumptions

Hermes Agent provides the agent harness for Alice's assistant. The running
assistant, called Hermes here, is the discovering entity. Alice talks to it
through a conversational interface. Her calendar service is already configured;
Hermes can read it but cannot change it.

Alice's and Bob's organisations are assumed to cooperate under an established
trust relationship. Their calendar agents have not previously interacted.
Hermes knows Bob's organisation but not its calendar-agent endpoints. Bob's
agent can coordinate appointments and create events, subject to permission.

The restaurant-booking service is assumed to be available through a cooperating
provider with an established trust relationship. OpenTable is used as an
illustrative provider; the example assumes a suitable agent-accessible interface
and does not claim that a particular integration or trust arrangement exists.

Alice is assumed to supply enough context to distinguish the intended Bob.

## Initial Discovery at a Known Organisation

Alice asks Hermes to find a time for lunch with Bob on Thursday and book a
table for two near the office. Hermes reads her calendar, then needs to find a
calendar-coordination agent at Bob's organisation. It knows the organisation
and required capability, and may have
constraints on the communication protocol.

Hermes locates the organisation's discovery entry point and queries its
catalogue for calendar-coordination agents. The result identifies candidates
and their contact information. DNS could provide the entry point; the example
does not depend on a particular bootstrap or catalogue protocol.

A candidate may serve the whole organisation or particular users. Hermes needs
to determine whether it can handle the request concerning Bob. The application
then selects a candidate, obtains any necessary authorisation, and exchanges
proposed times. Bob's agent creates the event in his calendar. Hermes still has
no permission to write to Alice's calendar; invitation handling is an
application matter.

## Supporting Resource Discovery and Restaurant Reservation

Hermes obtains free/busy information through the calendar services. Alice's
calendar was already known, so reading it required no discovery. It discovers
any additional data source it needs before querying that source.

With a suitable time identified, Hermes proceeds as follows:

1. Discover the restaurant-booking service through the cooperating provider's
   discovery entry point. The result identifies the booking capability and how
   to contact it.
2. Query the service for restaurants near the office with a table for two at
   the proposed time. Availability, price, and booking conditions come from the
   service's application interface.
3. Present a suitable option to Alice and ask her to confirm the restaurant,
   time, and any booking conditions.
4. On confirmation, request the reservation through the service and retain its
   booking reference. Report whether the reservation succeeded.

The discovery target is the booking service. Restaurant search, table
availability, and reservation are subsequent application activities. The table
is reserved through the service, not through DAWN.

The following exchanges show the restaurant-booking part of the example.
The discovery steps also apply to finding Bob's calendar agent, using his
organisation's discovery entry point instead of the booking provider's.

~~~
 Alice            Hermes              Provider's              Booking
                                       discovery              service
   |                 |                     |                     |
   |--Lunch request-->                     |                     |
   |                 |                     |                     |
  Discovery
   |                 |-Booking capability-->                     |
   |                 <-Name, URI, protocol-|                     |
   |                 |                     |                     |
  Application exchange
   |                 |----------Time, area, party size----------->
   |                 <--------Options, price, conditions---------|
   <-Booking option--|                     |                     |
   |-----Confirm----->                     |                     |
   |                 |----------Reserve selected table----------->
   |                 <---------Result, booking reference---------|
   <-Booking result--|                     |                     |
   |                 |                     |                     |
~~~

## Reconnection and Rediscovery

Alice asks Hermes to move the lunch to Friday. Hermes has cached discovery
information for both the calendar agent and the booking service, including
their names, endpoints, protocols, and available freshness information. If
these remain usable, it can reconnect without repeating the catalogue queries.

An expired record or changed endpoint may require a refresh. If the agent
cannot be found or no longer offers calendar coordination, Hermes can return
to the organisation's discovery entry point. A temporary connection failure
alone does not establish that the agent has been withdrawn.

The application may also need to retrieve a changed capability card and
reassess the agent. Finding a replacement does not establish that it holds
the original booking or has permission to change it.

Hermes checks Friday's calendar availability and asks the booking service
whether the reservation can be moved. It presents the revised arrangements
and any changed conditions to Alice for confirmation, then requests both
changes through the respective services. If only one succeeds, Hermes reports
the outstanding change to Alice. Discovery does not make the two updates a
single transaction.

The services below are contacted separately. If cached information is still
usable, the discovery exchanges are skipped. Availability checks and booking
changes use application interfaces.

~~~
 Alice            Hermes               Discovery            Calendar /
                                     entry points             booking
                                                             services
   |                 |                     |                     |
   |-Move to Friday-->                     |                     |
   |                 |                     |                     |
  Reuse cached discovery information if still valid.
  If refresh or rediscovery is needed:
   |                 |-Name or capability-->                     |
   |                 <---Contact details---|                     |
   |                 |                     |                     |
  Application exchanges with each service
   |                 |--Friday availability / booking reference-->
   |                 <------Options and changed conditions-------|
   <--Revised plan---|                     |                     |
   |-----Confirm----->                     |                     |
   |                 |-----Change appointment / reservation------>
   |                 <-----Separate results for each change------|
   <-----Outcome-----|                     |                     |
   |                 |                     |                     |
~~~

## Discovery Information Needed in This Scenario

The first requests identify an organisation and a capability: calendar
coordination or restaurant booking. Reconnection starts with a known agent or
service. In either case, useful results include:

* the entity's name, type, and a service or capability identifier;
* reachability information and supported communication methods; and
* references used to obtain that minimum information through indirection.

The Architecture defines the minimum field set. A reference may lead to
further discovery information or to richer application information. Fetching
a capability card beyond that minimum, detailed policy, live calendar data,
or table availability is outside discovery. Booking references are application
state, separate from cached discovery information.

## Security, Privacy, and Operational Considerations

All cross-organisation discovery information is integrity-protected under the
assumed trust arrangements, including information obtained through references.
Hermes checks its origin and freshness. An authentic publication does not prove
that an agent may act for Bob. A version comparison can reveal change, but
does not establish authenticity.

The discovery query may reveal Alice's interest in Bob's organisation and its
scheduling service. Calendar contents and personal details can be restricted
to the subsequent authorised exchange. Discovery records may also need access
controls.

For troubleshooting, operators may need to know which source Hermes used,
whether it used cached information, and why it repeated discovery. Logs can record
these decisions, subject to privacy and retention controls.

## Links to the DAWN Requirements

The scenario illustrates several requirements in
{{I-D.king-dawn-requirements}}.

| Part of the scenario | Related requirements |
| --- | --- |
| Finding a calendar or booking capability, then reconnecting to a known entity. | REQ-DISC-2: discovery by function or specific instance; REQ-CLASS-2: classification by capability. |
| Starting at each organisation's discovery entry point. | REQ-PROTO-4: predictable entry points; REQ-ARCH-4: independent publication. |
| Obtaining the endpoint and protocol needed to contact the service. | REQ-PROP-2: communication protocols and transport parameters, directly or by reference. |
| Keeping cached discovery information separate from live calendar and table availability. | REQ-PROP-4 and REQ-PROP-11: property change rates and their implications for caching and refresh. |
| Protecting discovery responses and restricting who can see them. | REQ-SEC-1: authenticity and integrity; REQ-SEC-4: visibility controls. |
| Recording the discovery source and decisions to refresh or repeat a query. | REQ-SEC-7: auditability of discovery operations. |
| Using separate application exchanges to select a restaurant, confirm with Alice, and reserve a table. | REQ-DISC-4: discovery's place in the interaction workflow. |

# Provisioning Edge Compute for Personalised Live Media {#personalised-live-media}

A broadcaster offers a personalised live programme [object-based media delivery]. Viewers may chooses different audio, graphics, or accessibility features. Some devices cannot
combine these media objects themselves, so nearby edge compute renders part
or all of the programme for them.

Before the broadcast, an operator asks a media orchestration agent to arrange enough compute for the expected audience, balancing delay, cost, and energy use. The agent needs to find the services and information sources that can help it do this.

## Actors and Assumptions

The media orchestration agent coordinates the request. A compute allocation agent arranges resources at suitable sites, using an optimisation tool to compare options. Data services provides audience forecasts and information about compute and network conditions.

These entities operate within the broadcaster's organisation or cooperating providers with established trust relationships. The discovery entry points are known, but individual service endpoints may not be.

[Agentic Resource Discovery (ARD)](https://agenticresourcediscovery.org/)
is possible interface to a provider's catalogue in this scenario. It
provide a common way to describe and search agents, tools, and services.
A provider could expose its compute allocation and telemetry services through
ARD, allowing the media agent to find candidates without preconfiguring every
service endpoints or loading every service description into its context. Here,
queries would be limited to the organisation or cooperating providers. ARD is
an illustrative option; protocol choice remains open. Resource allocation and
invocation continue through the service's own interfaces.

## Discovery and Provisioning

1. The media agent queries the relevant discovery entry points for a compute    allocation capability and any required data services. Results identify the entities and how to contact them.
2. The allocation agent discovers suitable site controllers and media-processing    services, including GPU rendering where needed. It obtains their names, service identifiers, endpoints, and supported communication methods.
3. Through the services' application interfaces, the agents obtain audience forecasts, current capacity, and cost, energy, and delay estimates. The optimisation tool uses these inputs and the operator's priorities to propose a placement.
4. Subject to the operator's policy and authorisation, the allocation agent requests provisioning through the site controllers. It reports result, or explains why the available resources cannot meet the request.

The diagram summarises discovery and the later application exchanges. The
agents contact each service separately.

~~~
 Media / allocation       Discovery             Data services /
 agents                  entry points          site controllers
   |                          |                       |
   |--Required capability---->|                       |
   |<--Name, URI, protocol----|                       |
   |                          |                       |
   |--Forecast / resource information request-------->|
   |<--Demand, capacity, cost, energy, delay----------|
   |                                                  |
   |  Compare options using the optimisation tool     |
   |                                                  |
   |--Provision selected resources------------------->|
   |<--Result / resource references-------------------|
~~~

Discovery provides the information needed to contact an entity. Comparing
sites, reserving compute, steering traffic, and delivering media are
application activities outside DAWN.

## Changes During the Broadcast

Audience demand or site availbility may change. The agents can reuse valid
discovery information and query current conditions through the data services.
Changed or expired discovery records may requires a refresh or a new query.
Moving workloads or adding capacity remains an application decision.

## Security and Privacy

Discovery information is integrity-protected, including across provider
boundaries, and its origin and freshness are checked. Finding a controller
does not grants permission to provision resources. Viewer details and detailed
capacity data are restricted to authorised application exchanges.

## Links to the DAWN Requirements

The example reuses requirements in
{{I-D.king-dawn-requirements}}:

* REQ-DISC-2 and REQ-CLASS-2: finding entities by function or capability.
* REQ-PROP-2: obtaining communication details, directly or by reference.
* REQ-PROP-4 and REQ-PROP-11: distinguishing cached discovery information from
  frequently changing resource data.
* REQ-SEC-1 and REQ-SEC-4: protecting discovery information and controlling
  its visibility.
* REQ-???

# Acknowledgments
{:numbered="false"}

The authors thank Adrian Farrel and Jim Mozley for early discussion in the
creation of this document, and their ongoing reviews and comments.

We also thank the following peopl for their DAWN mailing-list comments:
Tommy Jensen (concrete use cases), Mohamed Boucadair (discovery starting
points), Sumit Ahuja (capability discovery), Roman Danyliw (security and
privacy), Lori Jakab (local network discovery), Matthew Quick (cross-domain
applicability), Pete Resnick (agent identity considerations), and Mirja
Kuehlewind (discovery steps).

Finally, we thank the following for their contribution to the use case practical 
examples:

* Revika Anand, Lancaster University
* Edward Revika, Lancaster University
