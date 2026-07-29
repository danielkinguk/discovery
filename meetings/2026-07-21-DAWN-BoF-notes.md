# Discovery of Agents, Workloads, and Named entities (DAWN)

Working Group Forming BoF at IETF-126, Vienna, Austria

Tuesday, 21 July 2026
Session III
14:00 - 16:00
Grand Park 3
Chairs
- Wes Hardaker
- Adrian Farrel

AD: Éric Vyncke

Note takers: Muhammad Usama Sardar, Michael Richardson, Brian Trammell, Kehan Yao

## Logistics
Materials: https://datatracker.ietf.org/meeting/126/session/dawn
Note taking: https://notes.ietf.org/notes-ietf-126-dawn
Meetecho: https://meetings.conf.meetecho.com/ietf126/?group=dawn&short=dawn&item=1
Zulip: https://zulip.ietf.org/#narrow/stream/dawn

# Agenda

## 1. Administrivia and purpose of the BoF

- Presenters: Chairs and ADs
- Content: Usual meeting details.
- Purpose and non-purpose of the BoF
- Target: Working Group Forming
- Time: 10 minutes (10/120)

### Bullets

- Chairs present note well and administrative.
- Charter is a starting point; it is not meant to have consensus yet.
- WG-forming BoF
- BoF does not guarantee the creation of a WG
- To have a WG created, a well scoped problem that needs to be solved,
  has a lot of people willing to do the work, and has a high
  probability of success.
- This bof will discuss the problem space only, not solutions.
- During presentations, only short, clarifying questions will be taken.
- The last hour will be available for longer discussions

### Starting questions:

- What should be the focus: AI agents vs entities
- What are the first critical items to solve
- Is this within single organization or Internet-wide
- Is the DNS a starting point?

## 2. Scene-setting, terminology, and problem statement

- Presenter: Arashmid Akhavain (Huawei Canada)
- Content:
- What is the essence of the problem to be solved?
- What are we talking about when we say "entity" and "discovery"?
- References:
    - https://datatracker.ietf.org/doc/draft-farrel-dawn-terminology/
    - https://datatracker.ietf.org/doc/draft-akhavain-moussa-dawn-problem-statement/
- Time: 15 minutes (25/120)

### Presentation

- Terminology and discovery challenges
- A network of AI Entities and discovery of them

- Core Concepts Defined:**
    - Entity:** A participant in the ecosystem (AI agents, tools, workloads, compute nodes, data sources).
    - Discovery:** The process of locating entities exhibiting desired capabilities or properties.
    - Capability:** A description of what an entity can perform (e.g., translation, image generation).
    - Minimum Discoverable Information (MDI):** The baseline data an entity exposes to facilitate discovery.
    - Discovery Substrate:** The underlying infrastructure (like DNS, local registries, or databases) used to publish and retrieve MDI.
- Out of Scope:** AI model behaviors, subsequent post-discovery communication/interaction, entity selection algorithms, authentication, authorization, and orchestration.

### Discussion

- Ekr (chat): "we're going to solve the problem that is really easy
  and seems to map onto DNS but have no plan to solve anything
  difficult."

- Pete Resnick (chat): If MDI includes some interesting
  information, then there (seems to me) actual work that needs to be
  done. If MDI is "an opaque identifier", then EKR's dead right:
  There's not much of difficulty to solve.

- Daniel Kahn Gillmor (DKG) asked for clarification on terms like
  "MDI" (Minimum Discoverable Information) versus "MDR" -- MDR was a
  mis-speak.  Rashmit clarified that MDI represents the baseline
  metadata.
  
- M. Usama Sardar: in AI we have data, model, user. in this picture
  (slide 3), is everything in the diagram an entity? Is user an entity? 
  
    - Arashmid: entity could be any of those.
    - chairs: this is not entirely agreed to yet

- DKG and Eric Rescorla (Ekr) in chat expressed skepticism about how an
  internet-scale capability search (e.g., finding translation
  services) could scale efficiently.

- Linda Dunbar: an entity that contains workload and
  services... what's the difference between these?
    - Arashmid: all of these have a description. that's the MDI. 
    - Lindar: discovering compute, are you doing the whole orchestration in the WG? 
    - Arashmid: no.
    - Linda Dunbar questioned how DAWN avoids overlapping with cloud
      orchestration frameworks (e.g., AWS or Google Cloud compute
      registries). 
    - Rashmit clarified that DAWN aims to enable interoperability
      *across* distinct cloud and administrative domains.

- EKR: Can you give me an example use case.  Is an example who can
  translate french to english?  And if so then I end up with what?
    - Arashmid: agent discovering another agent is the primary use case.

- Ramesh: does this lead to search and semantic search?
    - Arashmid: individual companies have mature search engine.
    - Chairs: we'll get to that question beyond the terminology topic

## 3. Overview of categories of use cases

- Presenter: Kehan Yao (China Mobile) and Frank Brockners (Cisco)
- Content: Broad-brush view of the use cases by category rather than details.
- Reference:
- https://datatracker.ietf.org/doc/draft-kay-dawn-use-cases/
- Time: 15 minutes (40/120)

### Presentation

- Capability-Oriented
- Resource-oriented discovery
- Administrative Scope Extensions
- Operational discovery

- Four Primary proposed Use-Case Categories:**
    1.  *Capability-oriented:* An agent discovering tools (such as chart generators) to help design a slide deck.
    2.  *Resource-oriented:* Finding specific compute/GPU nodes with dynamic attributes (such as current load and availability).
    3.  *Cross-domain/Organizational:* A personal assistant in Company A scheduling a meeting with an assistant in Company B.
    4.  *Natural operations:* Human or system agents locating network fault analysis tools.

### Discussion

- EKR: for the Internet vs. enterprise case you mentioned: are both part of this scope?  Are global, Internet-wide capability queries (e.g., "who on the Internet can translate French to English?") are a realistic requirement or if the focus should be restricted to trusted partners or local namespaces.
    - Chairs: move to scope section in open discussion.

- Hesham: what are the protocols for search exist, and will DAWN solve them all.
    - Kehan: it is likely that multiple groups will need to interact
    - Chairs: it is unlikely we will to pick more than one use case, and that should be discussed later

- Rachid Bouziane: how do you establish trust in this environment?
    - A: trust is a multlayered problem. In DAWN, only MDI trust is in scope

- Usama: Trust is multi-layered as you describe. Who is trusting whom about what is still an open question here.
    - Chairs: yep, big topic we have to pin down.

- Benjamin Schwartz (chat): I think underlying useful thing here is basically "Can anyone here print a PDF?" That seems like a pretty familiar problem, and maybe already solved.  On request, Benjamin provided an example: Principally DNS-SD for IPP, RFC 6763

- Martin Thomson (chat):  this is the question to answer: on what scope is the discovery going to operate?

## 4. Solution requirements

- Presenter: Dan King (Old Dog Consulting)
- Content: What does a solution need to include?
- Reference:
- https://datatracker.ietf.org/doc/draft-king-dawn-requirements/
- Time: 10 minutes (50/120)

### Presentation

Security and Trust: Authenticity, DDOS, Extensibility, Trust 

- The requirements draft aims to classify requirements into entity
  classification, discovery protocol properties, scaling, resilience,
  trust, and security.
- These requirements are just a start and will change as the WG
  progresses.

### Discussion

- Steven: DAWN is a vertical line between the two boxes on the slide 4? 
    - A: yes

- Peter Liu: You mentioned there is no authentication.  Should the
  trust bundle / anchors be considered in scope for DAWN.
    - A: It probably depends on the use case.  It's not clear how
      mandatory it is.

- Usama: slide 8: trust being out of scope does not make much sense,
  if i am discovering agents at Internet scale some might be
  malicious.  Trust should be in scope.
    - A: good point we should consider that.

## 5. What the Community Needs to Decide

- Presenters: Chairs
- Content: High-Level Questions that Need to be Resolved
- Time: 10 minutes (60/120)

Chairs share 4 standard questions and what to focus the feedback on. 

- Éric Vyncke (responsible AD for the BoF): I insist that the narrow
  scope is important to allow for focus and have a succesful WG and
  not boil the ocean.

- Wes: Charter was shared on list already. Scope is probably the main
  dicussion. Out of scope is like future work.

## 6. Charter and WG Scope Discussion

- Presenters: Chairs
- Content: Review of the proposed charter and discussion
- Reference:
- https://github.com/danielkinguk/discovery/blob/main/charter/dawn-charter-02.md
- Time: 55 minutes (115/120)

Chairs showed the charter text and then came down to the scope section for discussion, which would likely have the longest and most important discussion in the room.

### Discussion

- Rachid: I think logically, we need to define trust before defining the
discovery process.

- Linda Dunbar: Will DAWN use the identity defined in WIMSE?
    - Adrian: People should not ask BoF chairs questions. Please just make
      the points you want to make.
    - Arashmid: will reuse whatever mech. identity is important, but
      not part of discovery.

- Yogesh Deshpande: Firstly, will DAWN reuse whatever mechanism that
  it sees fit from IETF to actually solve this problem, including
  identity and other important building blocks. Secondly, the
  importance and relevance should also be taken into account, beyond
  timing.

- Eric Vyncke as AD: For the timing, if we get to September
  discussion, we can get started discussion at IAB and IESG level in
  October and ready to go in November in San Francisco.  It also means
  people will continue to work on draft while we are chartering.  If
  there is discussion everywhere, in March, we are not yet there.

- Toerless Eckert: The only thing I can see that is really of interest
  is all the abilities to collect the database of all the relevant
  stuff, and then have an AI front-end that I can send the
  intelligent, possibly complex discovery questions to. That comes
  from a big database.  No individual discovery protocol, that I'm
  aware of, is going to answer these questions. Pulling the stuff
  together, having the standard data model for all that stuff, I think
  that will be very interesting. But, then I'll use an AI front-end to
  ask the questions to that database.

- Arnaud Taddei: 5 points to bring up about the charter:
   - 1. on Scope: WG should reuse existing trust data models and
     coordinate the structure of this code information with related
     external work from other bodies rather than define new semantics.
   - 2. on deliverables: We need to mention coordination with ITU-T
     SG17 focus group.
   - Milestones discussion
   - Need to add trust frameworks and methods to out of scope
   - Wes: Please send your list of changes to the mailing list. It
     will get too long to read all possible changes at the mic due to
     time constraints.

- Ted Hardie: One thing that works well in the IETF is to figure out
  where proprietary problems exist that can be brought into an
  interoperable context.  If there isn't one, don't put it in a
  charter.  I will say, the current one -- you have an ontology
  problem before everything else.  Don't tackle the ontology problem.
  Find out what is being published by the proprietary people that
  people are using and succeeds and says how to we put this into an
  interoprabble solution and make it something we use.

- Cullen Jennings: Biggest problem of the charter is "within
  collaborating organizations". People have different understanding
  about this.  I'll call it the diameter of the network we're talking
  about working across here before we're really going to be able to
  get to agreement on moving a charter forward. That is the key thing.
    - Wes: and we haven't even talked about in or cross organizations yet.
    - Cullen: or even what's an organization in the first place?

- Jonathan Rosenberg: We should exclude global Internet-wide
  discovery, as its unsolvable. I think it is solvable inside a domain
  and inside an organization, a company, for example, largely defined
  by a trust boundary.  And we have existing work that's been done.
  For example, if you want a directory of agents, looks a lot like
  LDAP or SKIM, we can solve these problems.  This has to be narrowed
  down to be inside a single domain or organization.  Pick agent or
  tool or whatever, not a random entity. Pick one thing.

- Haomian Zhang: Minimum requirements must be clear. AI agents are a
  subset of entities, but not tasks, or workloads etc. The WG could
  start with a specific capability; agents with multiple capabilities
  might be too broad.

- Danny Zollner: Solutions differ for personal, intra‑organizational,
  inter‑organizational, and Internet scenarios – scope is very
  complex.
    - That gets back to defining what an organization is problem

- Aijun Wang: WG should first focus on AI agent discovery. 

- Stephen Farrell: Agree with Ted. But doubts DNS can handle queries
  like finding an MRI – unrealistic.  It would be hard to create a WG
    - Wes: I've mentioned on the list twice now that we need to pick
      one use case.

- Pranyumna Chari: Agree with Ted. I think there is a lot of existing
  work out there in this general space of discovery and DAWN that
  should be taken into account.  One of the use cases I'd like to
  point out is general B2C use cases where not necessarily everyone
  has entities or assets on the same domains and discards and run
  times and how we address discovery across settings like this without
  share and scoping these trust domains out specifically.  Just
  bringing that up for the community to discuss.

- Eric Rescorla: The real question we should be asking is "Are there
  things we should do at all?" There are lots of work in this general
  space, including outside the IETF.  We should be asking whether
  there are already people in this general area that want to
  interoperate things that already exist. Also, Internet scale and
  org-internal are totally different problems. Internet scale is not
  plausible. Should we use dns?  Comically premature question at this
  point.

- Steven Mih: Implementer's view. Lots of those don't have domain
  name. I believe there is a need for a verifiable action record that
  is anchored to a transparent service.  We ran all this at the
  Hackathon last weekend and my charter ask is to consider that
  population with no domain and also, have it composable, such that we
  can reference by digest, the auth as well as the conduct and this
  makes sure that group of people are not second class citizens with
  trust.  My charter ask is to consider entities without a domain (name).

- Jari Arkko: We are stuck behind trying to find a simple thing to do
  easily and approve a charter, and then the needs that many of us
  have for these complex cases.  We should not forget we can already
  do some of the simple things with existing IETF protocols and other
  protocols as well.  What to do?  First off, I think we can actually
  realistically get the scope or scenario to one problem: which is
  where we discover something from a known and trusted other party.
  And I think we should leave the rest out, like random other parties
  on the Internet that others made the point already.  We need three
  things: initial context establishment ("find me the agent..."), a
  directory server with a registry record, and a data format.

- Naveed Ihsanullah: Identity work needs to be carefully considered.
  Many things are assuming identities will remain constant, or will be
  available later. The architecture requirement work should name
  identity and accountability properties that DAWN depends on and say
  whether DAWN owns them or depends on adjacent work and that should
  happen before the protocol work begins.

- Eliot Lear: There are multiple solution spaces here and DAWN
  probably doesn't need to scope down to handle just one of them.  So
  I would leave room for the possibility there will be multiple
  outputs. With so many inputs, it also strikes me that we're going to
  need some time with operational experience to see how these things
  consolidate. Having a common way to evaluate each of these inputs
  might be very useful, and on the scope, what I'm seeing is the
  beginnings of a way to do that evaluation.  So one of the things you
  might want to think about is creating group, saying, have at it. But
  let's evaluate and come up, maybe with some common terminology to
  understand how to evaluate. And then revisit what should be
  standardized later.
    - Wes: typically WGs are short term groups that can accomplish
      work in a short period of time (often 3-5 years).
      Specifications are useless without interoperability of course.

- Dan Druta: Narrow the scope to administrative or
  organizational. We're missing the point about what are the
  requirements.  I think the requirements should come from the
  ecosystems that already implement it and what are their
  interoperability needs.  Rather than boiling the ocean.
    - Wes: the deliverables do have some preliminary things and your
      point is valid that those types of things need to be included.

- Ramesh Raskar: WRT DNS or not DNS: the real question is what's the
  hybrid solution? There is a sub-problem that turns into this working
  group which is when you don't make a DNS anchored, you get a split
  between who maintains the identity, who maintains the metadata like
  agent card, and who maintains the run time. DNS anchored or not DNS
  anchored, maybe a hybrid solution is how to support a split amongst
  those three.

- John Zinky: WRT query by name or query by attributes, if this is
  limited to DNS... the beginning part of the domain name is the scope
  limiting part, and the rest is an explicit agent... or attributes,
  you'll get the agent card. If we limit scope to "name --> agent
  card" + a bunch of other records for rendezvous / negotiation, that
  might be doable.  Then we need to extend the DNS with extra
  information.  We can return other records to extend that "card" to
  return additional information.
    - Wes: we were asked to put DNS into the charter because it's a
      mechanism. I work on the DNS, it can't handle everything that
      DAWN would need to carry as its not designed for bulk transfer.

- M. Usama Sardar: This space not fully explored, there is a need to
  create an RG that can come up to with specific engineering problems
  to send to the IETF. I'm talking to IRTF chair. Many presentations
  here have no related work. A lot of scope problem comes due to not
  looking at the other work in the area.
    - Wes: We warned the ADs they'll need to take the results from
      three BoFs and figure out what to do with it
    - Adrian: The logical and staged approach of working through all
      this denies urgency.

- Sam Betts: maintainer of the (castle) project. There should be a
  split between "making something available to be discovered" and
  "layering on how those things can be discovered". e.g. in DNS,
  that's "making things available", then there are other active
  discovery protocols... You might not have a webserver. You may not
  have a domain. Those will need additional initial-discovery
  mechanisms. Scoping down to just AI agents... we found AI agents and
  tools are the most things that entities want to find today.

- Oscar de Dios: I might be able to advertise some faction of the
  functionality, but I might not be able to use them. Maybe we can
  also include limiting the advertisement of this entity or even some
  cases, hiding the advertisement of some entities depending on the
  user that is connected.  Two cases should be considered: where
  everything is open and is discoverable.

- Hesham Moussa: regarding scoping of what entities we can discover:
  suggest two approaches: find a common denominator across entities,
  or if we can't then pick the most pressing scenarios. I suggest that
  agents, tools, and skills are the most urgent discoverable entities
  we need to start with.

- Roberta Robert: We need to collaborate more.  Everyone wants to be
  heard, and everyone wants to put the flag into the AI thing, but we
  have an opportunity with this group to not let the AI thing get into
  groups that has well‑rounded scopes until we find there groups
  working on something we propose. This group is really good for
  discovery because we have a lot of answers here that we don't have
  the full picture yet.  All hands on deck are needed.  I'm very
  interested to see how security is going to work out.

- Arndt Schwenkschuster: The scope is all about what is discovered,
  but not how.  I suggest that scope focuses on what to discover, and
  let the market solve the data model.

- Shuping Peng: Narrow down the scope and have a clear focus on AI
  Agent. It would be good to start with scenarios that are
  manageable. Whether to use DNS or not depends on scenarios.

- Arshamid: There is a useful existing document on gap analysis, could
  help identify what needs to be done and added. DNS can be part of
  the solution, but not necessarily the whole. A hybrid approach is
  possible. It can be part of the equation. Attaching to the network,
  etc, happens before that point. We need to design a mechanism which
  is easily extensible.

- Leslie: Everyone should read RFC3404 and its related documents (on
  DNS-based dynamic delegation).  That work may be leverage as it
  had many similar problem spaces.

- Rachid: I have some comments about the scope. It would be better if
  we can add some mechanism about entity behavior after discovery.

## 7. Wrap-up / Next steps
- Presenters: Chairs and ADs
- Time: 5 minutes (120/120)

- Wes: We're going to ask our AD to speak in a second. I'll reiterate,
  more discussion on the mailing list about what we agree upon and
  what sort of the next steps would be would be fantastic.  You can go
  back to the message I posted on June 12 or something, asking what is
  the one use case that we want to do?

- Eric Vyncke as AD: My fear is that we air aiming for complexity and
  may try to boil the ocean.  I heard a lot of fair discussion,
  agreement, and also respectful disagreement. That is perfectly
  fine. I'm unsure about the outcome of the BOF and whether we'll be
  chartering something. But I'm way more positive
  now. Interoperability is key, and defining an appropriate trust
  model is also going to be difficult.  Just to be clear, the charter
  said we'll be working with WIMSE and others. In the charter, if you
  look at the phrasing, the chairs have been very careful. It was
  based on an input of mine because in a similar case for the digital
  emblem BOF (diem) and the group, unless and until we set DNS, we are
  going everywhere. Once it was clear to put DNS, it is not DNS. It is
  just a solution.

- Wes: Thank you very much. With that, I think we have a direction. I
  hope the IESG has a good time debating this week.
