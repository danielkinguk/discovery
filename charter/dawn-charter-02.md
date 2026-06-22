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

Although initially focused on discovery of AI agents, agentic tools,
and agentic skills, the WG is expected to produce results that are
general and reusable within other discovery contexts whenever
possible.

## Out of Scope

Specifically out of scope of the DAWN WG, at least during its initial
launch, includes:

- Entity registration within discovery servers
- Discovery of discovery servers.
- Bulk transfer of larger capabilities beyond the minimal
  establishment requirements.
- All communication between entities beyond the initial discovery process.

Future DAWN or other WG charters may consider taking on these tasks.

## Deliverables

The DAWN working group will work on the following deliverables,
roughly in this order:

- Terminology: A document defining common DAWN terminology for use in
  the other DAWN documents (Informational).

- Discovery Architecture: A document describing the problem space,
  requirements and the resulting DAWN architecture (Informational).

- Use Cases: A document describing broad use case categories
  (Optional, Informational).

- Protocol: A specification defining the protocol developed within the
  DAWN WG for communicating entity discovery and capability information.

## Coordination with Other Working Groups and Organisations

The DAWN working group will seek to coordinate with other WGs and
external standards bodies as necessary.  These may include WISME,
CORE, CATS, ITU-T SG17, 3GPP, and the Linux Foundation.

## Milestones

TBD
