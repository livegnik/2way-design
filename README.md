# 2WAY

2WAY is a peer-to-peer alternative to the centralized World Wide Web. Rather than simply providing identity and reputation management, it serves as a foundational substrate for decentralized communication, discovery, collaboration, and trust. At its core, 2WAY replaces traditional web servers, social networks, and content repositories with a single composable graph of verifiable data, owned and filtered locally by each participant.

Instead of relying on platforms, 2WAY lets users create, share, and interpret data directly, storing it in a shared trust-based graph where every interaction is signed and every node is under local control. From identities and reputations to marketplaces, feeds, and private communications, everything in 2WAY is managed without intermediaries.

For example, instead of visiting a social platform hosted on a corporate server, a user runs a Social plugin locally. It connects to their own graph and those of trusted peers. Updates appear in a timeline ranked by trust, not algorithms. Instead of publishing on a blog hosted by a platform, the user publishes an Attribute grouped under a Parent. Readers who trust the user can discover and share that object, filtering as they choose. Marketplace listings work the same way. No one approves or moderates them globally. Trust and discovery emerge from graph connections.

Unlike the Web, where data lives on someone else’s server and reputation is dictated by platforms, 2WAY data lives with the user. Trust is earned directly, not inferred by a system. And all logic, from messaging to moderation, can be shaped by the user’s local rules and plugin configurations.

This also leads to significant practical advantages. In a traditional system, each application is siloed. Your social feed, your messenger, your contacts, and your reviews are all managed by different companies. In 2WAY, all applications run on top of a single shared graph. This means a message, a product listing, or a reputation score created in one plugin can be immediately used by another. You do not need to sync accounts or export data. Every object is stored once and shared by reference.

As a result, notifications from different plugins appear in one place. You can see messages, mentions, reviews, edits, and requests together. You can also create hybrid workflows, such as linking a contact’s message history to their marketplace listings, or showing all social posts tagged with an item in your library. The boundaries between applications disappear.

This makes 2WAY not just a tool for self-sovereign identity but a blueprint for a new, decentralized internet. One that puts users in control, supports natural interoperability, and lets trust and discovery evolve from the bottom up.

## Design Principles and System Goals

* **Peer-to-peer architecture**. No servers or platforms are required. Each node can operate independently or in collaboration with others.
* **Graph-based data model**. All data is represented as nodes (Attributes, Parents) and edges between them. This structure accommodates arbitrary schemas and relationships.
* **Trust-by-connection**. Each user builds their own trust network. Reputation is not global but local and contextual.
* **Cryptographic integrity**. Every object is signed. Every message is encrypted. Authenticity is built-in.
* **Modular extensibility**. Plugins and sub-plugins allow specialized behaviors without affecting core infrastructure.
* **Resilience and scalability**. By avoiding global consensus and centralized storage, the system scales naturally with no single point of failure.

## Core Graph Model

Everything in 2WAY exists inside a single directed graph. This graph lives in two layers:

* **Graph in RAM**: Fast and queryable, built with NetworkX.
* **Graph on Disk**: Persistent storage, managed via SQLite.

Synchronization between these layers is handled by the Storage Manager, ensuring the graph is both performant and durable.

This unified structure is known as the **2WAY Graph**, and it represents the full set of objects known to a particular instance of the system. Within this larger graph, there are two conceptual views:

* **User Graph**: The local graph from the perspective of an individual user. It includes their own identity, trust links, and data they are permitted to access based on ACLs. The User Graph is used to build personalized views and determine what to display or act upon.

* **Server Graph**: The union of all User Graphs hosted on a single device or instance. It serves as the local graph database, containing all known Attributes, Parents, Edges, Ratings, and ACLs. The Server Graph is filtered per user into individual User Graphs.

* **2WAY Graph**: A broader term that refers to the complete logical structure that emerges across all peers running 2WAY. There is no global source of truth. Each peer builds and interprets its portion of the graph independently. The 2WAY Graph is an emergent, distributed network of signed and linked objects shared peer to peer.

### Objects in the Graph

There are five primary object types:

* **Attribute**: The smallest unit of information in 2WAY. Each Attribute is a key-value pair, such as `{ "type": "username", "value": "Alice" }`. Attributes can describe names, emails, cryptographic keys, tags, or any other individual data point. They are the atomic elements of the graph and can be rated, linked, or grouped.

* **Parent**: A higher-level node that acts as a container or label for other Attributes. A Parent has no value of its own but instead forms the root of a subgraph by linking to multiple Attributes via Edges. This allows structured data modeling. For example, a Parent could represent a user profile, a product listing, or a document, with Attributes linked as its children. A Parent can also link to one or more other Parent objects, enabling nested hierarchies and more complex structures such as threads, folders, or project trees.

* **Edge**: A directional link that connects a Parent to one or more child Attributes or Parent objects. Edges establish containment or association. They allow 2WAY to express composite structures, like a timeline post containing content, author, and timestamp. Edges preserve the integrity of relationships between objects in the graph.

* **Rating**: An opinion object. A Rating expresses approval, disapproval, or a scalar score about any Attribute or Parent. Each Rating is tied to the signer who issued it and can be interpreted in a localized trust graph. Ratings are stored as relationships, not global values, meaning every user can apply their own interpretation based on who they trust.

* **ACL (Access Control List)**: A set of permissions governing visibility and propagation. ACLs specify which public keys are allowed to view, replicate, or rate a given object. This enforces privacy and security rules directly within the graph structure. ACLs can restrict access to specific users or allow selective sharing based on trust or context.

This model is recursive and composable. Plugins, profiles, messages, assets, or apps all use the same structure. Plugins, profiles, messages, assets, or apps all use the same structure.

### Identity and Reputation

Each user is defined by their cryptographic public key (pubkey), which acts as the root node of their identity. Attributes and Parents branch off from this key. Users do not "own" usernames or emails on a server. Instead, they sign their own data, and others connect to it.

Reputation emerges organically. When one user rates another's Attribute or Parent, that rating exists as a signed object in the graph. You can choose to trust ratings only from your direct connections, or follow the trust paths two or three degrees out. Because the graph encodes these relationships natively, there is no need for a global score.

### Sybil Resistance

To prevent spam and fake identities from gaming the system, 2WAY uses local trust filtering. A user can require that new messages, listings, or posts must originate from known connections or be vouched for by a chain of trust. There are no global bans or algorithmic shadowbans. Trust is personal, verifiable, and filterable.

### Access Control

Unlike traditional file permissions or web servers, access control in 2WAY is embedded in the graph itself. Each object can carry an ACL specifying which pubkeys may read or replicate it. Plugins interpret these rules when traversing the graph, displaying only what is visible to the current user.

Ratings can also be private. A user may rate an object positively without making that rating public. Others can selectively share ratings or reputation data to build trust without broadcasting it.

## Modular Plugin Architecture

2WAY is designed to be minimal at its core and expandable through plugins. A plugin is any module that creates, modifies, or interprets data in the shared graph. Plugins act as frontend applications. They serve as the user interface layer, presenting and manipulating graph data visually and interactively.

However, most of the logic in 2WAY does not reside in these plugins. The actual data handling, graph management, cryptographic operations, access enforcement, and network interaction all happen in the 2WAY backend. This backend is always running on the same local device as the plugin interface. It behaves like a local client-server model where the server is embedded and under user control. The frontend makes requests to the backend, which performs the necessary actions and updates the graph.

Plugins can be standalone or contain sub-plugins. Sub-plugins are switchable modes or methods within a plugin that handle tasks in different ways.

For example:

* A **Library plugin** may offer several sub-plugins. One shows entries in the order they were created. Another filters them by keyword. A third ranks them based on how much you trust the author. Each of these is a different sub-plugin, giving you options for how to explore your graph.

* A **Cryptographic plugin** might support different cryptographic schemes. One sub-plugin may use standard ECDSA signatures. Another might support threshold signatures, where two out of three keys must agree to validate a change. Switching sub-plugins lets you adapt the system to different levels of security.

This approach gives developers and users flexibility. The main plugin provides the interface. The sub-plugins define how it behaves under the hood. There is no need to sync between apps, no duplicative storage, and no format conversion. Data created by one plugin can be reused by another.

### Predefined Plugins

While the user is free to install or create new plugins, the system provides a few defaults:

* **Contacts**: Manage identities and public keys.
* **Messages**: Peer-to-peer, end-to-end encrypted communication.
* **Library**: Search and navigate the graph.
* **Social**: Build a timeline of trusted updates.

Each plugin contributes objects to the graph and interprets graph data for the user. For example, a Social plugin may filter recent messages by trust score or degrees of separation.

## Network Model

2WAY is a local-first system. All operations happen on the user’s machine. For optional peer-to-peer communication, the Network Manager provides a secure, anonymous transport layer:

* **Onion addresses** via Tor
* **Proof-of-work puzzles** to prevent spam and DoS
* **Selective sync** governed by ACLs

Connections are end-to-end encrypted, signed, and filtered. Users only share data they choose to share. There are no public endpoints or discoverable IPs.

The Bastion Engine throttles connection attempts by requiring clients to solve puzzles. The Incoming and Outgoing Engines manage encrypted data flows. The State Engine ensures that only authorized data is synchronized.

## Security and Privacy

2WAY treats security not as a feature but as a default. The system assumes adversarial conditions:

* All shared data must be signed.
* All communications must be encrypted.
* No central authority can be trusted.

This model leads to:

* **Immutable logs**. Events can be signed and stored for auditing.
* **Key rotation and revocation**. Multi-signature schemes allow users to recover from key loss or compromise.
* **Metadata protection**. Onion routing prevents third parties from learning who is communicating.

By decentralizing not just storage but trust and access, 2WAY eliminates the need for gatekeepers.

## Real-World Applications

2WAY is not just a theoretical framework. Its flexible graph structure and plugin model make it suitable for a wide variety of applications:

* **Peer-to-peer marketplaces**
* **Decentralized social networks**
* **Collaborative editing platforms**
* **IoT configuration and management**
* **P2P lending and crowdfunding**
* **Decentralized academic publishing**
* **Reputation-based access control**
* **Federated discovery engines**
* **Trust-minimized file sharing**

Each of these use cases is possible using the same five object types, graph model, and local trust filtering.

A companion document, `2WAY 100 app ideas.md`, explores these in greater detail.

## Summary

2WAY is not just a new way to manage online identity and reputation. It is a new way of building decentralized systems. By replacing static servers and platforms with a locally filtered, cryptographically signed, trust-based and user-centered graph, it enables a new generation of peer-to-peer applications. Its plugin model ensures that it remains flexible. Its privacy defaults ensure it remains secure. And its reliance on real human trust, rather than algorithmic inference or platform control, ensures that it remains humane.

Whether you are building an encrypted messenger, a decentralized marketplace, a collaborative document system, or an anonymous social network, 2WAY gives you the primitives to do it without intermediaries, without surveillance, and without permission.

It is the graph-based, peer-to-peer alternative to the web.
