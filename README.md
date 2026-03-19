# Discovery of Entities
This document provides short description of a proposed Discovery IETF work item.
This is not a BoF Request and not a draft Working Group Charter.
The intention is to capture the scope of a piece of work that the proponents believes is in IETF scope and needs urgent attention.
Our hope is that Area Directors will help us dispatch this to a place to do the work:
- an existing working group
- a new working group

The proponents fully intend to continue refining existing Internet-Drafts concurrent with any work-dispatch process.

## Terminology 

- Entity: A system component that communicates at a peer-to-peer or client-server level with another entity. Examples include, tools, skills, tasks, workloads, services, task owners, and AI agents.
- Object: The records in the discovery system. Examples include, agent cards, task cards, resource cards, tool cards, and skill cards.
- Function: The functional processing capability that an entity offers. Examples include, tasks, workloads, endpoints, jobs, services, tools.
- Tasks: Legacy term kept for continuity with earlier drafts.
- Jobs: Legacy term kept for continuity with earlier drafts.
- Registration: The steps by which agents can register their existence. This should include attestation and other security mechanisms.
- Discovery: A process by which an entity can find another entity or a set of entities of a type that can perform a desired function. **The purpose of this work effort is limited to just this element. It is described in more detail in the Problem Statement and the Functional Requirements, below.**
- Capability exchange / negotiation: The processes by which agents can exchange details of what they can do, dynamic information about statuses (including workloads), and which particular features/functions they want to engage.
- Selection: The mechanisms and policies by which an agent determines which other agents it will communicate with.

## Problem Statement and Work Scope

Many distributed processing environments depend on the interaction between components that do not have pre-configured relationships. In order for these systems to operate correctly, the components must be able to discover each other. For complete generality, we call these components "entities". Entities may be tasks, workloads (cf. WIMSE), endpoints (cf. CoRE), services, AI agents, etc.

This discovery is as simple as asking "Find me an entity to talk to." However, there is a lot of detail underlying this question including:
- What functionality do we want an entity to provide for us?
- What mechanisms exist to facilitate ommunication with that entity?
- Is the information about the entity trustable?

There is a functional layer after discovery that determines which instance of a class of entity should be used. This process may examine location, reachability, load, and operational status. Those pieces of information have to be examinable, but they do not form part of the core discovery function, but may be implemented by a discovered intermediary aggregation point or broker. This element of the problem space is not in scope for the discovery work.

However, the different parts of the problem space lead to considering the distinction between mandatory base information which is likely to be static or semi-static, and more dynamic information that could be changing frequently and which is likely to cause scaling and stability issues for a discovery system.

Many discovery techniques exist today, and work has progressed beyond the discovery of simple web sites. This work effort will examine new types of entities and their special needs with respect to discovery and contrast them with state of the art discovery tools and mechanisms. Applicability will include the discovery of AI agents, but will also seek to generalise discovery to "entities" as defined here.

This work effort seeks to solve the following questions:
- How is an entity classified with respect to its function, origin, location, and type?
- How is an entity communicated with?
- What is the base set of information that is held for each entity?
- How is the information extensible on a per class-of-entity basis?
- Can this problem be solved in a centralised and distributed way? (Consider scaling, consolidation, regulation, etc.)

Issues of the larger architecture of how entities select each other and how they communicate are out of scope. How agents register and authenticate their registration are also out of scope. The solution should work independent of the discovery architecture and the system architecture into which the discovery system sits.

Where possible, any solutions work will be built in a modular way using existing IETF protocols. However, no protocol solution choices will be made until the requirements (functional and behavioral) have been agreed.

## Functional Requirements

- What are primary scenario groupings (categories) where discovery is needed.
- Who discovers (an entity)
- Who is discovered (another entity or a class of entities)
- What information is being discovered?
	- Who is responsible for this vs anonymous
	- Type (e.g., IETF, Microsoft,...)
	- What it does (functionality)
	- How much of this function can it do
	- How communication mechanisms excist for communication with the entity (and security for communications)
	- Who made the registration (trust or no-trust authentication)
- How is discovery achieved?
- Where does discovery fit in the overall workflow?

Discovered Information may be further categorised as:
- Mandatory or Optional
- Static, Mainly Static, or Dynamic
- Extensible by vendor/implementation, through further standardisation, or not at all

## Out Of Scope
- How do I register my entity (with option for attestation)
- Trust 
- Responsibility
- Capability and Negotiation 
- Tasks Management
- Agent-to-agent communications

## Implementations and Interoperability

>>> This section to be completed per suggestions at IETF Plenary

### What are implementable components?

### What needs to be standardised?

### What are the interoperability interfaces?

## Proponents
This is a list of people who contributed to the discussions that led to this work description. Draw no conclusions from the ordering of people in this list.
- Nic Williams <nwilliams@infoblox.com>
- Laurent Ciavaglia <laurent.ciavaglia@nokia.com>
- Arashmid Akhavain <arashmid.akhavain@huawei.com>
- Hesham Moussa <hesham.moussa@huawei.com>
- Roland Schott <Roland.Schott@telekom.de>
- Zaheduzzaman Sarker <zahed.sarker.ietf@gmail.com>
- Jim Mozley <jmozley@infoblox.com>
- Daniel King <daniel@olddog.co.uk>
- Adrian Farrel <adrian@olddog.co.uk>

## Relevant Internet-Drafts
This section does not imply that any draft is *the* draft, but attempts to show that people are thinking about this topic already.
- "AI Agent Discovery (AID) Problem Statement" <https://datatracker.ietf.org/doc/draft-mozley-aidiscovery/>
- "DNS for AI Discovery" <https://datatracker.ietf.org/doc/draft-mozleywilliams-dnsop-dnsaid/>
- "A Layered Approach to AI discovery" <https://datatracker.ietf.org/doc/draft-am-layered-ai-discovery-architecture/>
- "Task discovery in agentic networks" <https://datatracker.ietf.org/doc/draft-mapmw-task-discovery/>
- "Agent Identity and Discovery (AID)" <https://datatracker.ietf.org/doc/draft-nemethi-aid-agent-identity-discovery/>
- "Agent Registration and Discovery Protocol (ARDP)" <https://datatracker.ietf.org/doc/draft-pioli-agent-discovery/>
- "AI Agent Discovery and Invocation Protocol" <https://datatracker.ietf.org/doc/draft-cui-ai-agent-discovery-invocation/>
- "Agent Registration and Discovery Protocol (ARDP)" <https://datatracker.ietf.org/doc/draft-pioli-agent-discovery>
- "DNS-based Service Discovery for Computing-Aware Traffic Steering (CATS)" <https://datatracker.ietf.org/doc/draft-liu-cats-dns-service-discovery/>


