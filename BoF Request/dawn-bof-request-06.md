# Name: Discovery of Agents, Workloads, and Named entities (DAWN)

## Description 

Many distributed processing environments depend on the interaction
between components that do not have pre-configured capability, 
location, or reachability relationships. In order for these systems
to operate correctly, the components must be able to discover each
other. For complete generality, we call these components "entities".
Entities may be tasks, workloads, endpoints, services, AI agents, etc.

In each case, an entity needs knowledge of other entities before 
interaction can proceed: what they are, what they offer, and whether
they can be trusted. Such knowledge could be obtained through static
configuration, but this approach is impractical at scale and across
organisational boundaries. Existing discovery mechanisms, particularly 
those used for service or endpoint discovery, provide only limited
information such as basic identity and reachability. More advanced 
entity discovery use cases may require discovery of richer descriptive
properties such as the tasks an entity is able to undertake, supported
interaction modes and protocols, and lifecycle properties.

An automated and interoperable discovery mechanism is needed that builds
on existing protocols and tools, benefits from established trust models,
supports proven delegation and federation architectures, and allows
organisations to independently publish discovery information.

Providing a decentralised and interoperable discovery mechanism is
essential to protecting the openness of the Internet and protecting
against dominance by a single or a small number of providers. It will
also facilitate interoperability between systems of entities from 
different sources. Integral to this is building a governance system
for the registration of entities.

This BoF seeks to build consensus around establishing a working group
to develop requirements, information models, and protocol solutions for
entity discovery.

## Required Details

   - Status: WG forming
   - Responsible AD: Éric Vynke
   - BOF proponents
      - Adrian Farrel <adrian@olddog.co.uk>
      - Nic Williams <nwilliams@infoblox.com>
      - Roland Schott <Roland.Schott@telekom.de>
      - Laurent Ciavaglia <laurent.ciavaglia@nokia.com>
      - Arashmid Akhavain <arashmid.akhavain@huawei.com>
      - Daniel King daniel@olddog.co.uk
      - Jim Mozley jmozley@infoblox.com
      - Kehan Yao <yaokehan@chinamobile.com>
      - Zaheduzzaman Sarker zaheduzzaman.sarker@nokia.com
      - Hesham Moussa hesham.moussa@huawei.com
   - Number of people expected to attend: 150
   - Length of session: 2 hours
   - Conflicts (whole Areas and/or WGs)
      - Chair Conflicts: TBD
      - Technology Overlap: DNSSD, DNSOP, ACP-BoF, WIMSE, CORE
      - Key Participant Conflict: MPLS, CATS, TEAS, NMRG

## Information for IAB/IESG

To allow evaluation of your proposal, please include the following items:

   - Any protocols or practices that already exist in this space
      - Semi-private AI agent-to-agent ecosystems include forms of discovery such as may be seen in
         - Agent-to-Agent protocol (A2A) from Google
            - See https://a2a-protocol.org/
         - AGNTCY from Cisco
            - See https://agntcy.org/
         - MCP from the Linux Foundation
            - See https://modelcontextprotocol.io/
            - See "Discovery of Model Context Protocol Servers via DNS TXT Records" (draft-morrison-mcp-dns-discovery)
         - ATP from Nankai University
            - See "Agent Transfer Protocol (ATP)" (draft-li-atp)
         - AT protocol (ATPROTO) from Bluesky
            - See https://atproto.com/
      - DNS already performs a similar discovery mechanism and several proposals exist to make it applicable, such as
         - DNS-AID (draft-mozleywilliams-dnsop-dnsaid)
            - See https://dns-aid.org/
         - Agent Identity and Discovery (AID) (draft-nemethi-aid-agent-identity-discovery)
            - See https://agentcommunity.org/
         - DNS-Native AI Agent Naming and Resolution (draft-cui-dns-native-agent-naming-resolution)
         - AgentDNS: A Root Domain Naming System for LLM Agents (draft-liang-agentdns)
      - An alternative to DNS is proposed as
         - Agent Registration and Discovery Protocol (ARDP) from Roberto Pioli
            - See draft-pioli-agent-discovery
   - Which (if any) modifications to existing protocols or practices are required
      - It would be up to the working group to determine what requirements need to be addressed, which protocol(s) form the best starting point, and what extensions are needed
      - Regardless of the solution chosen, a common Information Model will be needed to structure the discovered information
   - Which (if any) entirely new protocols or practices are required
      - See previous answers
   - Open source projects (if any) implementing this work
      - See previous answers

## Agenda

Draft agenda:

   1. Administrivia and purpose of the BoF (Chairs and ADs) [5 : 5/120]
   2. Scene-setting, terminology, and problem statement (Arashmid Akhavain) [15 : 20/120]
   3. Overview of categories of use cases (Kehan Yao) [10 : 30/120]
   4. Solution requirements (Dan King) [10 : 40/120]
   5. Potential solution space (Jim Mozley) [10 : 50/120] 
   6. Draft charter (Jim Mozley) [10 : 60/120]
   7. Open discussion (All) [55 : 115/120]
   8. Wrap-up / Next steps (Chairs and ADs) [5 : 120/120]

## Links to the mailing list, draft charter if any (for WG-forming BoF), relevant Internet-Drafts, etc.

   - Mailing List: https://mailman3.ietf.org/mailman3/lists/dawn.ietf.org/
   - Draft charter: https://github.com/danielkinguk/discovery/tree/main/charter
   - Relevant Internet-Drafts
      - Terminology
         - https://datatracker.ietf.org/doc/draft-farrel-dawn-terminology/
      - Problem Statement
         - https://datatracker.ietf.org/doc/draft-akhavain-moussa-dawn-problem-statement/
         - https://datatracker.ietf.org/doc/draft-mozley-aidiscovery/
      - Requirements
         - https://datatracker.ietf.org/doc/draft-king-dawn-requirements/
      - Privacy Considerations
         - https://datatracker.ietf.org/doc/draft-iannone-dawn-privacy-considerations/
      - Potential Solutions
         - https://datatracker.ietf.org/doc/draft-mozleywilliams-dnsop-dnsaid/
         - https://datatracker.ietf.org/doc/draft-nemethi-aid-agent-identity-discovery
         - https://datatracker.ietf.org/doc/draft-cui-dns-native-agent-naming-resolution
         - https://datatracker.ietf.org/doc/draft-liang-agentdns
         - https://datatracker.ietf.org/doc/draft-pioli-agent-discovery
         - https://datatracker.ietf.org/doc/draft-am-layered-ai-discovery-architecture/
         - https://datatracker.ietf.org/doc/draft-mapmw-task-discovery/
         - https://datatracker.ietf.org/doc/draft-jimenez-agent-directory/
