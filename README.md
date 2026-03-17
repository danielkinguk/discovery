# Discovery
Discovery

## Terminology 

- Entity: 
- Object: 
- Tasks:
- Jobs:

## Problem Statement 

Many distributed processing environments depend on the interaction between components that do not have pre-configured relationships. In order for these systems to operate correctly, the components must be able to discover each other. For complete generality, we call these components "entites". Entities may be software tasks, services, AI agents, etc.

This discovery is as simple as asking "Find me an entity to talk to." However, there is a lot of detail underlying this question including:
- What functionality do we want an entity to provide for us?
- How do I communicate with that entity?
- Is the information about the entity trustable?

There is a functional layer after discovery that determines which instance of a class of entity should be used. This process may examine location, reachability, load, and operatoinal status. Those pieces of information have to be examinable, but they do not form part of the core discovery function, but may be implemented by a disocvered intermediary aggregation point or broker.

This leads to consider the distinction between mandatory base information which is likely to be static or semi-static, and more dynamic information that could be changing frequently and which is likely to cause scaling and stablity issues for a discovery system.

This work effort seeks to solve the following questions:
- How is an entity classified with respect to its function, origin, location, and type?
- How is an entity communicated with?
- What is the base set of information that is held for each entity?
- How is the information extensible on a per class-of-entity basis?
- Can this problem be solved in a centralised and distributed way?

Issues of the larger architecture of how entities select each other and how they communicate are out of scope. How agents register and authenticate their registration are also how of scope. The solution should work independent of the discovery architecture and the system architecture into which the discovery system sits.

Where possible, any solutions work will be built in a modular way using existing IETF protocols. However, no protocol solution choices will be made until the requirements (functional and behavioral) have been agreed.

## Functional Requirements

- Who discovery 
- What information is being discovered?


Responsiblity
Capability
Tasks
Schema 
