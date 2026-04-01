# Problem Statement for the Discovery of Agents, Workloads, and Named Entities (DAWN)

## Abstract

   Entities used for AI-based services, such as agents,
   software services, and cloud workloads are proliferating,
   yet there is no standardised way to discover what entities
   exist, what skills and capabilities they offer, or how to
   reach them across organisational boundaries.  Discovery
   today relies on proprietary directories or manual 
   configuration, creating fragmented ecosystems that prevent 
   cross-domain collaboration.

   This document describes the problem space that motivates
   the DAWN work.  It identifies why current approaches are
   insufficient and outlines the challenges a standardised
   discovery mechanism must address.  It does not propose a
   specific solution or protocol.

## Introduction

   Entities increasingly need to find and collaborate with
   other entities.  Entities possess complementary skills and
   capabilities for AI services.  An entity may need to
   locate a specialist agent for data analysis, a translation
   service, or a compute workload or storage capability in a
   specific jurisdiction, all without prior configuration.
   Before any interaction can occur, the discovering entity
   must learn what the remote entity does, how to communicate
   with it, and whether it can be trusted.

   Static configuration is impractical at scale.  As entities
   multiply across organisations, automated discovery of
   entities, their skills, and their capabilities becomes
   essential.

   Communication protocols such as the Agent-to-Agent
   Protocol (A2A) and the Model Context Protocol (MCP) define
   how entities interact once connected, but they do not
   address how entities find each other.  Therefore,
   discovery is a fundamental prerequisite.

   This document describes the problem space and informs the
   development of requirements [draft-king-dawn-requirements]
   and in the future, solution proposals for DAWN.


## Terminology

   The following terms are used in this document.  Full
   definitions are provided in [draft-king-dawn-requirements].

   TBA

## Motivating Scenarios

### Use Case Example

## Functional Requirements and Procedures

### Discovering Entities by Skill or Capability

   An entity needs to find other entities in other
   organisations that possess specific skills.  For example,
   a research assistant agent may need to discover a
   statistical analysis agent or a domain-specific knowledge
   service operated by a partner institution.  Today this
   requires out-of-band coordination or a shared proprietary
   platform.  There is no standardised way to query for
   entities by skill, capability, or domain.

### Discovering Entity Capabilities Before Interaction

   Before delegating a task, an entity must determine what a
   remote entity can do, what protocols it supports, and what
   security guarantees it offers.  Capability cards provide
   this information, but there is no standardised mechanism
   to discover which entities publish capability cards or
   where to retrieve them.

### Cross-Domain Collaboration

   Entities operating across organisational boundaries need
   to discover counterparts without depending on a shared
   registry.  For example, a customer-service agent in one
   organisation may need to find a logistics-tracking agent
   in another.  Current platform-specific registries do not
   interoperate, so entities remain invisible outside their
   own ecosystem.

### Workload and Service Discovery

   Workload orchestrators need to discover compute resources
   or services that satisfy constraints such as jurisdiction,
   hardware capability, or compliance certification.  Cloud-
   provider-specific catalogues do not interoperate across
   providers.

### Broker and Aggregator Discovery

   In large deployments, entities may need to discover
   intermediary brokers that index entities across multiple
   domains and provide dynamic information such as
   availability or routing guidance.

### Human-Initiated Discovery

   Operators need to discover and inspect entities for
   operational purposes: auditing deployed agents, verifying
   capability claims, or troubleshooting failures.  Discovery
   must be usable by humans through standard tooling, not
   only by automated systems.

## Current Approaches and Their Limitations

### Proprietary Directories

   Cloud providers and AI platforms maintain their own
   registries, tightly coupled to their ecosystem.  Entities
   registered in one platform are invisible to another,
   creating walled gardens.

### Static Configuration

   Manually configured endpoint lists cannot scale, cannot
   adapt to dynamic environments, and cannot convey the
   capability and trust metadata needed for cross-domain
   discovery.

### DNS-SD and SRV Records

   TBA

### Well-Known URIs

   TBA

### Ad Hoc Agent Discovery Proposals

   TBA

## Core Challenges

### Discovering Skills and Capabilities at Scale

   The central challenge is enabling entities to discover other
   entities based on what they can do, such as:

   o Agents

   o Skills

   o Capabilities

   o TBA

   A discovery mechanism that supports structured, scalable
   discovery of an entity's capabilities across
   organisational boundaries is therefore required.

### Fragmented Discovery Ecosystem

   Each platform develops its own discovery approach.  This
   fragmentation prevents entities from being discoverable
   across boundaries and limits the value of interoperable
   protocols such as A2A and MCP.

### Trust in Discovery Information

   When discovery crosses organisational boundaries, the
   discovering entity must verify that the information is
   authentic.  Without authenticated discovery, entities are
   vulnerable to poisoning attacks directing them to
   malicious endpoints.  DNSSEC provides a foundation, but
   discovery mechanisms must be designed to use it.

### Scalability and Decentralisation

   Discovery must operate at Internet scale without a single
   centralised registry.  Each organisation must be able to
   publish its entities' capabilities independently,
   mirroring the DNS delegation model.

### Static Versus Dynamic Properties

   Entity properties range from static (type, supported
   protocols, skills) to dynamic (availability, load,
   capacity).  A discovery mechanism must handle both without
   causing stale results or excessive query load.

### Extensibility

   New agent types, skill taxonomies, and capability formats
   will emerge.  Discovery must accommodate them without
   changes to the core mechanism.

## Relationship to Existing Work

## Security Considerations

   This document describes a problem space, not a protocol.

   Discovery information is a high-value target.  Poisoned
   responses could direct entities to malicious endpoints.
   Any mechanism must provide integrity and authenticity
   guarantees.

   Cross-domain discovery raises two distinct trust
   questions: whether the discovery source is authoritative,
   and whether the registered entity is what it claims to
   be.

   Discovery may expose sensitive information about an
   organisation's entities and capabilities.  Selective
   visibility mechanisms are needed.

## Privacy Considerations

   Querying for entities may reveal the discovering entity's
   intentions or interests.  Discovery should minimise
   information leakage through the query process.

   Published entity properties, such as skills, capabilities,
   and organisational affiliations, may be sensitive.
   Entities and their operators should control the
   granularity and audience of published information.

## IANA Considerations

   This document makes no requests of IANA.

## Informative References

## Authors' Addresses

