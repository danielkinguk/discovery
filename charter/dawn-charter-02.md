# Discovery of Agents With Names (DAWN)

AI systems depend upon the interactions between an entity (a
device or software, including but not limited to an AI agent) and 
one or more AI resources. For these interactions to work, the entity
must determine available AI resources and learn how to contact them.

The focus of this working group is on how an entity can discover an
agent's specific properties before proceeding: what type of agent it
is, what its reachability information is, what communication protocol 
options are available, and what services it offers. Additionally, more 
detailed metadata may be communicated as well, or may be left out of scope
for direct capabilities exchange between entity and AI agent.

To support these goals, the working group will specify an interoperable
and generic discovery mechanism that builds on existing protocols and tools,
benefits from established trust models, supports proven delegation and
federation architectures, and allows organizations to have independently
published discovery information.

## Scope 

Discovery in the DAWN context is limited to "find me an agent resource to
interact with" within an organization, between organizations, or within a 
local network. This may include communication about the following 
example attributes:

- What is the agent resource's type and classification?
- What communication and security protocols does the discovered agent resource support?
- What are the minimum requirements for information exchange?

Where possible, any solutions will be built in a modular way
using existing IETF protocols that provide support for any needed
communication, authentication, and privacy. The WG will consider mDNS
and DNS as potential mechanisms upon which to build a discovery protocol,
but may examine other solutions as well.

Note that discovery may be an iterative process and utilize indirection as
well as direct data transfer.

Although initially focused on discovery of AI agents, agentic tools,
and agentic skills, the WG should strive to produce results that are
general and reusable within other discovery contexts if possible.

## Out of Scope

Specifically out of scope for the DAWN WG during its initial phase are:

- Bulk transfer of capability information beyond the minimum
  requirements to establish communication.
- All communication between entities beyond the initial discovery process.
- Discovery of AI resource indexing across the wider Internet.
- Agentic AI stable identifiers.
- Entity registration within discovery servers.
- Discovery of discovery servers.
- How the interoperable information schema is made extensible.
- Definition of trust management and trust evaluation methods, but not
  excluding discovery of information that identifies the party that
  published or asserts it.

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
  (May remain as an Internet-Draft informing other work, or may be
  published as an Informational RFC.)

- Protocol: A specification describing the applicability of existing
  protocols and tools, and defining the protocol semantics or
  extensions developed to achieve the initial discovery goals within
  the Discovery Architecture. 

## Coordination with Other Working Groups and Organizations

The DAWN working group will seek to coordinate with other WGs
working on DNS, discovery, identities, or AI. It will also
coordinate with external standards bodies as necessary.

## Milestones

April 2027
Publication for DAWN Terminology document as an Informational RFC.

June 2027
Completion of DAWN Use Cases document.

December 2027
Publication request for DAWN Protocol Specification and Applicability
document as a Standards Track RFC.

January 2028
Publication request Discovery Architecture for as an Informational RFC.
