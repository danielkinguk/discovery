# Discovery of Agents With Names (DAWN)

AI systems depend upon the interactions between an client (a
device or software, including but not limited to an AI agent) and 
one or more AI resources. For these interactions to work, the client
must determine available AI resources and learn how to contact them.

The focus of this working group is on how a client can discover an
AI agent's specific properties before proceeding: what type of agent it
is, what its reachability information is, what communication protocol 
options are available, and what services it offers. Additionally, more 
detailed metadata may be communicated as well, or may be left out of scope
until a subsequent direct capabilities exchange between a client and an AI agent.
Note that discovery may be an iterative process, and may utilize either direct 
transfer or indirection.

To support these goals, the working group will specify an interoperable
and generic discovery mechanism that builds on existing protocols and tools,
benefits from established trust models, supports proven delegation and
federation architectures, and allows organizations to have independently
published discovery information.

## Scope 

Discovery in the DAWN context is limited to a client requesting, "Find
me an agent resource to interact with," within a local
network, within an organization, or between organizations. This may
include communication about the following example attributes:

- What is the agent resource's type and classification?
- What communication and security protocols does the discovered agent support?
- What are the minimum requirements for information exchange?

Where possible, any solutions created by this WG will be built in a
modular way using existing IETF protocols that provide support for any
needed communication, authentication, and privacy. The WG will
consider mDNS and DNS as potential mechanisms upon which to build a
discovery protocol, but may examine other solutions as well.

Although initially focused on discovery of AI agents and their
capabilities, the WG should strive to produce results that are general
and reusable within other discovery contexts if possible.

## Out of Scope

Specifically out of scope for the DAWN WG during its initial phase are:

- Bulk transfer of capability information beyond the minimum
  requirements to establish communication.
- All communication beyond the initial discovery process.
- AI resource indexing across the wider Internet.
- Stable identifiers of AI agents, tools and skills.
- AI agent or other resource registrations within discovery servers.
- Discovery of discovery servers.
- Interoperable information schemas beyond discovering a transfer protocol.
- Trust management and trust evaluation methods beyond defining trust
  content exchange protocols.

Future DAWN or other WG charters may take on these tasks.

## Deliverables

The DAWN working group will work on the following deliverables:

- Terminology: The definition of common DAWN terminology for use in
  the other DAWN documents. (May be published as an Informational RFC or
  included in the Architecture document.)

- Discovery Architecture: A document describing the problem space,
  requirements, and the resulting DAWN architecture. (May be published
  as an Informational RFC, but maybe held until the Protocol work is
  considered stable.)

- Use Cases: A document describing broad DAWN use case categories.
  (May be published as an Informational RFC)

- Protocol: A specification describing the implementation of the
  Discover Architecture (To be published as a Standards Track document).

## Coordination with Other Working Groups and Organizations

The DAWN working group will seek to coordinate with other WGs
relating to DNS, discovery, identities, or AI. It will also
coordinate with external standards bodies as necessary.

## Milestones

April 2027
Optional submission of the DAWN Terminology document to the IESG for publication.

June 2027
Optional submission of the DAWN Use Cases document to the IESG for publication.

December 2027
Submission of the DAWN Protocol specification to the IESG for publication.

January 2028
Optional submission of the DAWN Architecture document to the IESG for publication.
