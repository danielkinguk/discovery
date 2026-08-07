# Discovery of Agents, Workloads, and Named entities (DAWN)

Many distributed processing environments depend on the interaction
between components that do not have pre-configured capability,
location, or reachability relationships. In order for these components
to operate correctly, the components must be able to discover each
other. For complete generality, we call these components "entities".
Entities may be AI agents, software, services, endpoints, tasks,
workloads, etc.

The principle use case of this working group will be focusing on how
an entity (a device or software, including but not limited to an AI
agent) connected to a network can find available AI agents and how to
contact them about their specific capabilities.  The entity will need
to discover the agent's specific properties before proceeding: what
type of agent are they, what communication protocols options are
available, what services do they offer, and what information schemes
they support.  Additional more detailed metadata may be communicated
as well, such as how many tokens it can support, whether it is
reactive or proactive, whether it depends on a particular model, and
what data it needs as input.

To support these goals, an interoperable and generic discovery
mechanism is needed that builds on existing protocols and tools,
benefits from established trust models, supports proven delegation and
federation architectures, and allows organisations to independently
publish discovery information.

## Scope

Discovery in the DAWN context is limited to being able to "find me an
agent to interact with" within an organization, within collaborating
organizations or within local networks.  This may include
communication about the following example attributes:

- What is the agent's type and classification?
- What communication and security protocols does the agent support?
- What is the minimum requirements for information exchange?

Where possible, any solutions work will be built in a modular way
using existing IETF protocols that provide support for any needed
communication, authentication and privacy. The WG will consider mDNS
and DNS as potential initial contact mechanisms upon which to build a
discovery protocol, but may examine other solutions as well.

Although initially focused on discovery of AI agents, agentic tools,
and agentic skills, the WG should strive to produce results that are
general and reusable within other discovery contexts if possible.

## Out of Scope

Specifically out of scope of the DAWN WG during its initial launch,
includes:

- Bulk transfer of larger capabilities beyond the minimal
  establishment requirements.
- All communication between entities beyond the initial discovery process.
- Agentic AI stable identifiers 
- Entity registration within discovery servers
- Discovery of discovery servers.
- How is the interoperable information schema extensible?
- What attestation evidence and results are available, if any, for the agent? 

Future DAWN or other WG charters may consider taking on these tasks.

## Deliverables

The DAWN working group will work on the following deliverables,
roughly in this order:

- Terminology: A document defining common DAWN terminology for use in
  the other DAWN documents (Optionally published as Informational or
  included in the Architecture document).

- Discovery Architecture: A document describing the problem space,
  requirements and the resulting DAWN architecture (Informational).

- Use Cases: A document describing broad use case categories
  (Optionally published as Informational).

- Protocol: A specification defining the protocol semantics or
  extensions developed to achieve the initial discovery goals within
  the Discovery Architecture.

## Coordination with Other Working Groups and Organisations

The DAWN working group will seek to coordinate with other WGs and
external standards bodies as necessary.  These may include WIMSE,
CORE, CATS, DNSSD, DNSOP, ADD, DELEG, ITU-T SG17, ITU-T FG-TIDA, 3GPP,
and the Linux Foundation.

## Milestones

TBD
