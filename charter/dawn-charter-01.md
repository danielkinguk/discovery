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

Discovery in the DAWN context is limited to being able to "find me an
entity to talk to" within a collaborating organization.  This includes
communication about the following attributes:

- What is the entity's type and classification?
- What functionality does a discovered entity provide?
- What communication and security protocols does the entity support?
- What is the minimum requirements for information exchange?
- How is the interoperable information schema extensible?
- What attestation evidence and results are available, if any, for the entity? 

Where possible, any solutions work will be built in a modular way
using existing IETF protocols that provide support for any needed
communication, authentication and privacy. The WG will consider the
DNS as a likely initial protocol upon which to build a discovery
protocol.

Although initially focused on discovery of AI agents, the WG is
expected to produce results that are general and reusable within other
discovery contexts whenever possible.

## Out of Scope

Specifically out of scope of the DAWN WG, at least during its initial
launch, includes:

- Entity registration within discovery servers
- Discovery of discovery servers.
- Bulk transfer of larger capabilities beyond the minimal
  establishment requirements.
- All communication between entities beyond the initial discovery process.

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
