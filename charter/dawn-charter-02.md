# Discovery of Agents With Names (DAWN)

Agentic AI systems depend upon the interaction between an entity (a 
device or software, including but not limited to an AI agent) and an
AI agent.  For this to work, the entity must find available AI agents
and learn how to contact them about their specific capabilities.

The focus this working group will be on how an entity can discover an
agent's specific properties before proceeding: what type of agent they
are, what their reachability information is, what communication protocols 
options are available, what services do they offer, and what information 
schemes they support.  Additional more detailed metadata may be communicated
as well, or may be left out of scope for direct capabilities exchange between 
entity and AI agent.

To support these goals, the working group will specify an interoperable
and generic discovery mechanism that builds on existing protocols and tools,
benefits from established trust models, supports proven delegation and
federation architectures, and allows organisations to independently
publish discovery information.

## Scope

Discovery in the DAWN context is limited to "find me an
agent to interact with" within an organization, within collaborating
organizations, or within local networks.  This may include
communication about the following example attributes:

- What is the agent's type and classification?
- What communication and security protocols does the agent support?
- What are the minimum requirements for information exchange?

Where possible, any solutions work will be built in a modular way
using existing IETF protocols that provide support for any needed
communication, authentication and privacy. The WG will consider mDNS
and DNS as potential mechanisms upon which to build a discovery protocol,
but may examine other solutions as well.

Although initially focused on discovery of AI agents, agentic tools,
and agentic skills, the WG should strive to produce results that are
general and reusable within other discovery contexts if possible.

## Out of Scope

Specifically out of scope of the DAWN WG during its initial phase are:

- Bulk transfer of more capability information beyond the minimal
  requirements to establish communications.
- All communication between entities beyond the initial discovery process.
- Discovery across the wider Internet.
- Agentic AI stable identifiers 
- Entity registration within discovery servers
- Discovery of discovery servers.
- How the interoperable information schema is made extensible.
- Availability of attestation evidence and results for agents. 

Future DAWN or other WG charters may consider taking on these tasks.

## Deliverables

The DAWN working group will work on the following deliverables:

- Terminology: The definition of common DAWN terminology for use in
  the other DAWN documents. (May be published as an Informational RFC or
  included in the Architecture document.)

- Discovery Architecture: A document describing the problem space,
  requirements, and the resulting DAWN architecture. (To be published
  as an Informational RFC, but may be held until the Protocol work is
  very stable.)

- Use Cases: A document describing broad use case categories.
  (May be remain as an Internet-Draft informing other work or may be
  published as an Informational RFC.)

- Protocol: A specification describing the applicability of existing
  protocols and tools, and defining the protocol semantics or
  extensions developed to achieve the initial discovery goals within
  the Discovery Architecture. 

## Coordination with Other Working Groups and Organisations

The DAWN working group will seek to coordinate with other WGs and
external standards bodies as necessary.  These may include WIMSE,
CORE, CATS, DNSSD, DNSOP, ADD, DELEG, ITU-T SG17, ITU-T FG-TIDA, 3GPP,
and the Linux Foundation.

## Milestones

TBD
