# Discovery of Agents, Workloads, and Named entities (DAWN)

Many distributed processing environments depend on the interaction 
between components that do not have pre-configured capability, 
location, or reachability relationships. In order for these systems
to operate correctly, the components must be able to discover each 
other. For complete generality, we call these components "entities".
Entities may be tasks, workloads, endpoints, services, AI agents, etc.

For example, an AI agent may need to find another agent with specific
capabilities, a workload orchestrator may need to locate compute
resources in a particular jurisdiction, or a service consumer may need
to discover providers that support a required protocol version.

In each case, an entity needs knowledge of remote entities before 
interaction can proceed: what they are, what they offer, and whether
they can be trusted. Such knowledge could be obtained through static
configuration, but this approach is impractical at scale and across
organisational boundaries. Automated discovery mechanisms are needed.

Up to now, where automated discovery exists, it is typically handled
through proprietary directories or platform-specific mechanisms. Such
approaches do not scale across organisational boundaries and create
fragmented ecosystems where entities cannot find entities managed by
other organisations.

An interoperable and generic discovery mechanism is needed that builds on existing
protocols and tools, benefits from an established trust model, supports
proven delegation and federation architectures, and allows organisations
to independently publish discovery information.

Providing a decentralised and interoperable discovery mechanism is 
essential to protecting the openness of the Internet and protecting
against dominance by a single or a small number of providers. Integral
to this is building a governance system for the registration of entities.

The Discovery of Agents, Workloads, and Named entities (DAWN) working
group is chartered to develop requirements, information models, and
protocol solutions for entity discovery.

## Scope

Discovery in the DAWN context is as simple as requesting, "Find me an
entity to talk to." However, there is a lot of detail underlying this
request including:
- What functionality do we want an entity to provide for us?
- What mechanisms exist to facilitate communication with that entity?
- Is the information about the entity trustable?

The DAWN working group seeks to resolve the following questions as part
of resolving the discussions of entity discovery:
- How is an entity classified with respect to its function, origin,
  location, and type?
- How can an entity be communicated with by another entity?
- What is the base set of information that is held for each entity?
- How is the information extensible on a per class-of-entity basis?
- Can discovery be solved in different ways (centralised, partially
  distributed - i.e., with delegation - or fully distributed) with
  proper consideration of scaling, consolidation, regulation, etc.)?

The DAWN working group will:

- Consider discovery scopes to describe the domain over which discovery
  is performed. Discovery scope may be specified in one or more dimensions,
  including but not limited to administrative identifiers, trust domains,
  topological or distance metrics, geographic or jurisdictional boundaries,
  and temporal constraints. Discovery scope bounds the search space and
  supports scalability, relevance, and policy enforcement.

- Examine the distinction between mandatory base information which is
  likely to be static or semi-static, and more dynamic information that
  could be changing frequently and which is likely to cause scaling and
  stability issues for a discovery system.

- Examine all types of entity and their special needs with respect to
  discovery, and contrast them with state-of-the-art discovery tools
  and mechanisms.
  
- Consider the specific applicability to the discovery of AI agents, but
  will also seek to generalise discovery to the broader context of entities.
  The aim will be to derive general solutions that are applicable across
  all classes of entity (current and future) allowing for future use cases.

- Ensure that security is central to the architecture and solution such
  that security information that is registered for an entity can be
  referenced or published in discovery mechanisms, so that discovered
  information can be attested, so that the discovery relationship can
  be authenticated, and so that discovered information can be kept
  private in flight.

Where possible, any solutions work will be built in a modular way using existing
IETF protocols. However, no protocol solution choices will be made until the
requirements (functional and behavioral) have been agreed, and then this will
require an analysis of the capabilities of existing protocols and what gaps need
to be filled. 

## Out of Scope

There are functional layers that suround and interact with discovery:

- There is a functional layer before discovery that allows entities to
  register themselves for discovery. This element of the problem
  space is not in scope for DAWN.

- There is a functional layer after discovery that determines which 
  instance of a class of entity should be used. This process may consider
  location, reachability, load, version, and operational status. Those
  pieces of information have to be available for consideration, but they
  do not form part of the core discovery function: they may be implemented
  by a discovered intermediary aggregation point or broker or learned
  through direct communication with entities in the form of capability
  exchange and negotiation.. This element of the problem space is not in
  scope for DAWN.

Issues of the larger architecture of how entities select each other and
how they communicate are out of scope. How agents register and authenticate
their registration are also out of scope.

Additionally out of scope for DAWN are:
- Design, definition, and governance of the naming systems for entities.
- Trust, authentication, and authorisation of the entities.
- Capability exchange and negotiation between entities.
- Entity-to-entity communication.

## Deliverables

The DAWN working group will work on the following deliverables:

Terminology:
: A short document that sets out agreed common terms for use in the
  other DAWN documents.

Problem Statement:
: An explanation of the discovery problem being addressed by DAWN and
  the classes of entity that DAWN is attempting to serve.

Use Cases:
: This document will not attempt to describe individual use cases in
  detail, but will develop broad categories of use case that may help
  steer solution development to address general problems rather than
  specific niches.

Requirements:
: The requirements that a discovery solution MUST/SHOULD/MAY address.

Gap Analysis:
: A gap analysis / applicability statement to cover existing protocols
  with reference to the requirements set out in the requirements document.

Information Model:
: A structured information model describing what can be discovered for
  generic entities across all categories of use case. This will make a
  discoverable properties for particular classes of entity or categories
  of use case. Other optional object properties will remain the
  reponsibility of external forums and vendors, so the information model
  must be aumentable.

Security and Policy Architecture:
: An architecture document that describes how security and policy
  enforcement can be integrated into the discovery system.

The working group may also work on a broader architecture that shows how
discovery fits into an ecosystem (including registration, instance selection,
and entity-to-entity communication), but it is expected that this work will
be coordinated with other relevant working groups.

It is anticipated that the DAWN working group will also develop protocol
solutions documents. However, this work should not progress faster than 
the requirements and gap analysis documents listed above, and that 
extensions to existing an IETF protocol should be done in coordination with
the working group that owns the protocol. While use-case-specific solutions
or solution extensions will be considered, generalised solutions that are
applicable to the broad problem-space will be prefered. 

## Coordination with Other Working Groups and Organisations

This work is closely related to work done in other working groups and
organisations. The DAWN working group will seek to take input from other
experts while attempting to bring them together to coordinate on this
issue. This should include ITU-T SG17 and the Linux Foundation.

Within the IETF, DAWN will coordinate with WIMSE for consideration of
"workloads", CORE for consideration of "endpoints", and any working group
established to consider AI agent-to-agent communications. Additionally,
the DAWN working group will only work on extensions to an IETF protocol
if the working group responsible for the protocol agrees that the work
should be done in DAWN.

## Milestones

TBD nearer the time of a BoF
