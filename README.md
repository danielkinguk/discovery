# Discovery of Entities
This document provides short description of a proposed Discovery work item.
This is not a BoF Request and not a draft Working Group Charter.
The intention is to capture the scope of a piece of work that the proponents believes is in IETF scope and needs urgent attention.
Our hope is that Area Directors will help us dispatch this to a place to do the work:
- an existing working group
- a new working group
The proponents fully intend to continue refining existing Internet-Drafts concurrent with any work-dispatch process.

## Terminology 

- Entity: A system component that communicates at a peer-to-peer or client-server level with another entity. Examples include, AI agents.
- Object: The records in the discovery system.
- Function: The functional processing capability that an entity offers. Examples include, tasks, workloads, jobs, services, tools.
- Tasks: Legacy term kept for continuity with earlier drafts.
- Jobs: Legacy term kept for continuity with earlier drafts.

## Problem Statement and Work Scope

Many distributed processing environments depend on the interaction between components that do not have pre-configured relationships. In order for these systems to operate correctly, the components must be able to discover each other. For complete generality, we call these components "entities". Entities may be software tasks, workloads (cf. WIMSE), services, AI agents, etc.

This discovery is as simple as asking "Find me an entity to talk to." However, there is a lot of detail underlying this question including:
- What functionality do we want an entity to provide for us?
- How do I communicate with that entity?
- Is the information about the entity trustable?

There is a functional layer after discovery that determines which instance of a class of entity should be used. This process may examine location, reachability, load, and operational status. Those pieces of information have to be examinable, but they do not form part of the core discovery function, but may be implemented by a discovered intermediary aggregation point or broker. This element of the problem space is not in scope for the discovery work.

However, the different parts of the problem space lead to considering the distinction between mandatory base information which is likely to be static or semi-static, and more dynamic information that could be changing frequently and which is likely to cause scaling and stability issues for a discovery system.

This work effort seeks to solve the following questions:
- How is an entity classified with respect to its function, origin, location, and type?
- How is an entity communicated with?
- What is the base set of information that is held for each entity?
- How is the information extensible on a per class-of-entity basis?
- Can this problem be solved in a centralised and distributed way?

Issues of the larger architecture of how entities select each other and how they communicate are out of scope. How agents register and authenticate their registration are also how of scope. The solution should work independent of the discovery architecture and the system architecture into which the discovery system sits.

Where possible, any solutions work will be built in a modular way using existing IETF protocols. However, no protocol solution choices will be made until the requirements (functional and behavioral) have been agreed.

## Functional Requirements

- Who discovers (an entity)
- Who is discovered (another entity or a class of entities)
- What information is being discovered?
	- Who is responsible for this vs anonymous
	- Type (e.g., IETF, Microsoft,...)
	- What it does (functionality)
	- How much of this function can it do
	- How do I communicate with the entity (and security for communications)
	- Who made the registration (trust or no-trust authentication)
- How do I register my entity (with option for attestation) — out of scope

### Mandatory

### Optional 

## Out Of Scope
- Trust 
- Responsibility
- Capability and Negotiation 
- Tasks Management
- Agent-to-agent communications

## Proponents
This is a list of people who contributed to the discussions that led to this work description. Draw no conclusions from the ordering of people in this list.
- Nic Williams <nwilliams@infoblox.com>
- Laurent Ciavaglia <laurent.ciavaglia@nokia.com>
- Arashmid Akhavain <arashmid.akhavain@huawei.com>
- Hesham Moussa <hesham.moussa@huawei.com>
- Roland Schott <Roland.Schott@telekom.de>
- Zaheduzzaman Sarker <zahed.sarker.ietf@gmail.com>
- Daniel King <daniel@olddog.co.uk>
- Adrian Farrel <adrian@olddog.co.uk>
- Schema Definition

