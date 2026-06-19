# Discovery of Agents, Workloads, and Named entities (DAWN)

Many distributed processing environments depend on the interaction 
between components that do not have pre-configured capability, 
location, or reachability relationships. In order for these components
to operate correctly, the components must be able to discover each 
other. For complete generality, we call these components "entities".
Entities may be tasks, workloads, endpoints, services, AI agents, etc.

The principle use case of this working group will be focusing on how
an AI agent can find another AI agent with specific capabilities, or
how a workload orchestrator can to locate compute resources in a
particular jurisdiction, or how a service consumer can discover
providers that support a required protocol version.  In each case, an
entity needs knowledge of any other entity's specific properties
before proceeding: what type of entity are they, what services do they
offer, what communication protocols options are available, and what
information schemes they support.  Additional metadata may be
communicated as well, such as how many tokens it can support, whether
it is reactive or proactive, whether it depends on a particular model,
and what data it needs as input

To support these goals, an interoperable and generic discovery
mechanism is needed that builds on existing protocols and tools,
benefits from established trust models, supports proven delegation and
federation architectures, and allows organisations to independently
publish discovery information.

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
- What is the common base set of information that is held for all
  entity types?
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

- Specify the mandatory base information common across all entity types.

- Examine the distinction between static or semi-static information, and
  more dynamic information that could be changing frequently and which is
  likely to cause scaling and stability issues for a discovery system.

- Examine all types of entity and their special needs with respect to
  discovery, and contrast them with state-of-the-art discovery tools
  and mechanisms.
  
- Consider the specific applicability to the discovery of AI agents, but
  will also seek to generalise discovery to the broader context of entities.
  The aim will be to derive general solutions that are applicable across
  all classes of entity (current and future) allowing for future use cases.

- Ensure that security is central to the discovery architecture and solution such
  that security information that is registered for an entity can be
  referenced or published in discovery mechanisms, so that discovered
  information can be attested, so that the discovery relationship can
  be authenticated, and so that discovered information can be kept
  private in flight.

Where possible, any solutions work will be built in a modular way using existing
IETF protocols. However, no protocol solution choices leading to the adoption of
solutions documents addressing the DAWN problem space will be made until the
requirements (functional and behavioral) have been agreed, and then this will
require an analysis of the applicability of existing protocols and what gaps need
to be filled. 

## Out of Scope

There are functional layers that surround and interact with discovery:

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
- Trust, authentication, and authorisation of the entities in their entity-to-entity communications.
- Capability exchange and negotiation between entities.
- Establishing the relationship between entities and their local gateways.
- Entity-to-entity communication.

## Deliverables

The DAWN working group will work on the following deliverables:

- Terminology: A short document that sets out agreed common terms for use in the
  other DAWN documents.

- Problem Statement: An explanation of the discovery problem being addressed by DAWN and
  the classes of entity that DAWN is attempting to serve.

- Use Cases: This document will not attempt to describe individual use cases in
  detail, but will develop broad categories of use case that may help
  steer solution development to address general problems rather than
  specific niches.

- Requirements: The requirements that a discovery solution MUST/SHOULD/MAY address.

- Gap Analysis: A gap analysis / applicability statement to cover existing protocols
  with reference to the requirements set out in the requirements document.

- Information Model: A structured information model describing what can be discovered for
  generic entities across all categories of use case. This will be
  augmentable to include discoverable properties for particular classes
  of entity or categories of use case. Other optional object properties 
  will remain the responsibility of external forums and vendors, so the 
  information model must be augmentable.

- Security and Policy Architecture: An architecture document that describes how security and policy
  enforcement can be integrated into the discovery system.

The working group may also work on a broader architecture and a protocol framework overview that show how
discovery fits into an ecosystem (including registration, instance selection,
and entity-to-entity communication), but it is expected that this work will
be coordinated with other relevant working groups.

It is anticipated that the DAWN working group will also develop protocol
solutions documents. However, this work should not progress faster than 
the requirements and gap analysis documents listed above, and that 
extensions to existing an IETF protocol should be done in coordination with
the working group that owns the protocol. While use-case-specific solutions
or solution extensions will be considered, generalised solutions that are
applicable to the broad problem-space will be preferred. 

Although initially focused on discovery of AI agents, the WG is
expected to produce results that are reusable within other contexts
whenever possible.

## Coordination with Other Working Groups and Organisations

This work is closely related to work done in other working groups and
organisations. The DAWN working group will seek to take input from other
experts while attempting to bring them together to coordinate on this
issue. This should include ITU-T SG17, 3GPP, and the Linux Foundation.

Within the IETF, DAWN will coordinate with WIMSE for consideration of
"workloads", CORE for consideration of "endpoints", CATS for discovery of
computing services, and any working group established to consider AI
agent-to-agent communications. Additionally, the DAWN working group will
only work on extensions to an IETF protocol if the working group responsible
for the protocol agrees that the work should be done in DAWN.

## Milestones

TBD nearer the time of a BoF
