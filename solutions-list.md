# List of Solutions Relevant to DAWN

This is a working list of solution proposals and related projects that may be relevant to DAWN.

Last reviewed: 2026-06-19 23:14 BST.

The list is intended to show the breadth of current activity and to help DAWN
participants track potentially relevant work. Inclusion is descriptive only. It
does not imply endorsement by the IETF, by any DAWN work effort, or by this
repository.

It is categorised on two axes:
   - IETF I-D exists or work is external to the IETF
   - DNS-based or not

Note that there can be some overlap, e.g.:
   - Work is mainly in an external body, but there is an I-D that describes all or part of it
   - Work assumes some base discovery using DNS, but does most of the solution in a different protocol
   - Work may address functions adjacent to discovery, such as registration, identity, naming, runtime communication, directories, retrieval, or trust resolution

Current Internet-Draft versions, expiry dates, and status should be checked on
the Datatracker before citation.

The order of presentation has no import.

## Proposed solutions in Internet-Drafts

Anyone may submit an I-D to the IETF. These I-Ds are not endorsed by the IETF and have no formal standing in the IETF standards process or within the DAWN work effort.

### DNS-based solutions in Internet-Drafts

   - DNS for AI Discovery (DNS-AID)
        - https://datatracker.ietf.org/doc/draft-mozleywilliams-dnsop-dnsaid/
   - Agent Identity and Discovery (AID)
        - https://datatracker.ietf.org/doc/draft-nemethi-aid-agent-identity-discovery
   - DNS-Native AI Agent Naming and Resolution
        - https://datatracker.ietf.org/doc/draft-cui-dns-native-agent-naming-resolution
   - AgentDNS: A Root Domain Naming System for LLM Agents
        - https://datatracker.ietf.org/doc/draft-liang-agentdns
   - DNS-Based Agent Naming (DAN)
        - https://datatracker.ietf.org/doc/draft-seethiraju-dawn-dan/
   - DNS-based Service Discovery for Computing-Aware Traffic Steering (CATS)
        - https://datatracker.ietf.org/doc/draft-liu-cats-dns-service-discovery/
   - DNS-Anchored Identity Discovery for Autonomous Agents
        - https://datatracker.ietf.org/doc/draft-noss-jeftovic-groundmark-core/
   - Discovery of Model Context Protocol Servers via DNS TXT Records
        - https://datatracker.ietf.org/doc/draft-morrison-mcp-dns-discovery/
   - Agent Transfer Protocol (ATP)
        - https://datatracker.ietf.org/doc/draft-li-atp/
   - DNS-Anchored Durable Identity for AI Agents (DNSid)
        - https://datatracker.ietf.org/doc/draft-ihsanullah-dnsid/
   - Action Reference: A Deterministic Identifier for Agent Actions
        - https://datatracker.ietf.org/doc/draft-etcheverry-action-ref/
   
### Non-DNS solutions in Internet-Drafts

   - Agent Registration and Discovery Protocol (ARDP)
        - https://datatracker.ietf.org/doc/draft-pioli-agent-discovery
   - Agent Directory
        - https://datatracker.ietf.org/doc/draft-jimenez-agent-directory/
   - AGTP Agent Discovery and Name Service
        - https://datatracker.ietf.org/doc/draft-hood-agtp-discovery/
   - ARD Binding for AGTP: Agentic Resource Discovery over the Agent Transfer Protocol
        - https://datatracker.ietf.org/doc/draft-hood-agtp-ard/
   - Agent Discovery Protocol (ADP) v1.1 -- Well-Known Metadata and Interaction Layer
        - https://datatracker.ietf.org/doc/draft-pro-adp-agent-discovery/
   - API Index (APIX): Core Infrastructure for Autonomous Agent Service Discovery
        - https://datatracker.ietf.org/doc/draft-rehfeld-apix-core/
   - API Index (APIX): A Global Discovery Infrastructure for Autonomous Agent Services
        - https://datatracker.ietf.org/doc/draft-rehfeld-bot-service-index/
   - Metadata and Query Profile for Efficient Agent Discovery
        - https://datatracker.ietf.org/doc/draft-xu-efficient-agent-discovery-profile/
   - AI Discovery and Retrieval Endpoint (AIDRE)
        - https://datatracker.ietf.org/doc/draft-batum-aidre/
   - AINS: AInternet Name Service - Agent Discovery and Trust Resolution Protocol
        - https://datatracker.ietf.org/doc/draft-vandemeent-ains-discovery/
   - SD Agent: Selective Disclosure for Agent Discovery and Identity Management
        - https://datatracker.ietf.org/doc/draft-nandakumar-agent-sd-jwt/
          
## Proposed solutions external to the IETF

### DNS-based solutions external to the IETF

   - Agent-to-Agent protocol (A2A) from Google
        - https://a2a-protocol.org/
   - MCP from the Linux Foundation
        - https://modelcontextprotocol.io/
   - AT protocol (ATPROTO) from Bluesky
        - https://atproto.com/

### Non-DNS solutions external to the IETF

   - Agentic Resource Discovery (ARD) from Google/ARDS project
        - https://agenticresourcediscovery.org/
        - https://developers.googleblog.com/announcing-the-agentic-resource-discovery-specification/
   - AGNTCY from Cisco
        - https://agntcy.org/
