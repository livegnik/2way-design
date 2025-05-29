



<br><br>

# 2WAY: Protocol Architecture and Implementation Blueprint

<br><br>

# Table of Contents

<br>

[Introduction](#document-introduction)

<br>

1. [Frontend](#frontend)<br>
  1.1 [Introduction to the Frontend](#11-introduction-to-the-frontend)<br>
  1.2 [Flask](#12-flask)<br>
  1.3 [Plugins](#13-plugins)<br>
  1.4 [Pre-Installed Plugins](#14-pre-installed-plugins)<br>
  1.5 [Custom Plugins](#15-custom-plugins)<br>

<br>

2. [Backend](#backend)<br>
  2.1 [Introduction to the Backend](#21-introduction-to-the-backend)<br>
  2.2 [2WAY Graph](#22-2way-graph)<br>
  2.3 [2WAY Objects](#23-2way-objects)<br>
  2.4 [Database Schema](#24-database-schema)<br>
  2.5 [Graph Manager](#25-graph-manager)<br>
  2.6 [Storage Manager](#26-storage-manager)<br>
  2.7 [Key Manager](#27-key-manager)<br>
  2.8 [Log Manager](#28-log-manager)<br>
  2.9 [Network Manager](#29-network-manager)<br>

<br>

3. [Practical Examples](#practical-examples)

<br>

4. [Conclusion](#document-conclusion)

<br><br><br>

# Introduction <a name="document-introduction"></a>

Centralized identity and reputation systems dominate today's digital landscape, forming the backbone of online interactions. They manage user accounts and assess credibility across users, products, and services, operating much like the algorithms of major platforms. While these systems offer convenience, they introduce significant vulnerabilities and limitations that affect both users and third-party service providers. From privacy breaches to regulatory burdens, centralized systems pose risks to all stakeholders.

For users, these systems often require the disclosure of sensitive personal information to third-party intermediaries. This reliance raises privacy concerns and exposes users to data breaches and unauthorized access. Centralized control also restricts digital freedoms, as these systems remain subject to censorship and unilateral policy changes.

For third-party service providers, managing and securing vast amounts of user data incurs significant costs related to storage, security, and regulatory compliance. As these systems expand, they become more attractive targets for cyberattacks, increasing reputational risks and legal liabilities.

A decentralized approach mitigates these risks by eliminating central intermediaries. Distributing user data across a secure network reduces the likelihood of breaches and unauthorized access. Cryptographic security and decentralized graphs provide transparency and protection, ensuring data integrity without relying on a single authority.

For service providers, decentralization streamlines operations and reduces overhead costs associated with data management and security. By replacing centralized infrastructure with distributed models, organizations lower operational expenses while minimizing large-scale data breach risks. Technologies such as distributed graphs and peer-to-peer (P2P) networks enhance privacy, ease regulatory burdens, and strengthen resilience against cyberattacks.

Decentralization also fosters new business models based on trustless transactions, user-governed ecosystems, and automated contracts. These innovations reduce dependency on intermediaries while creating scalable and lower-risk revenue streams. Instead of competing for control over user data, decentralized applications reinforce one another, improving interoperability. Every tool that integrates with decentralized identity and reputation systems strengthens the entire network, enhancing trust, security, and efficiency for all participants.

A decentralized identity and reputation system also protects against Sybil attacks, a common threat in distributed networks where attackers create multiple fake identities to manipulate trust-based systems. By leveraging cryptographic authentication, decentralized reputation models ensure that credibility is established through verifiable interactions rather than arbitrary identity creation. Reputation scores and trust relationships are built through real-world engagement and cryptographic attestations, making it significantly harder for malicious actors to exploit the system. This approach improves security while preserving user autonomy, allowing networks to remain open and resistant to manipulation without relying on centralized verification authorities.

This shift reduces operational complexity and encourages open innovation, enabling smaller businesses and independent developers to compete without relying on proprietary identity and reputation systems controlled by large platforms. By making identity and reputation portable across networks, decentralization strengthens user autonomy and creates more resilient digital ecosystems.

<br>

Enter 2WAY, a pioneering free and open-source (MIT licensed) proof-of-concept that reimagines electronic identity and reputation management in a fully P2P environment. It empowers users to control their digital identities, manage linked data securely, and communicate directly without intermediaries. By integrating digital signatures, a graph-based structure, and a decentralized P2P network, 2WAY enables users to curate their digital personas, filter relevant information, and engage securely with trusted parties within familiar interfaces.

At its core, 2WAY provides a distributed identity, reputation, and access management system that verifies message authenticity using cryptographic proofs. This decentralized network of trusted servers allows users to exchange data with confidence, ensuring that identities and interactions remain secure through robust cryptographic mechanisms. Since authentication is based on cryptographic signing rather than centralized verification authorities, users retain full control over their identities without relying on external trust providers.

Designed for flexibility, 2WAY supports plugin development, enabling developers to create applications that extend the platform's core functionalities. Plugins interact securely with the 2WAY Graph and existing components, ensuring interoperability while allowing for customized extensions. This modular approach supports a wide range of services, from private communication and content-sharing to decentralized marketplaces and identity verification tools.

Following the principles of privacy by design, 2WAY minimizes the processing of personally identifiable information. Private messages and data are encrypted and shared only with user consent, ensuring confidentiality and security. Public messages can be broadcast on a best-effort basis, but this remains outside the scope of the proof-of-concept.

Because the system does not rely on centralized identity providers, users establish verifiable reputations through cryptographic attestations rather than personal data disclosure. Every interaction within 2WAY generates cryptographic proofs, allowing users to verify identity claims, reputation scores, and transaction history without requiring a central authority.

2WAY is designed to be lightweight, allowing both the frontend and backend to run on a desktop computer. This ensures accessibility while keeping resource requirements low. Unlike traditional web applications that depend on remote servers for data retrieval, all data in 2WAY is stored locally, keeping loading times minimal and interactions responsive. The proof-of-concept merges the frontend and backend into a single Flask-based application, simplifying development and deployment. If the proof-of-concept proves effective, the backend could be implemented as a daemon or service in a low-level language, while the frontend could be developed using any language or framework.

Scalability is achieved through a distributed architecture that uses decentralized graphs and P2P networks to distribute workloads across multiple servers. This allows horizontal scaling by adding more servers to meet increasing demand without reducing performance. The Network Manager synchronizes data efficiently, while the Storage Manager optimizes retrieval to maintain responsiveness under growing workloads. Since all data is stored locally on each user’s device, 2WAY provides instant access to identity and reputation data, ensuring users do not experience delays associated with centralized infrastructure.

2WAY also supports offline functionality, allowing users to access stored data without an active network connection. Updates synchronize automatically upon reconnection, ensuring continuity in identity management and messaging, even when network access is intermittent.

To enhance usability, 2WAY prioritizes a user-friendly design with clear and intuitive interfaces for digital identity and data management. By reducing the need for technical expertise, these interfaces encourage broader adoption and engagement. The system consolidates notifications, logs, and updates into a unified interface, ensuring users can track identity changes, messages, and interactions seamlessly.

<br>

This document provides a detailed exploration of the 2WAY system, covering its architecture, functionality, and real-world applications. It begins with an in-depth look at the frontend, explaining how the Flask framework supports the proof-of-concept and how plugins, both pre-installed and custom, extend the 2WAY protocol’s capabilities. The document explores how these plugins interact with the 2WAY Graph, enforce access control, and support real-time data synchronization.

The backend section introduces the core components of the 2WAY Graph, including Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs) objects. It describes the Database Schema and key backend components, such as the Graph Manager, Storage Manager, Network Manager, Log Manager, and Key Manager. These components work together to maintain system integrity, enforce cryptographic security, and enable decentralized identity management. The document also covers the decentralized network structure, secure communication protocols, and privacy-preserving mechanisms that ensure verifiable and tamper-resistant interactions.

Beyond technical architecture, this document explores 2WAY’s practical applications, such as managing contacts and messages, securing communications, preventing Sybil attacks, and enabling decentralized markets. It details identity verification, reputation tracking, P2P reputation systems, and cryptographic techniques like zero-knowledge proofs. Additional applications include decentralized finance, collaborative document editing, event ticketing, and access control systems. The effectiveness of the 2WAY network follows Metcalfe’s Law, where its value grows exponentially as more participants join, strengthening decentralized trust and authentication.

To ensure usability and adoption, 2WAY prioritizes an intuitive user experience with clear interfaces for managing identity, permissions, and data. The system consolidates notifications, logs, and status updates, ensuring users can track interactions efficiently. Real-time updates, secured by cryptographic authentication and WebSocket synchronization, keep interactions instant and verifiable. 2WAY also functions offline, synchronizing changes upon reconnection, ensuring continuity in identity management and messaging.

In summary, 2WAY introduces a decentralized approach to electronic identity and reputation management, eliminating reliance on centralized authorities while enhancing security, privacy, and user control. By removing third-party intermediaries, it reduces risks and operational costs associated with securing user data. This proof-of-concept demonstrates the feasibility of running both frontend and backend on a single desktop computer, leveraging Flask for an integrated and scalable experience. With its extensible plugin architecture, 2WAY provides a foundation for developers to build applications that support decentralized identities, trust-based interactions, and resilient digital ecosystems.

This document serves as a guide to understanding the inner workings of 2WAY and its potential to redefine how digital identities, reputation, and secure communications are managed in a decentralized world.

<br><br>

# 1. Frontend <a name="frontend"></a>

<br>

## 1.1 Introduction to the Frontend <a name="11-introduction-to-the-frontend"></a>

The 2WAY frontend serves as the primary interface for users to interact with its decentralized data structure. It provides a gateway for managing objects, relationships, and access controls, enabling dynamic data representation without reliance on a central authority. Unlike traditional applications that store data in isolated databases or predefined categories, 2WAY allows users to define and interact with objects flexibly, whether they represent people, digital assets, social connections, documents, or other entities.

As the proof-of-concept is built on the Flask framework, the frontend offers an extensible environment for interacting with the 2WAY system. Users can create, modify, and retrieve objects in a way that mirrors real-world relationships while remaining adaptable to various applications, from peer-to-peer communication and content sharing to decentralized reputation systems and marketplaces. Instead of enforcing a fixed schema, 2WAY enables users to establish objects and attributes dynamically, linking them in meaningful ways.

A key feature of the frontend is its plugin system, allowing users and developers to extend functionality seamlessly. Pre-installed plugins provide essential capabilities such as structured search, communication, and data organization, while custom plugins can leverage core 2WAY functionalities to build diverse applications. This modular approach ensures flexibility across different use cases.

The frontend also facilitates inter-plugin data access, allowing plugins to securely retrieve and combine information using Access Control Lists (ACLs). This enhances interoperability, ensuring that objects and relationships can be shared across functionalities. Instead of applications operating in isolation, users can interact with a unified, decentralized dataset where relationships between objects are as important as the objects themselves.

To improve usability, the frontend consolidates notifications, logs, and updates into a single interface. Users can track object changes, monitor updates from trusted sources, and review interactions across plugins without navigating between fragmented applications. Whether managing structured data, engaging in discussions, or tracking reputational shifts, the system provides clear insights into information flow within the decentralized network.

Among the pre-installed plugins:

- The Contacts plugin organizes objects representing people, systems, or other networked entities, providing an intuitive way to manage connections and trust relationships
- The Messages plugin enables secure, peer-to-peer communication between connected objects, ensuring private and verifiable interactions
- The Social plugin aggregates updates across the network, allowing users to see messages and content changes based on actual connections and trust levels rather than centralized algorithmic filtering
- The Market plugin facilitates peer-to-peer transactions, allowing users to list, discover, and exchange goods and services within a trust-based network
- The Library plugin serves as a universal search and filtering tool, leveraging the decentralized graph structure to locate objects based on relationships and degrees of separation

By running both the frontend and backend locally, 2WAY eliminates dependence on external infrastructure while improving responsiveness, security, and privacy. All operations occur on the user's device rather than a remote server, reducing latency and ensuring that users retain full control over their data and interactions.

Designed for flexibility and scalability, the 2WAY frontend provides a powerful, user-driven interface for working with decentralized data. Its plugin-based architecture, seamless cross-application data access, and robust querying capabilities make it a versatile tool for managing any type of object or relationship. Through its structured yet adaptable design, it empowers users to interact with digital information on their own terms, free from the constraints of centralized control.

<br>

## 1.2 Flask <a name="12-flask"></a>

Flask serves as the cornerstone of the 2WAY system's architecture, offering a versatile and lightweight framework for web application development. Traditionally used for backend development, Flask is uniquely employed in the 2WAY proof-of-concept to power both the server-side components and the client-side user interface. This approach merges the frontend and backend into a cohesive unit, simplifying development and deployment while promoting code reusability and maintainability. While Flask is used in this proof-of-concept to demonstrate the 2WAY protocol’s architecture, future implementations could adopt different languages or frameworks depending on performance requirements, deployment environments, or developer preferences. This setup enables 2WAY to function as a self-contained application, where both the frontend and backend run within a single process, reducing resource overhead and streamlining deployment.

By handling both frontend and backend operations, Flask ensures seamless communication between the user interface and server infrastructure. Its intuitive syntax and extensive ecosystem of extensions empower developers to create responsive, dynamic, and feature-rich web applications. Key extensions such as Flask-RESTful for structured API endpoints and Flask-WTF for form handling contribute to system robustness and flexibility. Flask-RESTful enables smooth interactions between the frontend and backend, particularly for querying and modifying the 2WAY Graph.

In the context of the 2WAY protocol, Flask’s lightweight nature is particularly relevant for supporting decentralized identity, reputation, and access management. By leveraging Flask’s capabilities, developers can ensure that the frontend experience integrates seamlessly with backend services, providing a cohesive and intuitive interface. For real-time data exchange, Flask is extended with WebSocket capabilities to provide instant updates for notifications, messaging, and other dynamic interactions. This includes system-wide feeds such as notifications and logs, ensuring a unified and responsive user experience across all plugins.

Flask’s flexible routing and middleware support efficiently manage both frontend and backend functionalities, ensuring smooth navigation and interaction. Rather than relying on Flask’s session management, 2WAY handles authentication and access control using cryptographic key pairs and decentralized trust mechanisms. Users sign messages with their private keys, while Access Control Lists (ACLs) enforce permissions, ensuring secure, trust-based interactions without centralized authentication.

Flask’s support for template rendering and dynamic content generation enhances interactive user interface development within 2WAY, enabling personalized experiences while maintaining flexibility in content presentation. Unlike traditional Flask applications that use Flask-SQLAlchemy for database interactions, 2WAY delegates all SQL query execution to the Storage Manager’s Storage Engine. This design centralizes data handling, ensuring efficient and consistent query execution across the system while maintaining Flask’s lightweight nature.

Flask’s modular design aligns with 2WAY’s plugin-based architecture, allowing developers to extend functionality by integrating custom plugins that interact with the system's API.

Overall, Flask’s simplicity, flexibility, and scalability make it an ideal choice for 2WAY’s unified architecture. By leveraging Flask, developers can build a powerful and user-centric platform that meets the requirements of decentralized identity management, reputation tracking, and access control while maintaining efficiency and adaptability.

<br>

## 1.3 Plugins <a name="13-plugins"></a>

Plugins in 2WAY extend the system’s core functionality, demonstrating how applications operate on top of the 2WAY protocol. The terms plugin and application are used interchangeably, as each plugin functions as an independent application that interacts with the system’s decentralized infrastructure. Plugins provide a flexible framework for integrating various services, enhancing user interactions, and leveraging 2WAY’s decentralized architecture.

Flask-based plugins streamline communication with the backend Graph Manager, enabling efficient data handling and synchronization. Operating within the Flask framework, plugins ensure modular and scalable management of user interactions. By integrating with the Graph Manager, plugins facilitate real-time updates and seamless data exchange between the frontend and backend.

The Graph Manager processes plugin-generated requests, handling object creation, retrieval, modification, and query execution. Plugins interact with the 2WAY Graph to manage structured data, enforce permissions, and execute complex queries. This includes creating and retrieving objects, defining relationships, and applying Access Control Lists (ACLs) to regulate access. Some plugins may define their own ACLs to manage permissions for their specific objects, ensuring that only authorized users can view or modify data.

All plugin actions run through the Graph Manager, which acts as the central interface between plugins and the 2WAY system’s data structure. The Graph Manager ensures consistency, integrity, and adherence to decentralized access control policies. While plugins request operations such as creating, retrieving, or modifying objects, the Graph Manager executes these requests, optimizing query performance and enforcing validation. Plugin developers do not manage database operations manually, as the Storage Manager handles all data persistence and retrieval, allowing developers to focus on application logic rather than low-level data management.

Each plugin operates with its own cryptographic key-pair, ensuring that all actions are securely authenticated, similar to user and server interactions. The Key Manager facilitates key generation and management, treating each plugin as a unique entity within the 2WAY Graph. This cryptographic model guarantees message integrity and prevents unauthorized modifications.

Plugins function as users within the system, allowing them to create and manage objects and define permissions through ACLs just like human users. The Graph Manager enforces access control based on the plugin’s assigned key, ensuring that only authorized plugins can modify specific objects. While not all plugin actions require cryptographic signing, their unique key-pairs ensure that every interaction is properly attributed and governed by the same permission rules applied to users in the 2WAY ecosystem.

Beyond standard operations, plugins facilitate inter-plugin data access. They can retrieve and combine information from different sources, allowing greater interoperability across applications. This ensures that structured data remains accessible and reusable across multiple plugins without duplication.

Pre-installed plugins provide essential system functions, including:

- The Contacts plugin for organizing networked entities and enabling trust-based interactions
- The Messages plugin for secure, peer-to-peer communication between connected objects
- The Social plugin for aggregating updates based on trust relationships rather than centralized algorithmic feeds
- The Market plugin for facilitating peer-to-peer transactions, allowing users to list, discover, and exchange goods and services within a trust-based network
- The Library plugin for structured search and filtering, leveraging the 2WAY Graph to efficiently locate and explore objects

In addition to these core plugins, developers can create custom applications tailored to specific use cases, such as marketplaces, identity verification tools, decentralized finance applications, and reputation-based services. Since plugins operate within the system’s modular architecture, they remain compatible with core functionalities while enabling a wide range of decentralized applications.

To support real-time interactions, plugins can integrate with the system-wide event system, allowing notifications, logs, and status updates to be consolidated into a unified feed. This enhances user experience by ensuring that plugin-generated events are easily accessible across different parts of the 2WAY system.

Overall, plugins are fundamental to 2WAY’s extensibility. They facilitate efficient communication, data exchange, and application development within a decentralized environment. By leveraging Flask’s flexibility and 2WAY’s structured graph-based framework, plugins empower developers to build feature-rich applications that seamlessly integrate with the 2WAY protocol while maintaining security, scalability, and a cohesive user experience.

<br>

## 1.4 Pre-Installed Plugins <a name="14-pre-installed-plugins"></a>

The 2WAY system includes several pre-installed plugins that provide essential functionality and enhance the user experience. These plugins integrate seamlessly with backend services, leveraging the 2WAY Graph for structured data management, secure interactions, and efficient information retrieval. Each plugin operates within the decentralized ecosystem, ensuring interoperability and extensibility while maintaining cryptographic integrity and access control.

The Contacts plugin acts as an address book, allowing users to manage and organize network connections. It structures contacts as objects in the 2WAY Graph, enabling users to navigate relationships, establish trust, and interact securely. Contacts can represent people, systems, automated agents, or any other networked entity. The plugin also supports filtering based on trust levels and degrees of separation, helping users prioritize meaningful interactions while maintaining verifiable, decentralized relationships. Contacts are integrated with other plugins, allowing seamless use in messaging, reputation tracking, and marketplace interactions.

The Messages plugin extends the Contacts plugin by enabling secure, peer-to-peer communication. Messages are authenticated using cryptographic verification, ensuring private and tamper-proof exchanges. Since message relationships are stored within the 2WAY Graph, they can be queried and integrated with other structured data. The plugin supports offline messaging by queuing messages when a recipient is unavailable and delivering them once a connection is re-established. It also interacts with the Social plugin by allowing message-based interactions to appear in the decentralized feed, enhancing visibility within a user’s trusted network.

The Social plugin aggregates updates from the user’s network, providing a decentralized alternative to traditional social feeds. Instead of relying on algorithmic filtering, updates appear based on direct relationships and trust levels. The plugin integrates with the Contacts and Messages plugins to display relevant interactions, including messages, status updates, and system notifications. Since visibility is determined by user-defined trust relationships, content propagation is fully decentralized and user-controlled. The Social plugin also interacts with the Market plugin by displaying transaction confirmations, trust updates, and other marketplace-related interactions within the feed.

The Market plugin enables peer-to-peer commerce by allowing users to create, browse, and participate in decentralized transactions. Unlike traditional marketplaces, where listings are public, the Market plugin operates on a trust-based model. Users only see listings from contacts within their 2WAY Graph or from entities they have explicitly approved. Transactions are private, and reputation is built through direct interactions rather than centralized rating systems. The plugin integrates with the Library for searching listings and with Contacts to manage trust-based visibility. Future expansions may include escrow mechanisms, automated contract execution, and decentralized dispute resolution. Market transactions are logged within the 2WAY Graph, ensuring cryptographic verification and historical consistency.

The Library plugin provides universal search and filtering capabilities, allowing users to locate and explore objects across different plugins. It leverages graph-based relationships to offer context-aware data retrieval, enabling users to search for specific data points, discover linked objects, and query large datasets efficiently. The plugin supports structured queries across all plugin-generated objects, ensuring interoperability and seamless information retrieval. Developers can extend the Library plugin by defining custom search parameters, integrating specialized filters, or enabling cross-plugin data visualization for complex relationships.

Pre-installed plugins are designed to work together, ensuring a seamless user experience through structured data exchange and integrated querying. Contacts improve identity management for messaging, the Library enables system-wide search across plugin-generated objects, and the Social plugin consolidates relevant updates. The Market plugin extends functionality by introducing a decentralized commerce layer. Plugin actions generate system-wide events, contributing to notifications and logs that create a unified interface for tracking interactions. WebSocket integration enables real-time updates for messaging, social interactions, and system-wide notifications.

Each plugin adheres to Access Control Lists (ACLs) to maintain security and privacy, ensuring that only authorized users can interact with specific data. Since all plugin interactions run through the Graph Manager, access permissions are consistently enforced, and all changes remain cryptographically verifiable. The Key Manager authenticates plugin actions using cryptographic key-pairs, ensuring that only legitimate plugins can perform operations within the system.

Beyond their core functions, pre-installed plugins provide a foundation for developers to extend or modify. Custom applications can integrate additional capabilities, such as encrypted file sharing within Messages, group-based social interactions in Social, or advanced search parameters in Library. Developers can also create entirely new plugins that leverage existing functionalities while introducing features tailored to specific use cases.

The system operates in both online and offline modes, allowing users to interact with pre-installed plugins even when disconnected. Data is stored locally and synchronized with the network when a connection is restored, ensuring that messages, contacts, and updates remain consistent across devices. The Storage Manager ensures data persistence while optimizing storage efficiency, allowing seamless offline interactions without compromising system integrity.

Future enhancements may introduce additional pre-installed plugins, including decentralized reputation tracking, encrypted voice or video messaging, and expanded marketplace functionalities. These extensions will maintain compatibility with the 2WAY Graph while expanding the system’s capabilities in a decentralized and secure manner.

Pre-installed plugins form the backbone of the 2WAY platform, providing essential services while ensuring flexibility for future development and customization. By integrating seamlessly with the 2WAY Graph and backend services, they facilitate structured, efficient, and user-controlled interactions in a decentralized ecosystem.

<br>

## 1.5 Custom Plugins <a name="15-custom-plugins"></a>

Beyond the default functionality provided by pre-installed plugins, the 2WAY system supports custom plugins, enabling developers to extend the platform’s capabilities and tailor the user experience to specific needs. Custom plugins allow developers to introduce new features, integrate third-party services, and modify the frontend interface according to user requirements while maintaining compatibility with the 2WAY Graph and access control mechanisms.

Built using the Flask framework, custom plugins can leverage Flask extensions and libraries to streamline development. This flexibility allows developers to create a wide range of plugins, from specialized communication tools to advanced data visualization and analytics. Since 2WAY handles all database operations through the Storage Manager and Graph Manager, developers do not need to manage raw SQL queries, ensuring data consistency and security across plugins.

One common use case for custom plugins is integrating external services or APIs. Developers might create plugins that connect with social media platforms, enabling users to share content, import contacts, or interact with external communities. Other potential integrations include secure identity verification systems, decentralized finance applications, or encrypted file storage services. These plugins interact with Access Control Lists (ACLs) to enforce security policies, ensuring users retain full control over their data.

Custom plugins can also be designed for specific industries, providing solutions for niche markets or specialized user groups. Examples include project management tools, customer relationship management (CRM) systems, supply chain tracking, and e-commerce solutions. Inter-plugin communication enables seamless integration between different functionalities, allowing custom plugins to work together with pre-installed ones. A CRM plugin, for example, could leverage the Contacts plugin for managing customer interactions or the Messages plugin for automated follow-ups.

Custom plugins can retrieve and combine data across different plugins using structured queries within the 2WAY Graph, ensuring interoperability without data duplication. This allows, for example, a marketplace plugin to integrate seamlessly with a reputation tracking plugin to display verified seller ratings. Developers can define structured relationships between plugins to enable complex interactions, such as linking social verification data to user profiles or embedding transaction history within decentralized applications.

Additionally, custom plugins can enhance user engagement by introducing gamification elements, personalized experiences, or advanced collaboration features. They can generate system-wide events that appear in notifications and logs, ensuring that users stay informed about relevant interactions. WebSocket integration enables real-time updates, allowing custom plugins to provide live data feeds, interactive dashboards, or instant messaging services.

Like pre-installed plugins, custom plugins can function in offline mode by caching data locally and synchronizing changes with the network once reconnected. The Graph Manager ensures that updates to the 2WAY Graph are processed correctly, enforcing access controls and maintaining data integrity. Once reconnected, the Network Manager handles synchronization to ensure consistency across devices and peers. This allows messaging, contact management, and other plugin-driven activities to remain accessible even when the system is temporarily offline.

Each custom plugin operates with its own cryptographic key-pair, ensuring that all interactions remain verifiable and secure within the 2WAY ecosystem. The Key Manager facilitates key generation and signing, allowing plugins to authenticate their actions and ensuring data integrity. Since plugins are treated as independent entities in the 2WAY Graph, they can define access policies using ACLs. The Graph Manager enforces these policies, ensuring that data visibility and modification permissions follow the system’s decentralized trust model.

Proper error handling mechanisms ensure that custom plugins operate smoothly, preventing disruptions to the overall system. Developers can also extend the Library plugin to define custom search filters, allowing users to retrieve structured data more efficiently across various applications.

Future enhancements may introduce a plugin repository or decentralized distribution system, allowing users to discover and install verified plugins that extend 2WAY’s capabilities while maintaining system security. This would provide a streamlined way for developers to share new plugins and for users to expand their system’s functionality without compromising decentralization or control over data access.

Custom plugins significantly enhance the flexibility and extensibility of the 2WAY platform. They allow developers to build applications tailored to unique user needs while maintaining security, interoperability, and compliance with the decentralized trust model. By supporting custom plugin development, 2WAY fosters innovation and expands the possibilities for decentralized applications, creating a robust and adaptable ecosystem.

<br><br>

# 2. Backend <a name="backend"></a>

<br>

## 2.1 Introduction to the Backend <a name="21-introduction-to-the-backend"></a>

The backend of the 2WAY system forms the foundation of its decentralized identity, reputation, and access management framework. It is designed to handle the complex operations required to maintain security, efficiency, and reliability across the 2WAY ecosystem. This infrastructure manages the creation, storage, and verification of all objects within the system, including digital identities, relationships, reputation scores, and application-generated data. It maintains structured connections between objects, enforces access control policies, and processes cryptographic attestations to ensure integrity and trust in a decentralized environment. By overseeing the full lifecycle of objects within the 2WAY Graph, the backend provides a scalable and tamper-resistant foundation for decentralized applications, secure interactions, and trust-based systems.

At the core of the backend is the 2WAY Graph, a structured data model that integrates both the User Graphs and the Server Graph. The User Graph represents individual user interactions, while the Server Graph aggregates all User Graphs on a particular server, encapsulating a subset of the network’s decentralized data. The Network Manager ensures that the 2WAY Graph remains consistent across decentralized nodes by synchronizing graph updates with trusted servers. Conflict resolution mechanisms ensure that replicated data remains accurate while preserving cryptographic integrity. This prevents data fragmentation and ensures that reputation scores and trust relationships are updated across the network without requiring a centralized authority.

The backend manages essential 2WAY Objects, including Attributes, Parents, Edges, Ratings, and Access Control Lists. Attributes are key-value pairs that store structured data. Ratings represent reputation scores and adjust dynamically based on verified interactions. Parents establish hierarchical relationships by linking to one or more child Attributes, enabling structured data organization. Edges define the relationships between Parents and their child objects, forming the foundation of trust and identity connections. Access Control Lists enforce security policies, ensuring that only authorized entities can view or modify specific data. Each object can be upvoted or downvoted indefinitely, affecting its relevance and visibility within the graph from the user's perspective.

Several critical components ensure the functionality and security of the 2WAY backend. The Database Schema defines how data is structured and organized, ensuring efficient access and retrieval. The Graph Manager processes incoming messages from the frontend, backend, or connected applications, handling updates to the 2WAY Graph and maintaining an active version of the graph in RAM. It ensures that all changes are securely processed and validated, while the Storage Manager persists the graph to disk, safeguarding data integrity across sessions.

The Key Manager is fundamental to 2WAY’s trust model, ensuring that all messages, identity claims, and transactions are signed and verifiable. It prevents identity spoofing by enforcing public key authentication and ensures that secure messaging and server-to-server communications remain cryptographically protected. The Network Manager facilitates P2P connectivity by tracking synchronized data between servers, managing pending synchronization, and implementing defenses against Denial of Service attacks. It dynamically adjusts proof-of-work-based client-puzzle challenges to regulate incoming network requests, mitigating the risk of resource exhaustion attacks while preserving system availability.

Additional components contribute to system resilience and operational efficiency. The Log Manager records system activities for auditing and debugging, providing an immutable history of actions performed within the network. Logs serve as an immutable record of system interactions, ensuring accountability and enabling forensic analysis in the event of a security breach. Cryptographically signed log entries allow nodes to verify past actions, maintaining a transparent yet privacy-preserving audit trail. The Installation Wizard and Startup Managers streamline the deployment and initialization process, ensuring that the system is properly configured and ready for use from the moment it is launched.

The backend supports offline functionality by allowing users to interact with locally stored data when disconnected. The Network Manager queues pending transactions and updates, applying them once a connection is re-established. This ensures that identity records, reputation scores, and access control updates remain accurate across all nodes, even in low-connectivity environments. As the system scales, optimizations in data indexing, graph traversal, and caching strategies will enhance performance across high-volume networks. Future updates may introduce adaptive storage techniques that balance real-time querying with efficient long-term data persistence.

The 2WAY backend is a modular and scalable infrastructure designed to support a secure and decentralized identity ecosystem. By integrating cryptographic verification, access controls, and a structured data model, it provides a resilient framework for managing digital identities, trust relationships, and reputation in a P2P environment. This section details each component, offering a comprehensive understanding of the backend architecture and its role in maintaining security, integrity, and efficiency within the 2WAY system.

<br>

## 2.2 2WAY Graph <a name="22-2way-graph"></a>

### 2.2.1 Introduction to the 2WAY Graph

The 2WAY Graph lies at the core of the 2WAY system, serving as a dynamic and interconnected framework for representing and organizing data. It functions as the backbone of decentralized identity, reputation, and access management, enabling seamless interactions across a peer-to-peer network.

At its essence, the 2WAY Graph is a directed graph-based data model that represents relationships and interactions between various entities. Nodes store objects such as Attributes, Parents, Ratings, and Access Control Lists (ACLs), while Edge objects define structured connections between Parent objects and their child Attributes, forming the foundation of trust relationships and access control structures. The graph enables flexible object creation and modification, ensuring that relationships between entities remain verifiable, traceable, and structured according to predefined access policies.

Each server maintains a localized subset of the 2WAY Graph, known as the Server Graph, which aggregates and synchronizes user-generated data while ensuring consistency across the decentralized network. This structure enables efficient data management and keeps reputation scores, access controls, and object relationships updated across trusted peers without requiring centralized coordination. The Network Manager facilitates synchronization by exchanging graph updates, preventing data fragmentation while preserving structural integrity.

The 2WAY Graph is decentralized and distributed, allowing users to create, share, and interact with data in a scalable and tamper-resistant manner. ACLs define permissions at the graph level, enforcing constraints on object visibility and modification rights. The 2WAY Graph applies these permissions dynamically, ensuring that only authorized entities can traverse or alter specific relationships. This permission model provides granular access control without requiring a centralized authentication system.

Parent objects define hierarchical relationships by linking to one or more child Attributes, allowing structured data organization within the graph. These relationships can establish access control inheritance, ensuring that permissions applied at the Parent level propagate to dependent objects where explicitly configured. Since any child Attribute can also function as a Parent object, the system supports multi-level nesting, enabling deeply structured hierarchies. This recursive relationship allows complex data models where objects can inherit permissions, link multiple related entities, and dynamically expand based on evolving graph structures. By leveraging this flexible architecture, the 2WAY Graph supports intricate access control mechanisms, scalable trust structures, and layered identity or reputation models without requiring a rigid schema.

The graph structure supports time-stamped event tracking, enabling historical analysis of identity interactions, reputation changes, and trust relationships. Some actions, such as identity attestations and key updates, are cryptographically signed to ensure verifiable records, while other updates follow predefined trust policies within the network. Logged events are managed by the Log Manager, ensuring historical records remain accessible and tamper-resistant for auditing and data integrity verification.

Before transmission, object packages are cryptographically signed by the sender and encrypted for the intended recipient, ensuring authenticity, confidentiality, and protection against unauthorized modifications. Upon receipt, the system verifies the package signature against the 2WAY Graph before applying updates. This process ensures that only authorized changes are integrated while maintaining security and consistency across the decentralized network.

By handling signing, encryption, and verification at the protocol level, the Key Manager secures graph updates and communications without imposing unnecessary cryptographic overhead on all operations. Instead of requiring every user interaction to be cryptographically signed, the system prioritizes signing for critical actions, such as identity attestations, key updates, and object package transmissions. Other updates are verified against the 2WAY Graph to ensure consistency and authenticity while maintaining efficiency. However, actions can be signed and logged if the plugin is configured to allow it, supporting not only enhanced security but also debugging, auditing, and the ability to verify past graph states based on recorded event history.

The 2WAY Graph is not a static structure but continuously evolves as new objects are created, relationships are modified, and reputation scores update based on interactions. These changes are incorporated into the graph while ensuring backward traceability and data integrity. To maintain consistency across the decentralized network, the 2WAY Graph employs structured synchronization mechanisms. Servers exchange graph updates securely, ensuring that distributed nodes remain aligned while preventing unauthorized modifications.

To maximize efficiency, the Graph Manager maintains an active subset of the 2WAY Graph in RAM, storing only the IDs of pubkey Attributes in the proof-of-concept while reducing reliance on disk operations for other data. The Storage Manager ensures data integrity by persisting graph updates to disk, preserving data across sessions while enabling queries to retrieve inactive objects when needed. While the proof-of-concept keeps RAM usage minimal, future implementations could expand the Graph in RAM by caching frequently accessed objects, preloading related data for faster lookups, or storing additional metadata to optimize query performance. These enhancements could improve efficiency for complex graph traversals and high-throughput environments. This RAM-based architecture allows the system to operate using a single database schema shared across all applications and plugins, ensuring seamless interoperability between decentralized applications while maintaining a unified storage model.

By keeping an active subset of the graph in RAM while persisting data in a traditional relational database instead of a dedicated graph database, 2WAY remains lightweight and efficient. This approach enables fast traversal and query execution without the complexity and overhead of specialized graph database systems, ensuring low-latency access while benefiting from the simplicity and portability of relational storage. SQLite3 serves as the database engine for the proof-of-concept, allowing 2WAY to function as an embedded system across a wide range of devices without requiring complex setup or additional dependencies. To further enhance performance, 2WAY employs indexing strategies and structured query optimizations, reducing computational overhead while maintaining efficient access to large datasets. These optimizations ensure that decentralized interactions remain responsive, even as the network scales.

The graph structure supports complex queries, enabling users and applications to efficiently retrieve structured data, filter information, and analyze trust relationships across decentralized identity networks. This graph-based model enables intuitive navigation and structured querying, allowing users to traverse relationships and analyze interconnected data. Complex queries facilitate efficient exploration of identity networks, trust structures, and reputation histories. The ability to model hierarchical relationships and multi-layered access controls makes it adaptable to diverse use cases, including secure messaging, decentralized identity verification, collaborative data sharing, and reputation scoring.

The architecture of the 2WAY Graph ensures resilience against failures by distributing data across multiple nodes. This redundancy improves availability and mitigates the risks associated with network disruptions. Data synchronization mechanisms maintain consistency across decentralized nodes, ensuring that changes propagate efficiently while preventing conflicts. This structure allows the system to function seamlessly even in environments with intermittent connectivity, reinforcing its reliability as a foundation for decentralized applications.

<br>

### 2.2.2 User Graph

The User Graph in the 2WAY system represents each user's unique network of nodes and edges, encapsulating their personal data, connections, and interactions. This graph reflects each user's contributions and relationships within the broader context of the Server Graph, which is the aggregate of all User Graphs in the system. Each User Graph is distinct, depicting specific interactions, preferences, and network connections.

Users always query data from their zeroth degree, meaning they primarily interact with and retrieve data directly relevant to them or within their immediate network connections. When querying the Server Graph, users explore their own graph, accessing relationships, application data, and interactions pertinent to them. This ensures users maintain a focused and personalized view of the data within the 2WAY system. They can efficiently navigate and interact with information relevant to their needs and interests while preventing exposure to unnecessary or unrelated data. Data in other User Graphs that do not overlap with their own remains invisible. Users only perceive and interact with data within their own User Graph or data directly connected to them through their network connections. Data outside their immediate network or areas of interest remains inaccessible unless explicitly granted access through ACLs.

User Graphs are stored locally and persist even when a user goes offline. A user can back up their device by syncing it with another device, making an offline backup or data dump to disk, or using a plugin that encrypts and uploads the user's backup to a service provider. When a backup is restored, the system verifies whether objects have a newer state before applying them. If an Attribute was up-voted in the backup and later down-voted by the user on a server, restoring the backup does not overwrite the newer state. This process ensures that only the most recent and relevant information is preserved. While a user’s User Graph can be synchronized across multiple devices, they do not necessarily have to be identical. A desktop may contain a more extensive graph with more stored connections, while a phone may only maintain a subset of the data necessary for mobile interactions. The system ensures that devices remain consistent with their own stored data while synchronizing critical updates to maintain logical integrity.

If changes occur locally, the system enforces access control policies when necessary, ensuring that unauthorized modifications do not affect the integrity of the graph. When updates are received over the network, the system prioritizes the most recent cryptographically signed changes, verifying their authenticity before applying them. This prevents conflicts while ensuring that outdated modifications do not overwrite newer data. A plugin can always log changes to the graph, ensuring that any modifications made within a session are recorded and, if necessary, cryptographically signed. This allows users to maintain a tamper-proof history of graph modifications, providing additional verification layers when needed.

For the proof-of-concept, the user can create new identities on the frontend by creating a new account, which will automatically have the Key Manager generate a key-pair for them in the background. This allows them to create multiple identities on a server with clear separation between them, since they would have to log out and log back in under their other identity again. In the future, this could be enhanced and refined further, and different options for features would be available.

Plugins in the 2WAY system can also create and manage objects through the Graph Manager. Each plugin has its own cryptographic key-pair, effectively making them users within the system. This allows plugins to function similarly to human users, with their own unique User Graphs, nodes, and edges. Plugins can create objects on behalf of multiple users, ensuring that not every user needs to create these objects individually, thus saving space in the graph. A market plugin, for example, could create categories and subcategories that are shared across all users. A book marketplace could create predefined genres like "Science Fiction," "Historical Fiction," or "Biographies," allowing users to add books under these categories without having to define them repeatedly. The same plugin could also pre-populate product listings for common items that many users might sell, enabling them to reference shared objects instead of duplicating entries. A document management plugin could create standardized templates for contracts, allowing different users to fill in required details while ensuring a structured data format remains in place. This minimizes redundancy and optimizes storage efficiency while ensuring structured data organization across the network.

Plugins can also define access permissions at the moment of object creation, ensuring that only authorized users can view or modify the data. A document collaboration plugin, for instance, could automatically assign read and write access to a predefined set of users or user groups when a new document is created. Instead of requiring each user to manually configure access settings, the plugin applies these rules dynamically based on predefined policies. If a marketplace plugin creates a product listing, it could allow only the listing owner to edit it while granting public read access for browsing. This ensures that structured access control mechanisms remain consistent across different applications without requiring manual intervention from users.

Data propagation across the decentralized network follows a trust-based relay mechanism, ensuring that updates reach only intended recipients. When a user updates an object, those changes synchronize with directly connected peers, who then distribute the update further based on pre-established trust relationships. This prevents unnecessary data exposure while ensuring that relevant updates propagate efficiently. Sybil attacks are mitigated not only because users gain credibility through real-world interactions, but also because users filter for relevance by degrees of separation. A malicious actor attempting to introduce fake identities into the network would find it difficult to gain visibility beyond their immediate connections, as their influence remains limited unless trusted users deliberately choose to interact with them. This filtering mechanism does not restrict network reach in the way traditional centralized systems might. Since degrees of separation naturally link all individuals within a few steps, any user in the system could theoretically connect to any other user through several degrees, ensuring that the network remains expansive while maintaining security.

The User Graph evolves dynamically as users interact, forming structured relationships between identities, reputation scores, and permissions. Trust connections determine visibility, allowing users to filter information based on degrees of separation. Query performance remains efficient as the graph scales, with indexing strategies minimizing computational overhead. Updates propagate along the shortest available paths, reducing network load while maintaining synchronization efficiency.

In most cases, objects are referenced rather than duplicated, ensuring that storage is used efficiently. However, when conflicts arise, such as when one user up-votes an object while another down-votes it, duplicates may be necessary to preserve both states. The same applies to conflicting edits or objects that exist within multiple parent-child relationships. For example, a book might be categorized under "Science Fiction" by one user and "Cyberpunk" by another, requiring distinct Edge objects while still referencing the same Attribute or Parent object.

Routing updates in a decentralized network presents unique challenges, as there is no central authority to direct data flow. Instead of searching the entire network for the best route, the system optimizes efficiency by leveraging existing user connections. Updates naturally travel through the network by following pre-established trust relationships, ensuring that data reaches its destination without the need for exhaustive searches. If all connections are treated equally, the system quickly determines the shortest path using breadth-first search, which explores the closest connections first. When connections have varying levels of importance, such as different levels of trust or priority assigned by plugins, Dijkstra’s algorithm can be used to calculate the most efficient route based on assigned weights. However, since weighted trust relationships are not always necessary, breadth-first search is sufficient in most cases. The system dynamically applies the appropriate method depending on whether weighted relationships are explicitly defined. These techniques allow the system to maintain low computational costs while ensuring that updates are delivered efficiently through the most optimal paths.

The system takes advantage of the small-world property in social and trust-based networks, where most nodes are only a few hops apart. This structure ensures that even without a centralized routing mechanism, updates can efficiently reach their intended recipients. Rather than performing network-wide searches that would require significant computational resources, updates are routed through localized trust structures, following the natural pathways formed by user relationships. By reducing redundant transmissions and avoiding unnecessary traversals, the system ensures that data propagation remains fast, scalable, and efficient, even as the network grows.

Each User Graph is cryptographically secured when synchronizing data across the network, ensuring that unauthorized modifications are impossible. Data authenticity is enforced through cryptographic signatures, preventing untrusted entities from forging or modifying graph relationships. Since cryptographic signing introduces computational overhead, the system minimizes its use by assuming that local operations on a trusted device do not require constant cryptographic verification. When a user modifies their own data on their own device, the system enforces access controls locally without requiring cryptographic validation. ACLs are checked when necessary to ensure that modifications follow established access rules, preventing unauthorized changes while optimizing performance. If necessary, a plugin can choose to log all graph modifications, cryptographically signing them before storage. This allows users to maintain a verifiable history of all changes within the system, providing additional security guarantees when needed.

Once data has been shared with another user, access control modifications do not automatically remove it from the recipient’s storage. A user cannot retroactively delete data that has been shared with another user on a separate server, as doing so would require enforcement mechanisms that do not align with the decentralized nature of the system. Users may request deletion, and such requests could be automated, but compliance with these requests depends entirely on the recipient’s willingness to honor them.

Future enhancements may include visual graph exploration tools, structured reputation analysis, and expanded interoperability between identity systems. These additions would improve user experience by providing deeper insights into trust relationships and network structure while maintaining the decentralized principles of the system.

<br>

### 2.2.3 Server Graph

The Server Graph in the 2WAY system represents the combined structure of all individual User Graphs stored on a server. Each user maintains their own directed graph, consisting of nodes and edges that define their objects, relationships, and interactions. The Server Graph integrates these separate User Graphs into a cohesive network, allowing for efficient data retrieval, structured connections, and controlled collaboration across the system.

Unlike traditional systems that duplicate data across multiple users, the Server Graph minimizes redundancy by using references instead of storing multiple copies of the same object. When different users interact with the same data, they link to a shared object rather than creating separate instances of it. This ensures that storage is optimized while maintaining clear relationships between users and the objects they interact with. However, in cases where conflicting states exist, duplicates may be necessary to preserve different user perspectives.

When users apply independent actions to the same object, such as one user up-voting and another down-voting it, both states must be retained separately. Since each vote is stored as part of the object itself, the system must create a duplicate to reflect the conflicting changes. Similarly, if an object is referenced in multiple Parent-Child relationships, separate instances of the relationship must exist to maintain structural integrity. For example, a book might be categorized under "Science Fiction" by one user and "Cyberpunk" by another, requiring distinct edges while still referencing the same object.

Time-sensitive attributes may also require multiple versions when they do not change globally for all users. If a marketplace item has fluctuating prices based on user location or seller adjustments, different users might see different values at the same time. The same applies to access control lists, where an object may include additional metadata for some users while remaining restricted for others. Conflicting edits to the same object also require temporary duplicates, ensuring that parallel modifications remain traceable until resolved.

The Server Graph is continuously evolving, adapting in real-time as users create, modify, and interact with data. Changes made within individual User Graphs are propagated to the Server Graph, ensuring that updates remain synchronized without introducing inconsistencies. In most cases, only the creator of an object has permission to modify it, unless modification rights are explicitly granted to others. When multiple users are allowed to modify the same object, the system resolves conflicts by applying the most recent valid change. If an update arrives over the network from another server, the system verifies its access permissions through the ACL before applying it. This applies to operations such as adding or removing child Attributes from a Parent object, changing an Attribute’s state through up-voting or down-voting, or any other modification that affects shared data.

When querying the Server Graph, access control policies ensure that users can only retrieve data they are permitted to see. If a user attempts to query an object that exists but is restricted, the system does not disclose its presence, returning no result instead. This prevents unauthorized users from inferring private relationships, metadata, or sensitive information about other entities in the system.

The Server Graph itself manages only local data, with broader network-wide synchronization handled by the Network Manager. When operating within a distributed environment, 2WAY instances exchange updates based on predefined trust relationships, ensuring consistency across multiple servers. Updates between nodes occur through cryptographic verification and state synchronization, ensuring that only valid, authorized changes propagate through the system. If network connectivity is lost, the Server Graph continues to operate using the latest available local data. Any pending updates are stored and synchronized once a connection is re-established, maintaining consistency across devices and servers without requiring constant online availability.

The proof-of-concept is designed to be efficient in handling data growth while maintaining query performance. Indexing strategies ensure that queries execute with minimal computational overhead, preventing performance degradation as the Server Graph expands. By structuring data in a way that naturally optimizes retrieval, the system maintains efficiency without requiring additional load distribution techniques beyond those necessary for its intended scope. Future iterations could explore additional optimizations, but the current design already supports a scalable and responsive data structure.

As the backbone of the 2WAY system, the Server Graph consolidates individual contributions into a structured, secure, and accessible environment. By integrating decentralized identity and reputation data, it facilitates trust-based interactions while preserving privacy and access control. The design ensures that 2WAY remains lightweight, resilient, and optimized for peer-to-peer communication, without relying on centralized oversight. The Server Graph works in tandem with the Network Manager, which facilitates peer-to-peer communication, ensuring that updates propagate efficiently across trusted servers while maintaining integrity and access control policies.

<br>

### 2.2.4 Graph on Disk

The Graph on Disk in the 2WAY system represents the storage mechanism used to persist the Server Graph, ensuring that all aggregated data from individual User Graphs is reliably maintained even when the system is offline. By storing the Server Graph on disk, the system guarantees durability, accessibility, and long-term integrity while enabling efficient retrieval and modification of information across the network.

The Server Graph is stored using a structured SQL schema that organizes data into dedicated tables for each plugin. These tables correspond to core object types such as Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). By leveraging a relational database management system such as SQLite3, the system ensures that all graph data is efficiently indexed, persisted, and queried. This approach enables rapid access to structured data while ensuring that operations scale effectively as the dataset grows. Since SQLite3 is an embedded database, 2WAY remains lightweight and fully self-contained, allowing the system to function without external dependencies while maintaining robust data storage capabilities.

The Graph on Disk serves as the authoritative source of truth for the 2WAY system, preserving all recorded interactions, relationships, and modifications made by users. Whenever a user creates, modifies, or deletes objects within their User Graph, these changes are recorded and synchronized with the Server Graph on disk. This ensures that the stored data remains consistent with real-time system activity, preventing data loss and maintaining structural coherence. Changes are committed in a way that minimizes unnecessary writes while ensuring that all updates remain secure and verifiable.

When conflicting states arise, such as when one user up-votes an object while another down-votes it, the Graph on Disk maintains separate object instances to preserve both perspectives. Rather than overwriting conflicting updates, the system stores multiple versions of the object until resolution occurs. This also applies to objects referenced in multiple Parent-Child relationships, ensuring that different structural contexts remain intact while linking back to shared data. The system allows for efficient resolution of such conflicts by verifying cryptographic signatures and prioritizing the most recent signed update when appropriate.

By maintaining a disk-based representation of the graph, the system facilitates efficient querying, filtering, and data analysis. Users can explore relationships, search for relevant objects, and retrieve structured insights without requiring constant in-memory processing. Indexing strategies optimize retrieval speeds, ensuring that frequently accessed data can be retrieved without performance bottlenecks. Queries can be executed based on degrees of separation, trust relationships, and structured object attributes, allowing for flexible exploration of the network while maintaining access control restrictions.

The persistence of the Graph on Disk ensures that the 2WAY system remains functional even in environments with intermittent connectivity. Users can operate offline with the most recent locally available data, and when network access is restored, pending updates can be synchronized to maintain consistency across the broader system. All offline modifications are cryptographically signed before merging with network updates to ensure data integrity and prevent conflicts.

While SQLite3 is the default database engine, the 2WAY system is designed with future scalability in mind. Future versions may introduce support for alternative storage backends, such as distributed databases or key-value stores, to accommodate larger networks with greater storage and processing demands. This flexibility would allow the system to scale beyond the proof-of-concept while maintaining the core principles of decentralization and data integrity.

As a fundamental component of the 2WAY system, the Graph on Disk ensures that all decentralized identity, reputation, and access management data remains secure, structured, and resilient. By providing a stable and efficient means of persisting graph data, it enables 2WAY to maintain reliability, scalability, and performance, supporting both individual users and large-scale distributed networks without compromising data integrity or efficiency.

<br>

### 2.2.5 Graph in RAM

The Graph in RAM in the 2WAY system serves as an in-memory representation of a subset of the Server Graph, optimized for fast query execution and efficient relationship traversal. By temporarily storing key data structures in Random Access Memory (RAM), the system minimizes disk access during common operations, significantly improving performance. The Graph Manager is responsible for creating, maintaining, and updating the Graph in RAM, ensuring that it remains synchronized with the Server Graph on disk while balancing memory efficiency.

The primary function of the Graph in RAM is to accelerate query execution by reducing the need for frequent disk access. Rather than scanning the database for every operation, the in-memory graph enables rapid lookups and traversal, significantly improving responsiveness. When a query is executed, the system begins by identifying nodes within the specified degree of separation in the Graph in RAM. This allows it to focus on the most relevant records before retrieving additional data from disk, optimizing performance and minimizing unnecessary computation.

Rather than storing record IDs as loose nodes in memory, the Graph in RAM is structured to be future-proof by explicitly associating data with its corresponding application namespace. For the proof of concept, only `app_0`, which represents the 2WAY system itself, is used. Under `app_0`, separate nodes exist for different database tables, with `app_0_attr` storing the public key Attributes and, in the future, `app_0_par` potentially representing Parent objects. The actual record IDs, such as `1` or `34`, are stored as child nodes under `app_0_attr`, allowing for a structured and scalable way of organizing graph data. This ensures that system data is always referenced explicitly through `app_0`, maintaining consistency as additional applications are introduced in future versions.

The Graph in RAM is dynamically updated as users interact with the system. If an object is referenced multiple times by different users, it remains in RAM as long as at least one active connection exists. When all edges (not Edge objects) to an Attribute are removed due to down-votes or changes in relationships, the corresponding record ID node under `app_0_attr` is also removed from memory, ensuring that RAM is not wasted on unnecessary data.

For future versions of 2WAY, if plugin-specific data needs to be stored in RAM, the system will support additional parent nodes in the in-memory graph. For example, if an application with `app_id = app_1` requires its Attributes table in RAM, the Graph Manager will create a node called `app_1_attr` and add small integer record IDs as child nodes to represent its entries. Similarly, if a plugin’s Parent table needs to be referenced in RAM, it will be stored under `app_1_par`. In future versions, plugins can designate which of their Attributes or Parents should be cached in RAM. The Graph Manager will dynamically allocate memory only to the most relevant data, ensuring that memory usage remains efficient while supporting multiple applications. Only critical or frequently queried plugin data will be included, while less relevant data remains on disk.

The Graph Manager remains responsible for loading and maintaining both core and plugin-specific data in RAM. During system initialization, it constructs the base structure, ensuring that `app_0` and its table nodes, such as `app_0_attr`, are created. As users interact with the system, the Graph Manager adds or removes record ID nodes dynamically, keeping memory usage optimized. This ensures that the in-memory graph structure remains lightweight while still enabling rapid lookups and efficient query execution.

Since the 2WAY system supports offline functionality, the Graph in RAM continues operating with the most recent available local data when network connectivity is lost. Queries are executed based on the cached in-memory graph and disk-stored relationships, allowing users to interact with stored data without interruptions. Pending modifications are stored locally and synchronized once the system reconnects to the network, ensuring consistency with other nodes.

For the proof of concept, the system uses NetworkX to manage the Graph in RAM. NetworkX is responsible not only for constructing and maintaining the Graph in RAM but also for efficiently managing in-memory relationships and ensuring optimal traversal performance. By leveraging NetworkX’s built-in graph operations, the system minimizes redundant computations and accelerates querying while maintaining a scalable structure. NetworkX also enables serialization of the Graph in RAM to disk, allowing it to be saved as a binary file when shutting down and reloaded during startup. This ensures continuity across sessions without requiring a full reconstruction from the database at every launch.

Future optimizations may include selective preloading of frequently accessed objects, dynamic caching strategies, and more granular control over memory allocation. As the system evolves, these improvements will further refine query performance while maintaining a balanced approach to resource utilization.

<br>

## 2.3 2WAY Objects <a name="23-2way-objects"></a>

### 2.3.1 Introduction to 2WAY Objects

In 2WAY, a small set of simple data structures are used to construct objects and relationships. These objects and relationships are represented as nodes and edges within the 2WAY Graph, encompassing all the data stored within the system, including user identities, application data, relationships, permissions, ratings, and other structured information. The flexibility of these objects allows the system to model a wide range of applications and data structures, with the graph structure facilitating data organization and relationships.

The following five objects are used to construct the system in its entirety:

1. **Attribute**:

    A key-value pair consisting of a "type" (the key, not to be confused with any cryptographic keys) and a "value." Attributes represent the basic units of information within 2WAY, forming the foundation for all other objects. Every piece of data in the system is ultimately defined as an Attribute, whether it represents identity-related details, metadata, or system-defined values. For example, an Attribute could store a public key (`{"type": "pubkey", "value": "ABC123"}`), a username (`{"type": "username", "value": "alice"}`), or an email address (`{"type": "email", "value": "alice@example.com"}`). Attributes also define relationships and classifications within the system, such as membership roles (`{"type": "role", "value": "admin"}`), content tags (`{"type": "tag", "value": "technology"}`), or transaction statuses (`{"type": "status", "value": "pending"}`). They can be application-specific, like a decentralized marketplace listing (`{"type": "price", "value": "29.99 USD"}`) or a voting system entry (`{"type": "vote", "value": "yes"}`).

    Since an Attribute is simply a structured representation of data, it can be used to define and represent any object in the known universe or in computational space. A planet can be described using Attributes such as mass, orbital period, and atmospheric composition. A book can be represented by Attributes for title, author, and genre. Even abstract concepts can be modeled through Attributes when they serve as factual properties of an entity, such as `"type": "trust_level", "value": "high"`. However, subjective evaluations, such as scoring a user's reputation or ranking a product, are better represented using Ratings, objects which provide structured scoring mechanisms alongside optional comments.
    
    By structuring all fundamental data as Attributes, 2WAY ensures that any application built on the platform can store, reference, and manipulate information in a uniform and extensible way. Because Attributes impose no predefined constraints on what can be represented, they allow for limitless expressibility, making it possible to model complex systems, real-world objects, and digital constructs within the same flexible framework.

2. **Parent**:

    A Parent object is a specialized type of Attribute that establishes structured relationships by referring to one or more child Attributes or child Parents through Edges. Unlike standard Attributes, which store isolated key-value pairs, a Parent object exists to define hierarchical connections within the system. It allows Attributes to be grouped logically while enabling multi-layered relationships.

    For example, a user in the 2WAY system is typically identified by their public key. A Parent object with `"type": "pubkey"` and `"value": "Alice's public key"` serves as the root of that user's information. Child Attributes linked to this Parent could define Alice’s details, such as `"type": "name", "value": "Alice"`, `"type": "email", "value": "alice@email.com"`, and `"type": "address", "value": "Roadstreet 123"`. The Parent object may also reference another Parent, such as `"type": "group", "value": "Enterprise LLC"`, indicating that Alice is part of an organization that itself has its own Attributes and hierarchical structure.

    A Parent object can also be used to model other structured relationships. A book in a digital library could be stored as a Parent with `"type": "book", "value": "1984"`, linking to Attributes like `"type": "author", "value": "George Orwell"`, `"type": "genre", "value": "Dystopian"`, and `"type": "publication_year", "value": "1949"`. In a marketplace application, a Parent might represent a product category like `"type": "category", "value": "Books"`, linking to other Parent objects representing individual books or authors, each with their own Attributes defining price, ISBN, and stock availability.

    Parent objects allow for nested hierarchical relationships, enabling more complex organizational structures. A company can be represented as a Parent `"type": "company", "value": "Enterprise LLC"`, with child Parents representing `"type": "department", "value": "Engineering"`, `"type": "department", "value": "Sales"`, each containing their own Attributes and child Parents for teams and employees.

    By using Parent objects, 2WAY enables structured, scalable relationships that maintain flexibility across different applications. Whether linking user data, organizing content, or structuring a business hierarchy, Parent objects ensure that connected Attributes and nested Parents remain logically organized and easily retrievable.

3. **Edge**:

    An Edge represents a connection between a single Parent Attribute and one or more child Attributes or child Parents. Edges define relationships within the graph, enabling structured data organization and supporting hierarchical models. Unlike Attributes, which store individual pieces of data, or Parent objects, which establish hierarchical groupings, Edges provide the fundamental linking mechanism that allows these objects to form structured relationships.

    For example, a user's public key may serve as a Parent object, with Edges connecting it to Attributes that define their details, such as `"type": "name", "value": "Alice"`, `"type": "email", "value": "alice@email.com"`, and `"type": "role", "value": "admin"`. Each of these connections is represented by an Edge, establishing a structured relationship between the Parent and its child Attributes.

    Edges also support multi-layered relationships, allowing Parent objects to connect to other Parent objects. In a corporate structure, an Edge could link `"type": "company", "value": "Enterprise LLC"` to `"type": "department", "value": "Engineering"`, with further Edges connecting the Engineering department to `"type": "team", "value": "Software Development"`, and so on. This hierarchical linking allows businesses, communities, or other structured datasets to be represented efficiently within the 2WAY system.

    Edges are also essential in applications where categorization and classification are necessary. In a marketplace, an Edge might link a Parent object representing a product category like `"type": "category", "value": "Books"` to subcategories such as `"type": "subcategory", "value": "Science Fiction"`, and further to individual book listings with `"type": "title", "value": "Dune"` and `"type": "author", "value": "Frank Herbert"`.

    Edges provide a flexible yet structured way to define and traverse relationships between objects in the 2WAY system. They ensure that data remains connected, searchable, and efficiently retrievable, allowing applications to model everything from user profiles and organizations to content taxonomies and supply chains in a unified, decentralized framework.

4. **Rating**:

    A Rating is an independent object that allows users to assign a score to an Attribute or Parent, providing a structured way to evaluate and rank entities within the 2WAY system. Ratings enable trust-based interactions by allowing users to express opinions on people, products, services, or content while maintaining data integrity. Since Ratings exist as separate objects, multiple users can rate the same entity without modifying its original data, ensuring that scores remain decentralized and resistant to manipulation.

    A user reputation system is a common example of Ratings in use. A Parent object representing a user (`"type": "pubkey", "value": "Alice's public key"`) can receive Ratings from others based on their past interactions. Each Rating could include `"type": "score", "value": "4.5"` and an optional `"type": "comment", "value": "Reliable and professional"` to provide additional context. The aggregation of Ratings over time allows for a decentralized reputation system where trust is built through recorded evaluations rather than a central authority.

    Ratings are also widely applicable in content and marketplace applications. A book review system could use Ratings attached to a Parent object representing a book (`"type": "book", "value": "Dune"`), where individual users submit Ratings like `"type": "score", "value": "5"`, `"type": "comment", "value": "A masterpiece of science fiction"`. In a decentralized marketplace, products may receive Ratings from buyers, with `"type": "score", "value": "4"`, `"type": "comment", "value": "Fast shipping, good quality"`, helping other buyers assess product reliability.

    Applications define their own rating scales, structures, and interpretation models, allowing flexibility in how Ratings are used. A plugin may implement a numeric scale such as 1 to 5 stars, a binary system like upvotes and downvotes, or a weighted trust score based on previous interactions. These structures determine how Ratings are aggregated, displayed, and used in decision-making processes within an application. Some systems may normalize Ratings across different contexts, while others might allow weighted scoring where certain users' Ratings carry more influence, such as verified buyers in a marketplace or long-term contributors in a governance system.

    Since Ratings are independent objects, they can be filtered, sorted, and queried separately from the entities they reference. The weight of Ratings can be adjusted based on context, such as limiting how frequently a user can rate the same entity or requiring verifiable interactions before submitting a score. Some applications may allow Ratings to be upvoted or downvoted by other users, further refining their credibility.

    By allowing customizable scoring systems defined by plugins, Ratings provide a flexible evaluation mechanism across different use cases. Whether used for reputation tracking, content feedback, product reviews, or governance models, Ratings enable transparent, user-driven assessments that enhance trust and decision-making in decentralized systems.

5. **Access Control List (ACL)**:

    An Access Control List (ACL) is a fundamental component of 2WAY’s security model, governing user permissions for accessing and modifying data. ACLs determine whether a user can read, write, modify, or delete specific Attributes or Parent objects. Each ACL entry links a user's public key Attribute to one or more target objects, enforcing strict access rules based on predefined permissions. By managing data visibility and modification rights at a granular level, ACLs ensure that sensitive information remains protected while allowing controlled collaboration.

    Read permissions define whether a user can query and retrieve an object. When a user attempts to access an Attribute or Parent, the system verifies whether their public key Attribute is listed in the ACL. If read permission is granted, the object is retrieved and displayed. Otherwise, no result is returned, preventing unauthorized users from inferring the existence of restricted data. This approach enhances privacy by ensuring that users cannot detect objects they are not permitted to view.

    Write permissions regulate a user’s ability to modify, delete, or create related objects. If a user lacks write access to an Attribute or Parent, any attempt to alter it will be rejected by the system. Write permissions extend to adding or removing Edges that link objects, ensuring that relationships within the graph remain controlled. In collaborative environments, ACLs allow applications to define roles where certain users can edit shared objects while others can only view them.

    ACLs also play a role in synchronization between servers. When data is shared across nodes, only objects for which a user has explicit read permissions are included in synchronization, ensuring that access control policies are maintained across distributed environments. This prevents unauthorized data leakage while allowing seamless updates between connected instances.

    Applications can implement custom permission models by defining ACL rules that adapt to specific use cases. A marketplace application may restrict product listing modifications to the seller, while a reputation system may only allow verified users to leave Ratings. Governance models can grant administrative roles to certain users, enabling them to adjust permissions for others.

    By enforcing fine-grained access control, ACLs enable a secure, decentralized environment where data access is strictly regulated, modifications are tracked, and collaboration is managed according to application-defined rules. Through this system, 2WAY provides a flexible yet robust security model that ensures data remains private, protected, and accessible only to those with the appropriate permissions.

All 2WAY objects are stored in the SQL database according to the system’s relational schema, ensuring structured and efficient data management. Each object type, including Attributes, Parents, Edges, Ratings, and ACLs, is assigned a unique record ID, which serves as a reference throughout the graph. To maintain logical separation between different applications, 2WAY organizes data into dedicated tables for each application rather than storing all objects in a single structure. Each table name is prefixed with the application's `app_id`, followed by the type of object it stores. For example, an application with `app_id = app_4` will store its Attributes in a table named `app_4_attr` and its Parent objects in `app_4_par`. This structure ensures that each application’s data remains isolated while still allowing controlled cross-application references, reducing query complexity and maintaining efficient data retrieval.

This design allows 2WAY to efficiently manage data at scale, preventing conflicts between different applications while maintaining flexibility for future expansion. Plugins function as separate applications, while the backend serves as a protocol, ensuring a structured yet extensible approach to data management. If an application needs to reference another application's data, it explicitly queries the corresponding table. Access control mechanisms, including ACLs and query restrictions, ensure that applications can only retrieve data they are authorized to access, preserving both security and data separation. Query restrictions enforce that searches start from a user's zeroth degree, meaning they can only access objects directly connected to them unless explicitly granted broader permissions, preventing unauthorized traversal of the Server Graph.

The Graph Manager plays a crucial role in managing objects within the Graph in RAM, ensuring efficient query execution and system performance. Instead of storing entire object records in memory, the Graph Manager maintains lightweight references to objects using their record IDs under the appropriate application namespace. This approach significantly reduces memory overhead while allowing for rapid lookups of frequently accessed data. When a query is performed, the Graph Manager first checks the Graph in RAM for relevant record IDs, enabling fast retrieval of directly connected nodes. If additional details are required, the system retrieves them from the SQL database, ensuring that only necessary data is loaded into memory. This hybrid approach optimizes system resources while maintaining consistency between in-memory structures and the database, preventing redundant data loading and improving response times. While the proof-of-concept only stores references to objects in RAM, future versions could allow entire objects to be stored in memory when needed, further improving query efficiency for specific use cases.

Objects in 2WAY are created and managed dynamically by applications through the Graph Manager, which acts as the interface between applications and the system’s storage layer. When an object is created, the Graph Manager forwards the creation request to the Storage Manager, which inserts the object into the appropriate database table and returns the assigned record ID. The Graph Manager then processes this record ID and, if necessary, integrates it into the Graph in RAM. Only specific objects, such as public key Attributes and frequently accessed data, are stored in-memory to optimize performance, while others remain accessible through database queries as needed.

Parent objects can be linked to their child Attributes or child Parents using Edges, defining hierarchical relationships within the graph. This structure allows for nested hierarchies, enabling complex multi-level relationships where a Parent object can itself be a child of another Parent, forming deep, structured connections within the system.

When objects are no longer needed, they are removed from both the Graph in RAM and the underlying database through coordinated updates between the Graph Manager and the Storage Manager, ensuring efficient data management. ACLs determine not only access permissions but also which objects are included in synchronization across nodes. When data is shared between servers, only objects that a user has explicit read or write permissions for are synchronized, ensuring privacy and access control remain intact.

2WAY does not enforce a specific application logic beyond its fundamental structural rules, allowing applications to define their own behaviors and interactions. Developers can extend objects dynamically by attaching metadata, defining new interaction models, or introducing application-specific processing rules. Applications can create custom object types while still relying on the core data model. For example, a reputation system may define additional Rating metadata, while a decentralized marketplace could introduce specialized Attributes for product listings. This flexible structure ensures that new applications can be built without modifying the underlying system.

The 2WAY object model enables applications to be built with flexibility, extensibility, and security in mind. By defining all system data as structured objects, 2WAY ensures that applications can model complex relationships while maintaining a standardized approach to identity, access control, and interactions. With a database structure that prevents fragmentation and supports cross-application interoperability, 2WAY provides a scalable foundation for decentralized systems. By prioritizing efficiency in querying, strict access control mechanisms, and a privacy-conscious architecture, 2WAY allows developers to build secure, efficient, and user-controlled applications that can seamlessly interact within a shared ecosystem.

<br>

### 2.3.2 Attribute

Attributes in the 2WAY system are vital key-value pairs, comprising a "type" and a "value". These Attributes serve as pivotal nodes within the server's graph structure, representing fundamental units of information. For instance, an Attribute could manifest as:

- `{"type": "name", "value": "Alice"}`
- `{"type": "pubkey", "value": "Alice's public key"}`
- `{"type": "book_title", "value": "Title of the Book"}`
- `{"type": "fileOnDisk", "value": "Path to the file"}`

Attributes are dynamically defined, either through API communication from the frontend or directly by the backend.

When a user generates an Attribute on the frontend, it's transmitted to the backend's Graph Manager API as a JSON document. For example:

```json
{
  "object": "attribute",
  "action": "new",
  "signer": "user_id",
  "app_id": "app_identifier",
  "type": "name",
  "value": "Alice",
  "vote": "1"
}
```

In this JSON structure:
- `object` indicates that this is an Attribute.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Attribute. `0` = self, for "pubkey" Attributes.
- `app_id` signifies the application identifier to ensure uniqueness and prevent naming collisions.
- `type` and `value` define the key-value pair of the Attribute.
- `vote` is a boolean value indicating the object's relevance (`1` for relevant, `0` for irrelevant).

The `vote` value aids in managing the object's lifecycle; an object with a vote of `0` is disregarded in future queries unless explicitly requested.

Once received, the Graph Manager commences the creation and management process of various object types within the system by authorized users. The newly formed Attribute is connected to the user's public key through an implicit edge. This connection is inherent since the public key is stored as an Attribute, and the new Attribute contains the signer's public key.

Optionally, each individual change can be logged to the Log Manager when updating the cryptographically unsigned object to the Graph on Disk. Logged changes can be signed before storage by passing through the Key Manager, ensuring data integrity and authenticity.

The Graph Manager also facilitates Attribute querying, enabling users to filter results based on the degree of separation and additional contextual criteria.

When queried, the newly created Attribute object is returned:

```json
{
  "id": 1,
  "signer": "user_id",
  "type": "name",
  "value": "Alice",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "document_hash"
}
```

In this JSON structure:
- `id` represents the unique identifier assigned to the Attribute in the database, ensuring each record is distinct and easily retrievable.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Attribute. `0` = self, for "pubkey" Attributes.
- `type` and `value` define the key-value pair of the Attribute.
- `vote` is a boolean value indicating the relevance of the Attribute (`1` for relevant, `0` for irrelevant).
- `timestamp` shows the time when the Attribute was created.
- `hash` represents the hash of the document.

When the change is queried from the Log Manager, the log presents the following response:

```json
{
  "id": 56,
  "action": "new",
  "signer": "user_id",
  "type": "name",
  "value": "Alice",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "document_hash",
  "signature": "cryptographic_signature"
}
```

In this JSON structure:
- `id` stands for the unique identifier assigned to the log entry.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`)
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user associated with this log entry.
- `type` and `value` define the key-value pair of the Attribute.
- `vote` is a boolean value indicating the relevance of the Attribute (`1` for relevant, `0` for irrelevant).
- `timestamp` shows the time when the log entry was created.
- `hash` represents the hash of the document.
- `signature` signifies the cryptographic signature of the log entry.

<br>

### 2.3.3 Parent

A Parent in the 2WAY system consists of a single Parent Attribute connected to one or more child Attributes and/or other Parents. This hierarchical structure allows for the organization and management of complex data relationships. For example:

```json
{
  "parent_type": "pubkey",
  "parent_value": "Alice's public key",
  "children": [
    {
      "child_type": "name",
      "child_value": "Alice"
    },
    {
      "child_type": "email",
      "child_value": "alice@email.com"
    },
    {
      "child_type": "address",
      "child_value": "Roadstreet 123"
    },
    {
      "child_parent_type": "group",
      "child_parent_value": "Enterprise LLC"
    }
  ]
}
```

In this example:
- `parent_type` is "pubkey", and `parent_value` is "Alice's public key".
- `children` array contains various child Attributes, each with its type and value, establishing specific information linked to the parent.
- `child_parent_type` and `child_parent_value` denote a child that is also a Parent, having its own child Attributes. In this case, "Enterprise LLC" can have further Attributes linked to it, reflecting its own hierarchical structure within the system.

Typically, users in the 2WAY system are identified by their public key (the "pubkey" Attribute). A user's parent Attribute might thus appear as `{"type": "pubkey", "value": "Alice's public key"}`. Child Attributes like `{"type": "username", "value": "Alice"}` or `{"type": "email", "value": "alice@gmail.com"}` are then associated with this parent, establishing the necessary relationships to organize and retrieve user data effectively.

To create objects other than users, define the required parent Attribute accordingly. For example, to store blog articles, you might use `{"type": "Post", "value": "Blog Post Title"}`. For a marketplace, start with `{"type": "category", "value": "Books"}`, followed by relevant child Attributes. A blog post could have children like `{"type": "title", "value": "Post Title"}`, `{"type": "author", "value": "Author Name"}`, and `{"type": "content", "value": "Post Content"}`. Similarly, a book might include children like `{"type": "author", "value": "Author Name"}`, `{"type": "ISBN", "value": "ISBN Code"}`, and `{"type": "content", "value": "Book Content"}`.

When creating a Parent object, the following JSON structure might be used:

```json
{
  "id": 1,
  "action": "new",
  "signer": "user_id",
  "app_id": "app_identifier",
  "parent_id": "4",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "document_hash"
}
```

In this JSON structure:
- `id` identifies the object.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Parent.
- `app_id` signifies the application identifier to ensure uniqueness and prevent naming collisions.
- `parent_id` references the parent Attribute object.
- `vote` indicates the relevance of the object (`1` for relevant, `0` for irrelevant).
- `timestamp` records the time of creation.
- `hash` represents the hash of the document.

As with any other object, changes can be signed and sent to the Log Manager, as described in the Attribute section.

<br>

### 2.3.4 Edge

In the 2WAY system, an Edge represents a parent-child relationship within the graph structure. These Edges connect objects, ensuring structural integrity and facilitating efficient data organization and retrieval. Edges are specifically created to link a Parent Attribute to its child Attributes, forming a clear and organized hierarchy.

When a new parent-child relationship is formed, an Edge is established between the Parent Attribute and its child Attributes. This relationship is explicitly defined to denote their connection within the graph.

Here's an example JSON document illustrating the establishment of a parent-child Edge:

```json
{
  "id": 1,
  "action": "new",
  "signer": "user_id",
  "parent_id": "4",
  "child_ids": [5,9,12,13,14],
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document"
}
```

In this JSON structure:
- `id` identifies the Edge object.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Edge.
- `parent_id`references the parent object.
- `child_ids` specifies the IDs of the child objects.
- `vote` indicates the relevance of the Edge (`1` for relevant, `0` for irrelevant).
- `timestamp` records the time of creation.
- `hash` represents the hash of the document.

It's important to note that Edges are only created for parent-child relationships. For other objects, such as Attributes, Ratings, and Access Control Lists (ACLs), the relationship is implied within the object itself, as they contain the signing public key. Therefore, no separate Edge objects are created for these objects.

As with any other object, changes can be signed and sent to the Log Manager, as described in the Attribute section.

<br>

### 2.3.5 Rating

In 2WAY, user or entity reputation can be effectively managed through structured JSON documents known as Ratings. These Rating objects encapsulate various reputation metrics, including comments, scores, and scales, to provide a comprehensive assessment of user or entity reputation within the system.

The Rating data structure includes the following fields:

- **comment**: Allows users to provide comments or feedback about the rated entity.
- **score**: Indicates the assigned score based on a rating scale.
- **scale**: Specifies the type or category of the rating scale used for assigning scores, predefined by the plugin.

This flexible data structure accommodates diverse rating types and scales, ensuring adaptability to different rating contexts. Once structured, the Rating object points at an Attribute or Parent within the system.

Here's an example JSON document illustrating the establishment of a Rating:

```json
{
  "id": 1,
  "action": "new",
  "signer": "user_id",
  "attribute_id": "1",
  "parent_id": "",
  "comment": "Wow, this is really great!",
  "score": "13",
  "scale": "out-of-10-but-up-to-13",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document"
}
```

In this JSON structure:
- `id` identifies the rating object.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Rating.
- `attribute_id` specifies the rated Attribute.
- `parent_id` specifies the rated Parent.
- `comment`, `score`, and `scale` capture the details of the rating.
- `vote` denotes the relevance of the rating.
- `timestamp` records the time of creation.
- `hash` represents the hash of the document.

As with any other object, changes can be signed and sent to the Log Manager, as described in the Attribute section.

<br>

### 2.3.6 Access Control List (ACL)

In 2WAY, the Access Control List (ACL) plays a pivotal role in managing user permissions within the system. This structured data entity acts as a bridge between a user's "pubkey" Attribute and the specific Attributes or Parents they are authorized to access.

The ACL object follows a structured format, containing entries that define access permissions granted to each user. These entries typically include:

- **pubkey_id**: The public key of the user for whom permissions are being defined.
- **permissions**: An array specifying the Attributes or Parents that the user is permitted to read.

Each entry in the ACL object establishes a direct link between a user's public key and the Attributes or Parents they have access to.

During state synchronization between users, the ACL plays a critical role in determining synchronized data for each connection in the User Graph. By referencing the ACL associated with each user, the system efficiently identifies permitted data for synchronization based on established permissions. This mechanism ensures that users only receive data for Attributes or Parents they have explicit read permissions for, thereby upholding data privacy and security.

Here's an example JSON document illustrating the establishment of an ACL:

```json
{
  "id": 1,
  "action": "new",
  "signer": "user_id",
  "pubkey_id": "1",
  "permissions_attribute": [3,5],
  "permissions_parent": [7,8],
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document"
}
```

In this JSON structure:
- `id` identifies the ACL object.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the ACL.
- `pubkey_id` links the ACL to a specific user.
- `permissions_attribute` and `permissions_parent` specify the attributes or parents the user can access.
- `vote` denotes the relevance of the ACL.
- `timestamp` records the time of creation.
- `hash` represents the hash of the document.

As with any other object, changes can be signed and sent to the Log Manager, as described in the Attribute section.

<br>

## 2.4 Database Schema <a name="24-database-schema"></a>

### 2.4.1 Introduction to the Database Schema

The database schema for the 2WAY system is meticulously designed to support seamless data management across the entire platform using a unified and flexible structure. This schema is implemented using SQLite3, chosen for its versatility and compatibility across various systems, aligning perfectly with 2WAY’s lightweight and accessible nature. While future iterations may explore alternative databases, SQLite3 currently demonstrates the protocol’s scalability and efficiency, particularly as it transitions to more robust environments.

The Storage Manager handles all database operations, ensuring efficient querying, storage, and retrieval of structured data. The schema unifies both frontend and backend data management into a single database, eliminating the need for separate databases for each component. This consolidation improves efficiency while maintaining a modular and scalable design.

Instead of relying on traditional relational tables, 2WAY leverages its graph-based structure to represent all data as interconnected 2WAY Objects, including Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). This design ensures consistent data representation and interaction throughout the entire platform, reducing redundancy and enhancing modularity.

User data is managed as hierarchical 2WAY Objects, eliminating the need for a dedicated `users` table. The parent object named "users" acts as a container for all user instances. Each user is represented as a Parent Attribute, such as `user_1`, which is itself a parent to multiple child Attributes. These child Attributes store user-specific information, including email, password_hash, is_active, email_confirmed_at, and last_password_reset_at. This hierarchical structure supports user registration, authentication, and management without conventional database tables, aligning with 2WAY’s graph-based model.

Similarly, plugin-specific data is organized under "app_id" objects, which are grouped under a Parent called "plugins." Each application or plugin is represented as a Parent Attribute, such as `app_1`, and is associated with child Attributes that store relevant metadata, including the hash of the application identifier, version, checksum, date_installed, and date_last_updated. These Attributes are stored in unified tables named according to the app_id, such as `app_1_attr`, ensuring consistent organization and scalability.

For the 2WAY system itself, `app_0` is reserved, and its Attributes are stored in the unified table named `app_0_attr`. This convention keeps the system's core data separate and easily identifiable, maintaining a clear boundary between the platform and installed plugins. This model eliminates the need for separate plugin-specific tables by centralizing metadata within the graph structure while preserving clear distinctions between core system data and dynamic plugin configurations.

This design decision enhances maintainability and adaptability, allowing 2WAY to support dynamic plugin configurations without structural changes to the schema. It also ensures data integrity and consistency across the entire platform, providing a scalable foundation for future expansions, including more complex graph structures and advanced querying capabilities.

Unlike traditional role-based access control models, 2WAY implements access permissions through a structured Access Control List (ACL) using graph relationships. Each ACL entry associates public key Attributes with specific data access rights. Permissions can be assigned to individual public key Attributes or to groups by associating them with Parent Attributes, such as `group_1`. This ensures fine-grained control over user permissions without the overhead of managing predefined roles.

The graph structure also enhances interoperability among plugins. Each plugin or application adheres to a consistent schema design within the database, as detailed in section 2.4.2, "Database Schema Design." By representing plugins as Parent Attributes, conflicts are prevented, enabling seamless data access and utilization across different modules, fostering collaboration and synergy.

This meticulous schema design fosters interoperability and seamless integration among plugins within the 2WAY system. By maintaining consistent naming conventions and structural guidelines, plugins can easily interact and share data, promoting code reuse and simplifying the development process while ensuring compatibility across diverse plugin functionalities.

In essence, the structured database schema underscores 2WAY’s commitment to modularity, flexibility, and interoperability. It enables developers to extend the platform with new features seamlessly while upholding consistency and compatibility across the entire ecosystem.

<br>

### 2.4.2 Database Schema Design

The 2WAY database schema is designed as a unified structure for managing all data across the platform, leveraging a graph-based model that ensures flexibility, scalability, and consistency. Implemented in SQLite3, the schema consolidates both frontend and backend data management into a single database, eliminating the need for separate tables for user management and plugins. This approach maintains efficiency while ensuring seamless integration and interoperability across all modules.

Instead of traditional rigid relational tables, the schema organizes data using interconnected 2WAY Objects, including Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). These objects are stored in relational tables within SQLite3 but are structured to model graph-like relationships. This approach allows flexible data representation and interaction while maintaining referential integrity and supporting advanced querying capabilities. It also allows the system to be lightweight enough to run in embedded environments, using SQLite3 on a phone or IoT device.

Here are the core tables in the schema:

**Attributes Table**: This table stores all key-value pairs representing fundamental units of information within the 2WAY system, including public keys, user data, and application metadata. It acts as the foundation for the graph structure by connecting to Parent objects. Attributes can represent various types of data, including identity keys, content metadata, and plugin-specific details.

- `id` INT: Unique identifier for the attribute.
- `type` TEXT: Type of the attribute, such as `email`, `pubkey`, or `app_id`.
- `signer` INT: Refers to the record ID that stores the public key (pubkey) of the entity creating the Attribute. `0` = self.
- `value` TEXT: Value of the attribute.
- `vote` INT: Vote count for the attribute, indicating relevance.
- `timestamp` INT: Timestamp of the attribute creation or modification.
- `hash` TEXT: Hash of the document, ensuring data integrity.
- `PRIMARY KEY (id)`: Primary key ensuring uniqueness.

**Parents Table**: This table stores all hierarchical relationships within the graph, organizing Attributes into meaningful structures. It represents entities that act as containers for other Attributes, enabling the construction of complex data hierarchies. For example, it manages user data as child Attributes under `users` or application metadata under `app_id`. Parent objects can also be nested to represent multi-level hierarchies.

- `id` INT: Unique identifier for the parent.
- `type` TEXT: Type of the parent, such as `user_id`, `app_id`, or `group_id`.
- `signer` INT: Refers to the record ID that stores the public key (pubkey) of the entity creating the Parent.
- `parent_id` INT: Identifier of the parent object, supporting hierarchical nesting.
- `vote` INT: Vote count for the parent.
- `timestamp` INT: Timestamp of the parent creation or modification.
- `hash` TEXT: Hash of the document, ensuring data integrity.
- `PRIMARY KEY (id)`: Primary key ensuring uniqueness.
- `FOREIGN KEY (parent_id) REFERENCES Parents(id) ON DELETE CASCADE`: Ensures referential integrity within hierarchical structures.

**Edges Table**: This table manages all connections between Parent and child Attributes, defining relationships within the graph. It enables the representation of complex data models, including hierarchical structures for user management and plugin metadata. Child nodes are stored as a JSON array within the relational table to facilitate flexible and efficient querying.

- `id` INT: Unique identifier for the edge.
- `type` TEXT: Type of the edge, defining the relationship.
- `signer` INT: Refers to the record ID that stores the public key (pubkey) of the entity creating the Edge.
- `parent_id` INT: Identifier of the parent node.
- `child_ids` JSON: JSON array of child node IDs stored as TEXT in SQLite3.
- `vote` INT: Vote count for the edge.
- `timestamp` INT: Timestamp of the edge creation or modification.
- `hash` TEXT: Hash of the document, ensuring data integrity.
- `PRIMARY KEY (id)`: Primary key ensuring uniqueness.
- `FOREIGN KEY (parent_id) REFERENCES Parents(id) ON DELETE CASCADE`: Ensures referential integrity within the graph structure.

**Rating Table**: This table stores all reputation metrics and feedback, linking them to Attributes or Parents within the graph. It supports flexible rating scales, enabling customizable reputation systems. Ratings can be associated with either leaf nodes (Attributes) or hierarchical structures (Parents), allowing dynamic and context-specific reputation calculations.

- `id` INT: Unique identifier for the rating entry.
- `type` TEXT: Type of the rating entry, such as `review`, `reputation_score`, or `feedback`.
- `signer` INT: Refers to the record ID that stores the public key (pubkey) of the entity creating the Rating.
- `attribute_id` INT: Identifier of the related attribute.
- `parent_id` INT: Identifier of the related parent, supporting hierarchical rating models.
- `comment` TEXT: Optional comment associated with the rating entry.
- `score` TEXT: Score given in the rating entry, customizable for different rating systems.
- `scale` TEXT: Scale of the score, defined by the application or plugin.
- `timestamp` INT: Timestamp of the rating entry creation or modification.
- `hash` TEXT: Hash of the document, ensuring data integrity.
- `PRIMARY KEY (id)`: Primary key ensuring uniqueness.
- `FOREIGN KEY (attribute_id) REFERENCES Attributes(id) ON DELETE CASCADE`: Ensures referential integrity with the Attributes table.
- `FOREIGN KEY (parent_id) REFERENCES Parents(id) ON DELETE CASCADE`: Ensures referential integrity with the Parents table.

**ACL Table**: This table manages access control within the 2WAY system using graph relationships. It supports fine-grained permissions for both individual users and groups by associating public key Attributes or Parent objects with specific access rights. Permissions can be assigned to individual entities through `pubkey_id` or to groups using `parent_id`, enabling flexible role-based or attribute-based access control.

- `id` INT: Unique identifier for the ACL entry.
- `signer` INT: Refers to the record ID that stores the public key (pubkey) of the entity creating the ACL.
- `pubkey_id` INT: Identifier of the public key (individual access control).
- `parent_id` INT: Identifier of the parent (group access control).
- `permissions` TEXT: Permissions associated with the ACL entry, such as read, write, or admin.
- `timestamp` INT: Timestamp of the ACL entry creation or modification.
- `hash` TEXT: Hash of the document, ensuring data integrity.
- `PRIMARY KEY (id)`: Primary key ensuring uniqueness.
- `FOREIGN KEY (pubkey_id) REFERENCES Attributes(id) ON DELETE CASCADE`: Ensures referential integrity with the Attributes table.
- `FOREIGN KEY (parent_id) REFERENCES Parents(id) ON DELETE CASCADE`: Ensures referential integrity with the Parents table.

This schema consolidates all data management into a unified graph-based model, supporting dynamic user and application data structures while maintaining data integrity and referential consistency. It eliminates the need for separate tables for frontend and backend operations, allowing seamless data access and utilization across all 2WAY modules. By leveraging hierarchical relationships and structured graph queries, the system ensures efficient data retrieval and interaction while maintaining compatibility and scalability across diverse plugin functionalities.

The schema’s flexibility allows developers to extend 2WAY with new features and applications without structural modifications, ensuring long-term adaptability and interoperability within the 2WAY ecosystem.

<br>

## 2.5 Graph Manager <a name="25-graph-manager"></a>

### 2.5.1 Introduction to the Graph Manager

In the 2WAY system, the Graph Manager is the central hub for managing graph data, including creating, querying, modifying, deleting, and up- and down-voting core objects like Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). It ensures efficient data handling and consistency through APIs.

Users interact with the frontend interface to create or manage objects, which sends API calls containing data such as Attribute key-value pairs or parent-child relationships to the backend's Graph Manager. The Graph Manager processes these requests, forwarding relevant information to the Log Manager for logging and the Network Manager for secure transmission. It maintains synchronization between the Graph in RAM and the disk-based Server Graph.

Querying objects is done through API calls to the Graph Manager, specifying parameters like the degree of separation from the user's public key and object type. The Graph Manager retrieves relevant nodes from the Graph in RAM and, if needed, fetches additional data from the disk with the Storage Manager. Data is stored in relational tables within SQLite3 but modeled as a graph structure in RAM for efficient querying. The queried data is then returned to the frontend.

The Graph in RAM is constructed using record IDs from the `pubkey` Attributes stored in the unified Attributes table, specifically within `app_0_attr` for the 2WAY system itself. During system initialization, the Graph Manager loads the relevant `pubkey` nodes and their edges into memory, creating a graph structure that models the hierarchical and relational data stored in the Server Graph. This construction is synchronized during significant updates, system initialization, and shutdowns, ensuring that the in-memory representation remains consistent with the disk-based Server Graph.

For the proof-of-concept, only `pubkey` Attributes are used in the Graph in RAM to efficiently model user and connection relationships. This choice keeps the initial implementation lightweight and focused while demonstrating the system's core functionality. However, this approach is designed to be expandable. Future versions could expand the Graph in RAM to include other Attributes or Parents, enabling more complex graph structures. Instead of limiting the in-memory graph to `pubkey` Attributes, additional nodes could represent objects from installed plugins, such as a movie category in a media catalog, a product listing in a decentralized marketplace, or a forum post within a discussion platform. Parents could group related Attributes into structured hierarchies, allowing for efficient querying of categories, ownership relations, or trust networks.

For example, a marketplace plugin could introduce `Parent` objects for product categories and `Attribute` nodes for individual items, enabling rapid lookup of available listings. A social application could structure user-generated content as a graph, where `Parent` nodes represent discussion threads and `Edges` connect responses to original posts. A collaborative knowledge base could model relationships between concepts, making it easier to traverse related topics dynamically. These enhancements would expand the system’s ability to represent diverse application data while maintaining fast in-memory operations for queries like recommendations, search indexing, and structured filtering.

By consolidating object management in the Graph Manager and exposing functionalities through APIs, the 2WAY system ensures consistency, security, and scalability. This approach simplifies database interactions, enhancing system usability and maintainability. Object management includes maintaining relational integrity between Attributes, Parents, and Edges while preserving hierarchical relationships.

The Graph Manager synchronizes the Graph in RAM with the Server Graph during system initialization, shutdown, or significant updates, ensuring data consistency. It updates nodes and edges in the Graph in RAM when changes occur, such as adding or removing connections. These changes are propagated back to the Server Graph, updating the corresponding records in the relational tables within SQLite3 to maintain consistency between the in-memory and disk-based representations.

Querying operations leverage the graph structure in RAM to efficiently explore relationships, particularly by degree of separation from the user's public key. These queries are optimized using caching for in-memory traversal and indexing strategies within SQLite3 for efficient relational queries. Users query the Graph Manager to obtain table record IDs of relevant nodes for efficient data exploration. These queries leverage relational joins in SQLite3 to efficiently model graph traversal operations, supporting advanced querying capabilities while maintaining referential integrity.

The Graph Manager efficiently handles nested relationships by maintaining hierarchical connections between Parent and child nodes. This structure supports dynamic data models, including user hierarchies and plugin metadata, allowing for flexible and context-specific data retrieval.

The Graph Manager is also responsible for enforcing Access Control Lists (ACLs), ensuring that users and applications can only modify objects they have permission to access. ACL checks are applied selectively to prevent unauthorized changes, such as modifying shared data, editing objects owned by other users, or interacting with restricted plugin-managed content. Because users only query from their own zeroth degree and do not gain access to other users’ data through standard queries, ACL enforcement primarily focuses on write and modification permissions rather than read access.

ACL verification occurs before any modifications are written to disk, preventing unauthorized changes at the Graph Manager level. Additionally, when another user connects via the Network Manager, the State Engine evaluates ACLs to determine which objects should be synchronized. This ensures that shared Attributes, Ratings, or Parent relationships are only accessible by authorized recipients.

Actions such as adding new objects under a parent that the user does not own, modifying shared content, or deleting objects created by others require ACL validation. However, operations that only affect a user’s own objects, such as querying their own data or modifying self-created attributes, do not require ACL enforcement. This selective approach ensures a balance between security, system efficiency, and decentralized data sharing within 2WAY.

Error handling and validation are integrated into the Graph Manager to ensure robust data integrity and security. Each API request is validated for completeness, consistency, and authorization before processing. Errors and edge cases, such as invalid references or cyclic dependencies, are gracefully managed, with detailed logging sent to the Log Manager for auditing and debugging.

The proof-of-concept focuses on storing record IDs of public key Attributes in the unified Attributes table named `app_0_attr`, which is reserved for 2WAY itself. This naming convention keeps the system’s core data separate and easily identifiable within the unified schema. For example, if Alice signs her own public key, it is stored as an Attribute with the record ID `1` under `app_0_attr`, and a corresponding node is added to the Graph in RAM. If Alice adds Bob's public key as an Attribute with record ID `34`, a node and edge are added to the Graph in RAM. When a `pubkey` Attribute is down-voted or deleted, the node and edge are removed from the Graph in RAM, but data in SQLite3 persists unless explicitly deleted.

All other applications and plugins are organized under the "plugins" Parent, each represented as a Parent object such as `app_1`, `app_2`, and so on. Their corresponding Attributes are stored in similarly named tables, such as `app_1_attr`, ensuring a consistent hierarchical structure while maintaining clear separation between the core system (`app_0`) and installed plugins. This approach keeps the schema organized and scalable, supporting dynamic plugin configurations without structural modifications.

By managing synchronization, changes, and queries, the Graph Manager ensures the integrity, accessibility, and responsiveness of graph data within the 2WAY system.

<br>

### 2.5.2 Creating and Managing Objects

To create or manage objects within the 2WAY system, users interact with the frontend interface, which communicates with the backend's Graph Manager through API calls. These API calls contain JSON documents specifying the details of the objects to be created, updated, or deleted. Below are examples of JSON documents for creating different types of objects based on the database schema:

### Creating Attributes
```json
{
  "object": "attribute",
  "action": "new",
  "signer": "user_id",
  "app_id": "app_identifier",
  "type": "name",
  "value": "Alice",
  "vote": "1"
}
```
In this JSON structure:
- `object` specifies the type of object being created, which is an `attribute`.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Attribute. `0` = self, for "pubkey" Attributes.
- `app_id` is the unique identifier for the application.
- `type` indicates the type of the attribute, in this case, `name`.
- `value` is the value of the attribute, here it is `Alice`.
- `vote` denotes the relevance or importance of the attribute, set to `1`.

### Creating Parents
```json
{
  "object": "parent",
  "action": "new",
  "signer": "user_id",
  "app_id": "app_identifier",
  "parent_id": 123,
  "vote": "1"
}
```
In this JSON structure:
- `object` specifies the type of object being created, which is a `parent`.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Parent.
- `app_id` is the unique identifier for the application.
- `parent_id` is the identifier for the Parent object.
- `vote` denotes the relevance or importance of the Parent, set to `1`.

### Creating Edges
```json
{
  "object": "edge",
  "action": "new",
  "signer": "user_id",
  "app_id": "app_identifier",
  "parent_id": 123,
  "child_ids": [456, 789],
  "vote": 1
}
```
In this JSON structure:
- `object` specifies the type of object being created, which is an `edge`.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Edge.
- `app_id` is the unique identifier for the application.
- `parent_id` is the identifier for the Parent node.
- `child_ids` is a list of identifiers for the child nodes.
- `vote` denotes the relevance or importance of the edge, set to `1`.

### Creating Ratings
```json
{
  "object": "rating",
  "action": "new",
  "signer": "user_id",
  "app_id": "app_identifier",
  "attribute_id": 0,
  "parent_id": 456,
  "comment": "Great experience!",
  "score": "5",
  "scale": "5",
  "vote": 1
}
```
In this JSON structure:
- `object` specifies the type of object being created, which is a `rating`.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Rating.
- `app_id` is the unique identifier for the application.
- `attribute_id` is the identifier for the related attribute.
- `parent_id` is the identifier for the related Parent.
- `comment` captures the user's feedback, here it is `Great experience!`.
- `score` is the rating score given by the user, set to `5`.
- `scale` indicates the scale of the score, set to `5`.
- `vote` denotes the relevance or importance of the rating, set to `1`.

### Creating ACLs
```json
{
  "object": "acl",
  "action": "new",
  "signer": "user_id",
  "app_id": "app_identifier",
  "pubkey_id": 123,
  "access_to_id": [456, 789],
  "access_to_parent": 0,
  "permissions": 1
}
```
In this JSON structure:
- `object` specifies the type of object being created, which is an `acl` (Access Control List).
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the ACL.
- `app_id` is the unique identifier for the application.
- `pubkey_id` is the identifier of the public key.
- `access_to_id` is a list of identifiers for the objects to which access is being granted.
- `access_to_parent` indicates the Parent object to which access is being granted.
- `permissions` specifies the level of permissions granted, set to `1`.

Upon receiving these JSON documents from clients or the backend/system, the Graph Manager manipulates the 2WAY Graph as requested. If logging is necessary, the documents are sent to the Key Manager for timestamping and signing before being passed to the Log Manager.

The messages processed by the Graph Manager result in objects being created, updated, or deleted in the database via the Storage Manager. Additionally, the Graph Manager ensures that any necessary updates are made to the Graph in RAM.

When the Graph Manager receives a message from the Network Manager (i.e., from another server), it processes the received documents and logs them in a similar manner, ensuring consistent and secure updates across the system.

<br>

### 2.5.3 Managing Object Visibility

Objects within the 2WAY system can be created, updated, deleted, or down-voted. The latter signifies their irrelevance or disapproval by the user, and down-voted objects are not returned when queried for, unless specified otherwise. This approach ensures data integrity and historical traceability, as every interaction with an object can be preserved. Different users may have varying perspectives on the relevance or validity of an object, and preserving objects allows the system to accommodate these differing opinions.

An example of a JSON document for updating and down-voting an Attribute, to be processed by the Graph Manager:

```json
{
  "object": "attribute",
  "action": "edit",
  "signer": "user_id",
  "app_id": "app_identifier",
  "type": "name",
  "value": "Alice",
  "vote": "0"
}
```

In this JSON structure:
- `object` specifies the type of object being updated or down-voted, which is an `attribute`.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`), in this case `edit`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user making the change.
- `app_id` is the unique identifier for the application.
- `type` indicates the type of the attribute, in this case, `name`.
- `value` is the value of the attribute, here it is `Alice`.
- `vote` denotes the relevance or importance of the attribute, set to `0` indicating down-vote.

In case of logging, upon receiving this JSON document, the Graph Manager forwards the document to the Key Manager for signing.

```json
{
  "object": "attribute",
  "action": "edit",
  "signer": "user_id",
  "app_id": "app_identifier",
  "type": "name",
  "value": "Alice",
  "vote": "0",
  "timestamp": 1618000000,
  "hash": "generated_hash",
  "signature": "generated_signature"
}
```

The signed document is then forwarded to the Log Manager for logging. Concurrently, the Graph Manager updates the 2WAY Graph in RAM and synchronizes changes with the Graph on Disk via the Storage Manager to reflect the updated or down-voted state.

By preserving objects and utilizing mechanisms for down-voting, the 2WAY system allows users to filter and prioritize data according to their own preferences and judgments. This ensures a more personalized and user-centric experience, where each individual can curate their digital environment without permanently removing information that might be relevant to others.

While the current proof-of-concept does not support automatic removal of objects, future implementations could incorporate mechanisms for cleaning up the database. For example, duplicate objects or those beyond a certain age threshold could be automatically pruned to maintain database efficiency and manageability. Such features would require careful consideration of criteria and processes to ensure consistency and data integrity in the system.

<br>

### 2.5.4 Querying Objects

In the 2WAY system, users initiate object queries through the frontend interface, which communicates with the backend's Graph Manager via API calls. These API calls include JSON documents that specify parameters such as object type, degree of separation from the user's zeroth degree (their public key), and voting status. By default, the system retrieves and returns up-voted objects, ensuring users receive the most relevant data.

Here is an example JSON document for querying up-voted objects:

```json
{
  "object": "attribute",
  "signer": "user_id",
  "app_id": "app_identifier",
  "type": "book_title",
  "value": "",
  "degree": 2,
  "vote": 1
}
```

In this JSON structure:
- `object` specifies the type of object being queried, which is an `attribute`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user querying the data.
- `app_id` is the unique identifier for the application.
- `type` indicates the type of the Attribute, in this case, `book_title`.
- `value` is the value of the Attribute, here it is an empty string.
- `degree` specifies the degree of separation for the query, set to `2`.
- `vote` denotes the relevance or importance of the Attribute, set to `1`.

Upon receiving this JSON document, the Graph Manager processes the request by first identifying relevant nodes within the Graph in RAM, by degree of separation. It then queries data from the database based on the specified parameters. The queried data is subsequently returned to the frontend for user interaction.

For querying down-voted objects, users can adjust the "vote" parameter accordingly. Here's an example JSON document for querying down-voted objects:

```json
{
  "object": "attribute",
  "signer": "user_id",
  "app_id": "app_identifier",
  "type": "book_title",
  "value": "",
  "degree": 2,
  "vote": 0
}
```

Setting the "vote" parameter to "0" retrieves the down-voted objects, enabling users to access data that they or others have considered less relevant or disagreed with. This feature provides a comprehensive view of the data landscape within the 2WAY system, accommodating diverse perspectives and preferences.

Upon receiving these JSON documents, the Graph Manager processes the request directly, ensuring that the queried objects match the specified parameters, including object type, degree of separation, and vote status. The Graph Manager retrieves and returns accurate data from the database, maintaining consistency and relevance in the retrieved information.

By supporting queries for both up-voted and down-voted objects, the 2WAY system offers a balanced approach to data retrieval. This approach enhances user experience by delivering relevant and up-to-date information by default, while also allowing users the flexibility to explore broader data sets as needed. It underscores the system's commitment to user-centric design and comprehensive data management capabilities.

<br>

### 2.5.5 Filtering Objects

In addition to querying objects, users can filter objects within the 2WAY system based on specific criteria. This filtering functionality allows users to narrow down their search results and focus on the most relevant information. Filtering can be applied to all object types within the system, except for Edge objects.

Below is an example of a JSON document for filtering objects based on specific criteria:

```json
{
  "object": "attribute",
  "signer": "user_id",
  "app_id": "app_identifier",
  "criteria": {
    "type": "first_name",
    "value": "Alice",
    "degree": 3,
    "vote": 1
  }
}
```

In this JSON structure:
- `object` specifies the type of object being queried, which is an `attribute`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user making the query.
- `app_id` is the unique identifier for the application.
- `criteria` is an object that contains the specific parameters for filtering:
  - `type` indicates the type of the Attribute, in this case, `first_name`.
  - `value` is the value of the Attribute to filter by, here it is `Alice`.
  - `degree` specifies the degree of separation for the query, set to `3`.
  - `vote` denotes the relevance or importance of the Attribute, set to `1`.

Upon receiving this JSON document, the Graph Manager applies the specified filtering criteria to the queried data, returning only the objects that match the given criteria. This enables users to efficiently retrieve and analyze data based on their specific requirements.

#### Filtering by Parent

To filter objects based on Parents, users can specify criteria for Parents in their query. Below is an example of a JSON document for filtering objects that have a specific parent relationship:

```json
{
  "object": "parent",
  "signer": "user_id",
  "app_id": "app_identifier",
  "criteria": {
    "parent_type": "book_title",
    "parent_value": "",
    "degree": 1,
    "vote": 1
  }
}
```

In this JSON structure:
- `object` specifies the type of object being queried, which is a `parent`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user making the query.
- `app_id` is the unique identifier for the application.
- `criteria` is an object that contains the specific parameters for filtering:
  - `parent_type` indicates the type of the parent object to filter by, in this case, `book_title`.
  - `parent_value` specifies the value of the parent object, which is left empty in this example.
  - `degree` specifies the degree of separation for the query, set to `1`.
  - `vote` denotes the relevance or importance of the parent relationship, set to `1`.

#### Filtering by Ratings

To filter objects based on Ratings, users can specify criteria for Ratings in their query. Below is an example of a JSON document for filtering objects that have positive ratings:

```json
{
  "object": "rating",
  "signer": "user_id",
  "app_id": "app_identifier",
  "criteria": {
    "min_score": "6",
    "scale": "out-of-10",
    "degree": 1,
    "vote": 1
  }
}
```

In this JSON structure:
- `object` specifies the type of object being queried, which is a `rating`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user making the query.
- `app_id` is the unique identifier for the application.
- `criteria` is an object that contains the specific parameters for filtering:
  - `min_score` indicates the minimum score to filter by, set to `6`.
  - `scale` specifies the scale of the Rating, in this case, `out-of-10`.
  - `degree` specifies the degree of separation for the query, set to `1`.
  - `vote` denotes the relevance or importance of the Rating, set to `1`.

#### Filtering by ACL

To filter objects based on Access Control Lists (ACLs), users can specify criteria for ACLs in their query. Below is an example of a JSON document for filtering objects that meet certain ACL criteria:

```json
{
  "object": "acl",
  "signer": "user_id",
  "app_id": "app_identifier",
  "criteria": {
    "type": "",
    "value": "",
    "permissions": 1,
    "degree": 1,
    "vote": 1
  }
}
```

In this JSON structure:
- `object` specifies the type of object being queried, which is an `acl`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user making the query.
- `app_id` is the unique identifier for the application.
- `criteria` is an object that contains the specific parameters for filtering:
  - `type` indicates the type linked to the ACL, left empty in this case, returning all relevant objects.
  - `value` specifies the value linked to the ACL, left empty in this case, returning all relevant objects.
  - `permissions` indicates the level of permissions required, set to `1`.
  - `degree` specifies the degree of separation for the query, set to `1`.
  - `vote` denotes the relevance or importance of the ACL, set to `1`.

#### Comprehensive Filtering

Here is a more extensive and potentially UX-friendly search query example that demonstrates filtering based on various criteria, including Attributes, Ratings, and relationships:

**Goal:** Retrieve all "phone numbers" (Attributes with type=”phone_number” and any value) of "restaurants" (Parent object), apart from "The French Cock" (attribute; type="restaurant" and value="The French Cock"), with "positive ratings" (Rating object) from "Friends" (Parent object) and "Family" (Parent object), but not "people with bad taste in food" (Parent object) in zeroth degree, and signed by anyone within 2 degrees of separation or less.

```json
{
  "object": "attribute",
  "signer": "user_id",
  "app_id": "app_identifier",
  "degree": 2,
  "criteria": {
    "type": "phone_number",
    "vote": 1,
    "parent": {
      "type": "restaurant",
      "exclude_value": "The French Cock"
    },
    "ratings": {
      "min_score": "1.75",
      "scale": "out-of-5-stars",
      "vote": 1,
      "signed_by": ["Friends", "Family"]
    },
    "exclude_parents": ["people with bad taste in food"]
  }
}
```

In this JSON structure:
- `object` specifies the type of object being queried, which is an `attribute`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user making the query.
- `app_id` is the unique identifier for the application.
- `degree` specifies the degree of separation for the query, set to `2`.
- `criteria` is an object that contains specific parameters for filtering:
  - `type` indicates the type of attribute, in this case, `phone_number`.
  - `vote` denotes the relevance or importance of the attribute, set to `1`.
  - `parent` specifies criteria related to the parent object:
    - `type` indicates the type of parent object, here it is `restaurant`.
    - `exclude_value` excludes attributes associated with the restaurant named `The French Cock`.
  - `ratings` defines criteria related to ratings:
    - `min_score` specifies the minimum score required, set to `1.75`.
    - `scale` indicates the scale of the rating, here it is `out-of-5-stars`.
    - `vote` denotes the relevance or importance of the rating, set to `1`.
    - `signed_by` lists entities that have signed the rating, including `Friends` and `Family`.
  - `exclude_parents` lists parent categories to exclude, such as `people with bad taste in food`.

Upon receiving this JSON document, the Graph Manager processes the request by first identifying relevant nodes within the Graph in RAM. It then uses the resulting record IDs to query data from the database with the help of the Storage Manager, applying all specified filtering criteria before returning the data to the frontend.

This approach to filtering objects ensures that users can refine their queries to retrieve the most relevant and useful information, tailored to their specific needs and preferences. By supporting complex filtering criteria, the 2WAY system offers a robust and flexible method for data retrieval, enhancing overall user experience and data discoverability.

<br>

### 2.5.6 Storing and Retrieving the Graph in RAM

The Graph Manager in the 2WAY system is responsible for the storage and retrieval of the Graph in RAM, ensuring its synchronization with the persistent Server Graph. This process involves constructing the Graph in RAM from the Server Graph, storing it to disk, and retrieving it when necessary.

The Graph in RAM is initially constructed from the Server Graph, utilizing the NetworkX library to create and manage graph data structures in Python. During initialization, the Graph Manager populates the in-memory graph with relevant nodes and edges (not to be confused with Edge objects) based on the data stored in the Server Graph. These nodes can represent various objects such as Attributes, Parents, and connections between users.

Once constructed, the Graph in RAM can be stored to disk for persistence using the "nx.write_gpickle" function provided by NetworkX. This serialization process saves the graph data structure in a binary format, allowing it to be efficiently written to disk for long-term storage. Storing the graph to disk ensures that the latest state of the Graph in RAM is preserved even when the system is restarted or shut down.

When the system is initialized or when the Graph in RAM needs to be reconstructed, the Graph Manager retrieves the serialized graph data from disk using the "nx.read_gpickle" function. This deserialization process loads the graph structure back into memory, restoring it to its previous state. The retrieved graph can then be verified against the Server Graph to ensure consistency and accuracy.

At any point, the Graph in RAM can be verified against the Server Graph to confirm that they are synchronized. This verification process involves comparing the nodes and edges in the in-memory graph with the corresponding data in the Server Graph. Discrepancies or inconsistencies can be identified and resolved to maintain data integrity.

Additionally, if the Graph in RAM becomes corrupted or needs to be reconstructed from scratch, the Graph Manager can rebuild it using data from the Server Graph. This reconstruction process involves fetching the relevant data from the Server Graph and populating the in-memory graph accordingly.

In summary, the Graph Manager handles the storage and retrieval of the Graph in RAM, ensuring its alignment with the persistent Server Graph. By utilizing serialization and deserialization techniques provided by the NetworkX library, the Graph Manager enables efficient data management and synchronization within the 2WAY system.

<br>

### 2.5.7 Changes to Graph in RAM

The 2WAY system's Graph Manager is designed to handle dynamic changes in the Graph in RAM, specifically focusing on managing record IDs of public key Attributes with unique identifiers. This section elaborates on how nodes and edges are modified based on interactions within the 2WAY system, using JSON document examples to demonstrate these modifications.

#### Adding Nodes and Edges

When a user, such as Alice, initially stores her own public key, an Attribute is created with a distinct record ID stored in the `app_0_attr` table.

```json
{
  "id": 1,
  "signer": "user_id",
  "type": "pubkey",
  "value": "alices_pubkey",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "document_hash"
}
```

In this JSON structure:
- `id` represents the unique identifier of the Attribute, here set to `1`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Attribute. `0` = self, for "pubkey" Attributes.
- `type` specifies the type of Attribute, in this case, `pubkey`, indicating it represents Alice's public key.
- `value` holds the actual value of the Attribute, which is "alices_pubkey".
- `vote` indicates the relevance or importance of the Attribute, set to `1`.
- `timestamp` records the time when the Attribute was created or modified, specified as `1648062000`.
- `hash` represents the hash value associated with the document, ensuring data integrity and authenticity.

This JSON document illustrates the creation of a node in the Graph in RAM, representing Alice's public key Attribute within the 2WAY system.

Upon creating this object, the Graph Manager adds a node with the value "1" to the Graph in RAM, representing Alice's public key.

Next, if Alice adds Bob's public key as an Attribute, another Attribute is created, resulting in a new record ID:

```json
{
  "id": 34,
  "signer": "1",
  "type": "pubkey",
  "value": "Bob's public key",
  "vote": 1,
  "timestamp": 1648062010,
  "hash": "document_hash"
}
```

In this JSON structure:
- `id` specifies the unique identifier of the Attribute, which is `34`.
- `signer` indicates the entity (in this case, Alice's public key) responsible for adding or modifying the Attribute.
- `type` denotes the type of Attribute, which is `pubkey`, indicating it represents a public key.
- `value` contains the actual value of the Attribute, which is "Bob's public key".
- `vote` signifies the relevance or importance of the Attribute, set to `1`.
- `timestamp` records the time when the Attribute was created or modified, set to `1648062010`.
- `hash` represents the hash value associated with the document, ensuring data integrity and authenticity.

The Graph Manager then adds a node with the value "34" to the Graph in RAM and creates a directed edge between nodes "1" (Alice) and "34" (Bob), establishing a connection between the two users, from Alice, to Bob.

#### Removing Nodes and Edges

If a "pubkey" Attribute, or, connection is down-voted, it signifies that the connection is no longer relevant or trusted. This down-vote action is represented by the following JSON document:

```json
{
  "id": 34,
  "signer": "1",
  "type": "pubkey",
  "value": "bobs_pubkey",
  "vote": 0,
  "timestamp": 1648062020,
  "hash": "document_hash"
}
```

In this JSON structure:
- `id` specifies the unique identifier of the Attribute, which is `34`.
- `signer` indicates the entity responsible for the action, identified by the record ID `1`.
- `type` denotes the type of Attribute, which is `pubkey`, representing a public key.
- `value` contains the actual value of the Attribute, which is `bobs_pubkey`.
- `vote` signifies the relevance or importance of the Attribute, set to `0`, indicating a down-vote.
- `timestamp` records the time when the down-vote action occurred, set to `1648062020`.
- `hash` represents the hash value associated with the document, ensuring data integrity and authenticity.

Upon processing this JSON document, the Graph Manager queries the Attribute for Bob's "pubkey", and verifies the previous version of the Attribute is up-voted and exist in the Graph in RAM, to then remove the node "34" and the edge between nodes "1" and "34" from the Graph in RAM. This ensures that the in-memory graph only reflects active and trusted connections.

#### Future Extensions

While the current proof-of-concept focuses on managing connections represented by public key Attributes, future versions of 2WAY could potentially allow for the addition and removal of other types of Attributes or Parents from the Graph in RAM. However, these enhancements are beyond the scope of this proof-of-concept and would require additional considerations for implementation.

In summary, the Graph Manager in the 2WAY system dynamically adjusts the Graph in RAM to reflect changes in connections, ensuring data accuracy and efficient query operations. The use of JSON documents facilitates the management of nodes and edges, highlighting the flexibility and scalability of the system.

<br>

### 2.5.8 Querying Nodes from RAM and Associated Data

Upon receiving the query request from the user, the Graph Manager processes the request by retrieving the relevant nodes from the Graph in RAM. The degree of separation specifies how far the query should traverse from the user's node. For example, if the degree is set to 2, the Graph Manager retrieves nodes that are directly connected to the user's node (first-degree) as well as nodes connected to those nodes (second-degree).

The filtering criteria specified in the query request further refine the results. In the provided example, only nodes representing public key attributes that have been up-voted are retrieved. The original query submitted by the user, for this example, looks as follows:

```json
{
  "object": "attribute",
  "signer": "user_id",
  "app_id": "app_identifier",
  "criteria": {
    "type": "first_name",
    "value": "Alice",
    "degree": 2,
    "vote": 1
  }
}
```

The Graph Manager querys the Graph in RAM with the help of NetworkX and returns a set of nodes, categorized by their degree of separation. The following JSON document exemplifies the query initiated by the user to retrieve nodes from the Graph in RAM:

```json
{
  "signer": "user_id",
  "degree": 2
}
```

In this JSON structure:
- `signer` identifies the user who initiated the query, referenced by their `user_id`.
- `degree` indicates the degree of separation from the user's zeroth degree, set to `2`.

This JSON document illustrates a query operation aimed at retrieving nodes from the Graph in RAM that match the specified criteria. The Graph Manager handles this query, ensuring efficient data retrieval and responsiveness within the 2WAY system.

Upon executing the query described above, the Graph Manager returns an array of integers representing the record IDs of "pubkey" Attributes stored within the Graph in RAM, filtered by a degree of separation of `2` from the user's zeroth degree. Here's an example of how the returned results might look:

```json
{
  "query_result": {
    "degrees": [
      {
        "degree": 1,
        "nodes": [34]
      },
      {
        "degree": 2,
        "nodes": [56, 78, 102]
      }
    ]
  }
}
```

In this JSON structure:
- `query_result` contains the results of the query operation.
- `degrees` is an array that categorizes the results based on different degrees of separation from the user's zeroth degree.

#### Degree 1:
- `degree` specifies the degree of separation, which is `1`.
- `nodes` is an array containing the record IDs of nodes (or "pubkey" Attributes) that are directly connected to the user's zeroth degree. In this case, the array `[34]` indicates that there is one node at degree `1` from the user.

#### Degree 2:
- `degree` specifies the degree of separation, which is `2`.
- `nodes` is an array containing the record IDs of nodes that are two degrees away from the user's zeroth degree. The array `[56, 78, 102]` indicates that there are three nodes at degree `2` from the user.

This JSON document illustrates how the query results are structured to provide information about nodes at different degrees of separation within the 2WAY system. It allows users to understand the connectivity and relationships captured by the system based on their query parameters and degree specifications. The Graph Manager ensures efficient handling and retrieval of these results, supporting seamless navigation and exploration of data within the system.

This data allows the system to identify and further interact with specific nodes within the 2WAY Graph, facilitating efficient navigation and exploration of connections and relationships.

To retrieve the relevant data from the Graph on Disk based on the array of record IDs returned by the Graph Manager, the Storage Manager executes the following query:

```json
{
  "object": "attribute",
  "signer": "user_id",
  "app_id": "app_identifier",
  "criteria": {
    "type": "first_name",
    "value": "Alice",
    "degree": 2,
    "vote": 1,
    "connections": [34, 56, 78, 102]
  }
}
```

In this JSON document:
- `object` specifies the type of object being queried, which is an `attribute`.
- `signer` refers to the user's identifier who initiated the query.
- `app_id` is the identifier for the application.
- `criteria` contains specific parameters for filtering:
  - `type` specifies the type of attribute being queried, in this case, `first_name`.
  - `value` indicates the value to filter by, which is `Alice`.
  - `degree` denotes the degree of separation for the query, set to `2`.
  - `vote` specifies the relevance or importance of the attribute, set to `1`.
  - `connections` is an array of record IDs representing the `pubkey` Attributes retrieved from the Graph in RAM.

This query effectively retrieves data from the Graph on Disk based on the user's original query and the specific "pubkey" Attributes identified in the previous step. The Storage Manager ensures that the queried data matches the specified criteria, providing accurate and relevant results to the user.

The Graph Manager formats this data and sends it back to the frontend interface for user interaction. An example of the JSON document representing the query results might look like this:

```json
{
  "query_result": [
    {
      "signer": "user_id",
      "type": "first_name",
      "value": "Alice",
      "vote": 1,
      "degree": 1,
      "timestamp": 1648062030,
      "hash": "document_hash"
    },
    {
      "signer": "user_id",
      "type": "first_name",
      "value": "Alice",
      "vote": 1,
      "degree": 2,
      "timestamp": 1648062040,
      "hash": "document_hash"
    },
    {
      "signer": "user_id",
      "type": "first_name",
      "value": "Alice",
      "vote": 1,
      "degree": 2,
      "timestamp": 1648062040,
      "hash": "document_hash"
    },
    {
      "signer": "user_id",
      "type": "first_name",
      "value": "Alice",
      "vote": 1,
      "degree": 2,
      "timestamp": 1648062040,
      "hash": "document_hash"
    }
  ]
}
```

This JSON document, `query_result`, contains an array of JSON objects representing attribute data retrieved from the Graph in RAM in response to a user query. Here's a breakdown of each key field:

- `signer`: Indicates the user identifier (`user_id`) who initiated the query.
- `type`: Specifies the type of attribute being queried, which is `first_name`.
- `value`: Represents the specific value associated with the attribute, in this case, "Alice".
- `vote`: Denotes the relevance or importance of the attribute, set to `1`.
- `degree`: Indicates the degree of separation for each attribute from the user's node within the Graph in RAM. For the entries provided:
  - The first object has a degree of `1`, indicating it is directly connected to the user.
  - The subsequent objects have a degree of `2`, indicating they are two degrees away from the user.
- `timestamp`: Represents the timestamp when each attribute data was recorded or updated, using Unix time (`1648062030` and `1648062040` in this example).
- `hash`: Provides the hash of the document, ensuring data integrity and security.

In this example JSON document, the query results consist of Attributes representing the first name "Alice" that are within two degrees of separation from the user's public key and have been upvoted. Each entry in the `query_result` array includes essential information such as the signer, type, value, degree of separation, timestamp, and hash of the document. This data provides a snapshot of the Attributes associated with nodes in the Graph in RAM that match the specified criteria.

To further explore related data, such as the full names associated with each signer returned earlier, another query can be formulated using the `Parent` attribute relationship. For instance, a query could be structured as follows:

```json
{
  "object": "attribute",
  "signer": "user_id",
  "app_id": "app_identifier",
  "criteria": {
    "child_type": "full_name",
    "parent": {
      "type": "pubkey",
      "child_id": [34, 56, 78, 102]
    }
  }
}
```

In this JSON document:
- `object` specifies the type of object being queried, which is an `attribute`.
- `signer` identifies the user who initiated the query.
- `app_id` is the identifier for the application.
- `criteria` specifies the parameters for filtering:
  - `child_type` denotes the type of child attribute being queried, specifically `full_name`.
  - `parent` identifies the parent attribute relationship:
    - `type` specifies that the parent is a `pubkey` attribute.
    - `child_id` is an array of record IDs representing the `pubkey` attributes retrieved from the previous query results.

Executing this query would retrieve additional data from the Graph on Disk, specifically the full names associated with each signer's pubkey attribute that was returned in the initial query. This approach allows for a layered exploration of connected data within the 2WAY system, leveraging relationships defined by attribute types and their hierarchical structure to enrich the user's data retrieval experience.

Alternatively, users could streamline their data retrieval process by formulating a more comprehensive query that incorporates both initial data retrieval and subsequent related data exploration.

#### Future Enhancements

While this proof-of-concept focuses on querying nodes based on public key Attributes and their degrees of separation, future versions of 2WAY could incorporate more advanced querying capabilities. This might include filtering based on additional Attributes or incorporating more complex relationship criteria. However, such enhancements are beyond the scope of this proof-of-concept.

In conclusion, querying nodes from the Graph in RAM in the 2WAY system is a streamlined process that leverages the Graph Manager to handle user queries efficiently. By specifying query parameters and filtering criteria through JSON documents, the system ensures that users receive accurate and relevant data from the in-memory graph, enhancing the overall user experience.

<br>

### **2.5.9 Enforcing Access Control Lists (ACLs)**

The Graph Manager enforces Access Control Lists (ACLs) to regulate permissions when querying, creating, or modifying objects in the database. ACL verification ensures that only authorized users and applications can interact with data, maintaining security and compliance within the 2WAY system. Given that users only query from their own zeroth degree and do not gain access to other users' data through standard queries, ACL enforcement is primarily focused on preventing unauthorized modifications rather than restricting read access.

ACL checks are enforced based on whether an action could impact others, ensuring that unauthorized users cannot make disruptive changes to shared or sensitive data. The Graph Manager automatically determines when ACL verification is required and blocks unauthorized changes before they are written to the database. Additionally, ACLs also regulate which data is shared between users when synchronizing state over the network.

### **When ACLs Should Be Checked**

ACL checks are enforced under conditions where a user’s action could introduce unauthorized changes that affect shared objects or impact other users. They also apply when determining which data should be synchronized with remote users connecting to the system.

#### **1. When creating objects under a parent they don’t own**
If a user attempts to create a new object under a Parent Attribute they don’t own, this could introduce untrusted data into a shared structure.

- Example: A user attempts to add a document under a company profile they don’t have write access to.
- ACL Check: Verify that the user has `write` permissions on the parent object before allowing the new object creation.

An example request for creating a new object:
```json
{
  "object": "attribute",
  "action": "new",
  "signer": "user_id",
  "app_id": "app_identifier",
  "type": "project",
  "value": "Confidential Report",
  "vote": 1
}
```
Before executing the request, the Graph Manager checks whether the `user_id` has permission to create an object of type `project`. If the ACL does not grant `write` access, the request is denied.

#### **2. When modifying or deleting existing objects that affect others**
If an object was created by one user, and another user attempts to modify or delete it, ACLs should be checked to prevent unauthorized changes.

- Example: A user attempts to edit a group’s description or remove another member from a shared project.
- ACL Check: Verify that the user has `edit` or `delete` permissions for the object before allowing modification or deletion.

An example request for modifying an object:
```json
{
  "object": "attribute",
  "action": "edit",
  "signer": "user_id",
  "app_id": "app_identifier",
  "type": "project",
  "value": "Updated Report",
  "vote": 1
}
```
The Graph Manager verifies whether the `user_id` has `edit` access to `project` objects. If access is not granted, the request is rejected.

#### **3. When synchronizing state with a remote user**
When another user connects to a server via the Network Manager, the State Engine determines which objects need to be synchronized. ACLs are checked during this process to ensure that only permitted data is shared.

- Example: Alice creates a `Rating` for an Attribute or adds an Attribute to a Parent she has given her friends access to. When a friend connects to Alice's server, the Network Manager's State Engine checks ACLs to determine if the friend should receive this data.
- ACL Check: Verify that the connected user has `read` permissions for the relevant data before including it in the synchronization process.

An example ACL granting read access:
```json
{
  "id": 1,
  "signer": "alice_id",
  "pubkey_id": "friends_group_id",
  "permissions": {
    "read": ["rating", "profile_data"],
    "write": [],
    "edit": [],
    "delete": []
  },
  "timestamp": 1648062000,
  "hash": "document_hash"
}
```
When Alice's friend connects, the Network Manager's State Engine verifies the ACL and only syncs objects of type `rating` and `profile_data` if the friend belongs to the `friends_group_id`.

#### **4. When querying plugin or system-level data**
If a query involves plugin-managed objects or system-wide data, ACLs should determine whether the user has access to the relevant entries.

- Example: A plugin-created leaderboard ranking should not expose private user scores unless they have access.
- ACL Check: Ensure that the user has `read` access to the requested plugin or system-level data.

An example request for querying plugin data:
```json
{
  "object": "attribute",
  "signer": "user_id",
  "app_id": "hashed_plugin_identifier",
  "criteria": {
    "type": "high_score",
    "degree": 1,
    "vote": 1
  }
}
```
Before returning the results, the Graph Manager verifies that the user has `read` permissions for `high_score` objects within the given plugin.

### **When ACLs Are NOT Checked**

ACL checks are not necessary in cases where the user’s action cannot affect anyone else or when implicit ownership applies.

#### **1. When querying one’s own zeroth-degree objects**
Since users only query data from their own zeroth degree, they do not gain access to another user's private data through queries.

- Example: A user searches for their own stored contacts, messages, or reputation scores.
- No ACL Check Needed because the user already has implicit access.

#### **2. When modifying or deleting objects they personally created**
A user should always be able to modify or delete an object they themselves created, unless ACLs explicitly restrict self-editing (which would be an exceptional case).

- Example: A user edits their own profile information or removes their own post.
- No ACL Check Needed because the user has implicit ownership over their own objects.

#### **3. When a local administrator performs an action**
Users designated as local administrators should have unrestricted access and bypass ACL checks entirely.

- Example: A system admin needs to delete or modify any user-generated object for moderation purposes.
- No ACL Check Needed since admins have full system control.

### **ACL Structure and Enforcement**
ACL records define access rules by linking user public keys to specific objects and specifying permission levels. Each ACL record follows this format:
```json
{
  "id": 1,
  "signer": "admin_user_id",
  "pubkey_id": "target_user_id",
  "permissions": {
    "read": ["type_1", "type_2"],
    "write": ["type_3"],
    "edit": ["type_4"],
    "delete": []
  },
  "timestamp": 1648062000,
  "hash": "document_hash"
}
```
- `pubkey_id`: The user receiving permissions.
- `permissions`: Lists of object types the user can `read`, `write`, `edit`, or `delete`.

ACL enforcement occurs before the Storage Manager writes to disk, ensuring unauthorized changes are blocked at the Graph Manager level. The Network Manager's State Engine also applies ACL checks when determining which objects should be synchronized with remote users. However, administrators on the local system are exempt from ACL checks and have unrestricted access.

### **Summary: When ACLs Are Enforced**
| **Action Type** | **ACL Check?** | **Reasoning** |
|--------------|------------|------------------|
| Querying own data | ❌ No | Users can only query from their own zeroth degree, preventing unauthorized access to others' data. |
| Creating objects under own parent | ❌ No | Users have implicit ownership over their own objects. |
| Creating objects under a parent owned by another user | ✅ Yes | Prevents unauthorized additions to shared objects. |
| Modifying or deleting own objects | ❌ No | Users should be allowed to edit or delete what they created. |
| Modifying or deleting objects owned by another user | ✅ Yes | Prevents unauthorized edits to shared objects. |
| Querying plugin/system data | ✅ Yes | Ensures proper permissions for accessing plugin-managed data. |
| Syncing data with another user | ✅ Yes | The Network Manager's State Engine checks ACLs before sending data to a remote user. |
| Admin actions | ❌ No | Admins should always have full access. |

### **Conclusion**
ACLs are enforced for write, modification, and data synchronization operations, ensuring that only authorized users can change shared objects or access remote data. Queries within a user's own zeroth-degree scope do not require ACL enforcement. The Network Manager's State Engine applies ACLs during data synchronization to prevent unauthorized data sharing between users.

By applying ACL checks selectively, the system maximizes security while minimizing unnecessary overhead, ensuring a balance between access control and efficiency.

<br><br>

## 2.6 Storage Manager <a name="26-storage-manager"></a>

### 2.6.1 Introduction to the Storage Manager

The Storage Manager is responsible for maintaining the integrity, persistence, and efficient retrieval of data within the 2WAY system. It acts as the interface between the Graph in RAM, maintained by the Graph Manager, which handles dynamic interactions, and the Graph on Disk, where all data is stored permanently. The primary role of the Storage Manager is to ensure that every change to the system is properly recorded, retrieved when needed, and protected from inconsistencies.

The Storage Manager dynamically creates and maintains tables for plugins based on their unique `app_id` values, ensuring that each plugin operates within its own isolated namespace while still integrating seamlessly with the rest of the system. When a new plugin is introduced, the Storage Manager automatically generates tables corresponding to the required object types, such as Attributes, Parents, Edges, Ratings, and ACLs. This structure prevents naming conflicts between different plugins and ensures that stored data remains logically separated. By associating each table with a specific `app_id`, the system enables plugins to function independently while still interacting with shared components like the Graph Manager and Access Control Lists. This approach allows plugins to extend the system’s functionality without interfering with core data structures or other plugins, making 2WAY highly modular and adaptable.

When a user creates, modifies, or deletes an object, the Graph Manager processes the request and determines whether the change should be written to the database. The Storage Manager then handles the actual storage operation, ensuring that the update is committed correctly. This ensures that even if the system is restarted, the latest state of the graph remains intact. The Storage Manager also works closely with the Log Manager when certain changes require logging, particularly those involving modifications to sensitive objects.

Retrieval is equally important to the Storage Manager’s role. Users do not query the Graph on Disk directly. Instead, they query the Graph Manager, which holds the Graph in RAM; an optimized version of the network structure for fast lookups. When additional details are required beyond what is stored in memory, the Storage Manager retrieves the requested data from disk and returns the relevant objects. This approach balances speed and efficiency, ensuring that common queries are handled rapidly while deeper queries can access the full dataset without unnecessary delays.

Since the 2WAY proof-of-concept is implemented in Flask, and uses SQLite3 by default, the Storage Manager is designed to operate without external dependencies or additional setup. The database schema follows a structured design that prevents naming conflicts between plugins and ensures that all stored data remains logically separated. Each object type, whether an Attribute, Parent, Edge, Rating, or ACL, has a designated storage table that aligns with the overall structure of the system. This organization allows for clear relationships between objects, making queries more efficient and ensuring that the integrity of the database is preserved.

The Storage Manager must also support changes to the Graph in RAM. When objects are added or removed from the graph, the corresponding updates must be reflected in storage. The Storage Manager ensures that the latest modifications are written to disk, but it does not dictate how the Graph Manager structures in-memory relationships. The two systems work together, with the Graph Manager determining which data should be present in memory and the Storage Manager ensuring that all persistent records remain accurate.

The Storage Manager is also responsible for handling database cleanup when necessary. While the system does not automatically delete objects unless explicitly requested, some objects may become irrelevant due to downvotes or aging data. Future implementations may include automated pruning processes to remove obsolete records and optimize performance. For now, the Storage Manager ensures that even outdated data remains available unless specifically removed, allowing users to retrieve historical information when needed.

Security is another key function of the Storage Manager. Since stored data includes cryptographic attributes and access control settings, the database must remain tamper-proof and resistant to corruption. The Storage Manager ensures that stored records cannot be altered without proper authorization. It works in conjunction with the Key Manager when cryptographic signing is required, ensuring that signed logs remain verifiable and unaltered.

The Storage Manager’s role is foundational to the 2WAY system. Without it, data persistence would not be possible, and the in-memory graph would lose all structure on restart. By ensuring that every object is recorded, retrieved, and managed efficiently, the Storage Manager provides stability and consistency across the entire platform. It is the underlying system that allows all graph-based interactions to function seamlessly, bridging the gap between real-time memory operations and long-term data storage.

<br>

### 2.6.2 Storage Engine

The Storage Engine is the core component of the Storage Manager responsible for writing, retrieving, and maintaining data in the 2WAY system’s persistent storage. It ensures that objects created by users, plugins, and system processes are correctly structured, indexed, and accessible when needed. The Storage Engine is designed for reliability, efficiency, and modularity, allowing the system to handle both high-frequency interactions in the Graph in RAM and long-term data persistence in the Graph on Disk.

All interactions with the database pass through the Storage Engine. When an object is created, modified, or deleted, the Storage Manager generates a structured SQL operation that ensures the change is correctly committed. The database schema is optimized for the structure of the 2WAY graph, with tables dedicated to specific object types, including Attributes, Parents, Edges, Ratings, and ACLs. Each table is further isolated by the `app_id of the plugin responsible for managing the data, preventing naming conflicts and ensuring that plugins function independently.

The Storage Engine prioritizes data integrity and transactional consistency. All write operations are executed within atomic transactions, ensuring that changes are either fully committed or completely rolled back in the event of an error. This mechanism prevents data corruption and ensures that the system remains in a consistent state even in the event of unexpected failures. Transactions are particularly important when modifying multiple related objects, such as updating a Parent and its associated Attributes simultaneously.

Since the 2WAY system primarily relies on SQLite3 for storage, the Storage Engine takes advantage of SQLite’s lightweight design and minimal setup requirements. By embedding the database directly into the application, the Storage Engine eliminates the need for an external database server, making deployment and maintenance simpler while ensuring that the entire system remains self-contained. The database schema is structured for efficient querying and indexing, with indexes applied to frequently accessed fields such as public key Attributes, timestamps, and relationships between Parents and their child objects. These optimizations reduce query latency and improve the system’s responsiveness.

The Storage Engine supports sequential writes and batch processing for operations that involve multiple objects at once. When large updates occur, such as importing a dataset or syncing a plugin’s objects, the Storage Engine processes transactions in batches, reducing the performance impact on the system. This ensures that storage operations do not become a bottleneck, even when handling complex queries or large datasets.

When retrieving data, the Storage Engine processes queries efficiently by filtering based on criteria such as object type, degree of separation, and ACL permissions. If a user requests data from their own zeroth degree, the Storage Engine retrieves the relevant records directly. If deeper queries require retrieving linked objects, the Storage Manager optimizes these queries to return the minimal necessary dataset, reducing unnecessary disk reads. Queries that involve parent-child relationships leverage SQL joins to return structured results without redundant queries.

For system-wide optimizations, the Storage Engine includes mechanisms for database vacuuming and indexing maintenance. Over time, as objects are modified and deleted, the underlying SQLite database can accumulate fragmentation that slightly impacts performance. The Storage Engine periodically compacts the database to optimize storage efficiency and ensure fast query performance. Future enhancements may introduce scheduled background maintenance tasks to further optimize indexing and reduce storage overhead.

Security is an integral part of the Storage Engine’s design. Since data includes cryptographic keys, signatures, and ACLs, the Storage Engine ensures that all stored records are tamper-resistant and cryptographically verifiable. The database enforces access controls to prevent unauthorized modifications, and in cases where signed logs are required, the Storage Engine interacts with the Key Manager to ensure that each modification is properly signed before it is written to disk. This approach guarantees that any modifications to critical objects remain auditable and that unauthorized changes are automatically rejected.

The Storage Engine is built to support future scalability. While SQLite3 serves as the default storage backend in the proof-of-concept, the underlying database schema and query structure allow for potential expansion to more advanced storage solutions in future versions. If higher scalability or distributed storage is required, the Storage Engine can be adapted to support alternative database backends while preserving the same logical data model.

By maintaining an efficient, secure, and modular approach to data storage, the Storage Engine ensures that 2WAY remains a robust platform for decentralized interactions. It provides the essential foundation for long-term data persistence, ensuring that every object remains accessible, verifiable, and efficiently stored while seamlessly integrating with the rest of the system.

<br>

### 2.6.3 Creating Databases and Tables

### 2.6.4 Data Storage and Manipulation

### 2.6.5 Data Retrieval

<br>

## 2.7 Key Manager <a name="27-key-manager"></a>

### 2.7.1 Introduction to the Key Manager

The Key Manager within the 2WAY system is designed to securely generate, manage, and utilize cryptographic keys for users, underpinning the system's robust security architecture. It facilitates a range of cryptographic operations such as key generation, signature verification, message signing, encryption, and decryption, ensuring the integrity, authenticity, and confidentiality of user interactions. Additionally, the Key Manager plays a critical role in signing logs and verifying messages between servers, ensuring secure and verifiable communication across the network.

Each user within the 2WAY system can manage multiple cryptographic key-pairs, supporting a variety of applications under a single identity. This is achieved through the implementation of Hierarchical Deterministic (HD) Keys, which create a structured, tree-like hierarchy where a single master key can generate multiple child keys. This structure simplifies key management, enabling users to derive new keys as needed without compromising the security of the master key.

Hierarchical Deterministic Keys are essential for maintaining an organized and efficient key management system. Each derived key serves a unique purpose and is cryptographically linked to the master key, providing a secure means to handle multiple cryptographic tasks. For instance, users can employ one key for authenticating their identity, another for signing messages, and additional keys for interactions with trusted third parties. This hierarchical approach compartmentalizes cryptographic functions, enhancing both security and usability.

In this proof-of-concept, message signing on the frontend is not supported. Future versions may introduce frontend or hardware key signing for added security.

The Key Manager also incorporates Zero-Knowledge Proofs (ZKPs), a powerful cryptographic technique that allows users to prove the validity of certain information without revealing the information itself. ZKPs are integral to preserving privacy and security within the 2WAY system, enabling secure user authentication, transaction verification, and protected communications. By leveraging ZKPs, the Key Manager ensures that sensitive information remains confidential and is not exposed during verification processes.

Integration with the parent-child relationships within the 2WAY system further enhances the functionality of the Key Manager. Users can manage their keys effectively by aligning them with these relationships, using a primary key for identity verification and secondary keys for specific tasks like message signing or encryption. This hierarchical and relational approach streamlines key management and strengthens security by isolating different cryptographic functions.

The Key Manager provides seamless integration for key generation, ensuring that keys are securely created and stored. For message signing and verification, the Key Manager uses advanced algorithms to maintain the authenticity and integrity of communications. It also signs messages before they are sent to another server, ensuring that messages can be cryptographically verified upon receipt. Additionally, the Key Manager helps with encrypting messages before transmission, providing confidentiality so that intercepted communications remain unreadable to unauthorized parties. These cryptographic mechanisms are also used when objects require verification before being written to disk, particularly in cases where logs must be cryptographically signed to prevent tampering.

Revocation and re-issuance of keys are crucial functionalities supported by the Key Manager. In the event of key compromise or the need for key updates, the Key Manager facilitates the revocation of the old key and the issuance of a new one. This process is critical for maintaining the long-term security and reliability of the 2WAY system, ensuring that users can continue their interactions securely without disruption. Key revocation also propagates through the system, ensuring that all relevant parties are aware of compromised keys and preventing unauthorized access.

In summary, the Key Manager is a pivotal component of the 2WAY system, providing comprehensive cryptographic support to secure and streamline user interactions. By implementing Hierarchical Deterministic Keys and Zero-Knowledge Proofs, the Key Manager ensures robust key management, secure communications, and effective integration with the hierarchical structure of the 2WAY system. It enforces cryptographic integrity across user interactions and inter-server communication, safeguarding all operations against unauthorized modifications or forgery.

<br>

### 2.7.2 Generate Keys

### 2.7.3 Verify Signatures

### 2.7.4 Sign Messages

### 2.7.5 Encrypt Messages

### 2.7.6 Decrypt Messages

### 2.7.7 Revocation and Re-Issuance of Keys

<br>

## 2.8 Log Manager <a name="28-log-manager"></a>

### 2.8.1 Introduction to the Log Manager

The Log Manager is a critical component of the 2WAY system, responsible for ensuring the integrity, reliability, and security of the platform by recording and managing logs of operational activities. It serves as the central repository for logging system events, including successful operations, errors, warnings, and other significant occurrences. This logging mechanism is essential for maintaining system health, diagnosing issues, and providing an audit trail for security and compliance.

The Log Manager integrates with multiple components, including the Network Manager, the Bastion Engine, the Graph Manager, the Storage Manager, and the Key Manager. It ensures that all significant events, particularly those involving failed operations, failed Bastion messages, and failed incoming and outgoing messages, are logged and preserved for future reference.

One of its primary functions is logging failed operations within the system. These failures can range from minor warnings to critical errors that may affect functionality. By capturing these events, the Log Manager provides valuable insights into system performance, helping administrators diagnose and resolve issues before they impact stability. Effective logging contributes to system reliability by identifying patterns of failure and enabling proactive maintenance.

Another crucial function is logging failed Bastion messages. The Bastion Engine, a core part of the Network Manager, establishes secure connections between servers using client-puzzle challenges to mitigate Denial of Service attacks. The difficulty of these puzzles adjusts dynamically based on incoming connections. If a client-puzzle challenge fails or a Bastion message is not delivered, the Log Manager records the failure, ensuring that authentication issues can be analyzed and addressed.

The Log Manager also captures logs of failed incoming and outgoing messages handled by the Network Manager. After a server successfully authenticates a connection through the Bastion Engine, the Incoming Engine and Outgoing Engine manage message transmission. These components ensure secure and reliable communication between users and servers. If a message fails to send or receive due to network disruptions, server errors, or other failures, the Log Manager records the event. These logs provide administrators with visibility into communication issues and allow them to investigate problems that may affect data flow.

Beyond system monitoring, the Log Manager powers the platform-wide notification system, which consolidates all user notifications into a single, filterable feed. Every user action that results in a notification, such as a new post appearing in a social feed, a completed marketplace transaction, or a friend sharing media, is first logged. These logs are then processed to generate user-facing notifications that appear within the unified notification center. Because notifications originate from logged events rather than separate mechanisms, the system ensures consistency across all plugins and interactions. This allows users to view, filter, and manage all their notifications from a single interface, whether they relate to social activity, financial transactions, or other interactions within the 2WAY system.

The Log Manager follows best practices in logging and monitoring, ensuring that logs are comprehensive, secure, and easily accessible to authorized personnel. Logs are timestamped and include metadata such as the source of the log entry, the type of event, and relevant context. This level of detail is essential for effective troubleshooting and forensic analysis, allowing administrators to trace issues back to their origin and implement corrective actions.

Security is a key consideration in the design of the Log Manager. Logs may contain sensitive information, so they must be protected from unauthorized access and tampering. The Log Manager employs encryption and access controls to safeguard log data, ensuring that only authorized personnel can view or modify logs. These protections preserve log integrity, preventing malicious alterations that could obscure critical security events.

The Log Manager also supports integration with external monitoring and alerting systems, enabling real-time oversight of the 2WAY platform. By feeding log data into external monitoring tools, administrators can set alerts for specific events or patterns, allowing them to respond quickly to potential threats or operational issues before they escalate.

The Log Manager is a fundamental component of the 2WAY system, providing a structured approach to logging that enhances system stability, security, and transparency. By recording failed operations, failed Bastion messages, and failed incoming and outgoing messages, it ensures that administrators have the necessary data to maintain system performance. Its adherence to strict security and logging best practices makes it an essential part of the 2WAY infrastructure. Additionally, by serving as the backbone for the system-wide notifications stream, it enables users to stay informed about relevant events across all plugins and interactions in a unified, structured manner.

<br>

### 2.8.2 Logging Failed Operations

### 2.8.3 Logging Failed Bastion Messages

### 2.8.4 Logging Failed Incoming Messages

<br>

## 2.9 Network Manager <a name="29-network-manager"></a>

### 2.9.1 Introduction to the Network Manager

The Network Manager is a pivotal component of the 2WAY system, responsible for managing network connections, ensuring data integrity, and facilitating secure communication between servers. Within the 2WAY infrastructure, it oversees the establishment, maintenance, and security of network interactions, ensuring that data flows seamlessly and securely between interconnected servers. This role is critical for maintaining the overall health and efficiency of the network, enabling the system to function as a cohesive and resilient platform.

At its core, the Network Manager handles the complexities of networking by leveraging advanced protocols and network topologies to enable efficient and secure data routing. Servers within the 2WAY system only connect to other servers that are part of the Server Graph, a dynamic structure that defines relationships between trusted servers. To establish a connection, a server must possess the public key of at least one user associated with the target server and its Onion address. The Onion address, a key feature of the Tor network, ensures anonymity and encrypted communication. When this address is stored as a child attribute of a pubkey parent attribute, the server attempts to initiate a connection.

The process of establishing a connection involves several critical steps managed by the Network Manager. Initially, servers communicate through their Bastion Engine, which verifies connections using client-puzzle challenges. These puzzles mitigate Denial of Service (DoS) attacks by requiring computational effort before authentication, preventing attackers from overwhelming the system with requests. The difficulty of these puzzles adjusts dynamically based on incoming traffic, increasing protection under high load. Once a server successfully solves a client puzzle, it sets up a connection to a second Onion address. The Incoming Engine and Outgoing Engine communicate over this second Tor connection, ensuring that established communication channels remain functional even if the DoS Guard Manager is actively mitigating an attack on the primary Bastion connection.

The State Engine plays a crucial role in maintaining and synchronizing network-wide state data. It ensures that all connected servers share a consistent and up-to-date view of stored objects, resolving conflicts when discrepancies arise. The State Engine enables querying and state-sharing between servers, supporting efficient data synchronization and preserving network integrity.

Another core component is the Network Engine, responsible for managing network services and ensuring efficient inter-server communication. This engine handles the creation, activation, suspension, and revocation of Onion services, which are essential for maintaining secure and anonymous peer-to-peer connections. Additionally, the Network Engine manages socket connections, ensuring reliable transmission and reception of encrypted data.

The Bastion Engine strengthens the network’s defense against attacks by monitoring incoming traffic, detecting threats, and working alongside the DoS Guard Manager to mitigate DoS attempts. The DoS Guard Manager generates and verifies client puzzles to prevent malicious traffic. If a server detects a DoS attack targeting its Bastion Engine, it revokes the compromised Onion service, generates a new one, and updates its connected peers through the Outgoing Engine.

The Incoming Engine and Outgoing Engine are responsible for handling inbound and outbound network traffic, respectively. The Incoming Engine processes received messages, applying filtering, queuing, and routing before delivering them to their appropriate destinations. The Outgoing Engine ensures that messages are properly formatted, encrypted, and transmitted, facilitating secure and uninterrupted communication between users and servers. These engines play a vital role in maintaining message integrity and timely delivery across the network.

The Network Startup Engine is responsible for initializing network connections and services during system startup. It facilitates the creation and solving of client puzzles, ensuring that servers authenticate their first-degree connections before allowing further interaction. This engine is critical for bootstrapping the network and ensuring that all necessary services are operational from the moment the system starts.

Overall, the Network Manager is integral to the 2WAY system, providing a robust framework for managing network connections, securing data transmissions, and ensuring the seamless operation of inter-server communications. By leveraging networking best practices, cryptographic security, and adaptive defense mechanisms, the Network Manager ensures that the 2WAY system remains resilient, efficient, and highly secure, supporting decentralized and interconnected environments with minimal trust dependencies.

<br>

### 2.9.2 Networking
The networking architecture of the 2WAY system is designed to facilitate secure, anonymous, and efficient communication between servers while maintaining a decentralized structure. It employs a combination of cryptographic identity verification, onion routing, and dynamic network graph mapping to enable seamless interactions between trusted nodes. The Network Manager ensures that all communication occurs over encrypted channels and that connections are only established between mutually authenticated servers.

At the foundation of 2WAY’s networking model is the Server Graph, which defines the relationships between interconnected servers. Each server maintains a local subset of the Server Graph that includes the public keys and Onion addresses of the servers it has permission to connect with. This graph-based approach eliminates the need for centralized coordination while ensuring that only authenticated servers participate in the network. A server does not broadcast its existence to unknown peers but instead relies on previously established trust relationships to facilitate node discovery.

For a server to initiate communication with another server, it must possess a public key Attribute that corresponds to a user account on the target server, along with the server’s Onion address, which is stored as a child attribute of that public key. These attributes are retrieved from the Graph Manager, ensuring that only pre-approved connections are attempted. When a server attempts to connect, it first reaches out to the target’s Bastion Engine, which authenticates the request using a client-puzzle challenge before allowing further interaction. This challenge-response mechanism protects against Denial of Service attacks by requiring the requesting server to perform computational work before the connection is accepted.

Once authentication is successful, the two servers establish a second, separate Onion service dedicated to handling encrypted communication. This design prevents ongoing communications from being disrupted if the Bastion Engine is under attack, as all application-layer data transmission occurs over the secondary connection. The Incoming Engine and Outgoing Engine handle message exchange over this secure channel, ensuring reliable and confidential communication.

Data routing within the 2WAY system follows a peer-to-peer model where each server only communicates directly with its known peers. There is no global broadcast mechanism, reducing the risk of metadata leaks and preventing network-wide disruptions. When a server needs to query data beyond its immediate peers, it sends requests through multi-hop relay paths defined by its existing trust relationships. The degree of separation in the Server Graph determines how far a request can propagate, ensuring that queries do not extend beyond the intended scope.

Message confidentiality and integrity are maintained through end-to-end encryption at multiple layers. Before being transmitted, messages are signed using the sender’s cryptographic key to ensure authenticity. The message payload is then encrypted to prevent interception, ensuring that only the intended recipient can decrypt its contents. This encryption model applies to both user-generated content and system-level messages exchanged between servers.

The 2WAY proof-of-concept leverages the Tor network for anonymous and encrypted communication, utilizing Onion services to obscure metadata and ensure decentralized routing. However, the underlying architecture is designed to be flexible. Tor can be replaced with alternative networking technologies such as I2P, Yggdrasil, or any other peer-to-peer encrypted transport layer that supports anonymous and secure connections. The modular nature of the Network Manager allows for easy adaptation, meaning future implementations could swap out Tor for a different networking stack depending on performance, security, or decentralization preferences.

The 2WAY system also implements adaptive traffic routing to mitigate censorship and improve resilience. If a server detects that a direct connection to one of its peers is unavailable, it can attempt to reach the same server through an alternative route, leveraging the indirect paths defined by the Server Graph. This enables communication continuity even if some nodes become temporarily unreachable.

By combining cryptographic authentication, onion routing, and a graph-based network structure, the 2WAY system ensures that all connections remain secure, private, and resistant to attacks. The decentralized nature of the network eliminates reliance on any single point of failure, allowing servers to operate independently while still maintaining trusted communication paths.

<br>

### 2.9.3 Establishing Connections
Details on how connections are established between nodes, including the handshake process, encryption protocols, and authentication mechanisms.

### 2.9.4 State Engine and Data Synchronization

#### 2.9.4.1 Introduction to the State Manager
Overview of the State Manager, describing its role in maintaining and synchronizing the state across the network.

#### 2.9.4.2 State Engine
Technical details on the State Engine, including how it processes state changes, manages state conflicts, and ensures consistency.

#### 2.9.4.3 Querying States
Methods for querying the current state of the network or specific nodes, including API endpoints and data formats.

#### 2.9.4.4 Sharing States
Mechanisms for sharing state information between nodes, including synchronization protocols and data dissemination strategies.

### 2.9.5 Network Engine

#### 2.9.5.1 Introduction to the Network Engine
Overview of the Network Engine, highlighting its role in managing network services and ensuring efficient communication.

#### 2.9.5.2 Creating Onion Services
Step-by-step guide to creating Onion Services for anonymous and secure communication within the network.

#### 2.9.5.3 Starting Onion Services
Instructions on how to start Onion Services, including configuration options and common issues.

#### 2.9.5.4 Stopping Onion Services
Procedure for safely stopping Onion Services without disrupting ongoing communication.

#### 2.9.5.5 Revoking Onion Services
Details on how to revoke Onion Services, including security considerations and best practices.

#### 2.9.5.6 Closing Sockets
Explanation of socket management, including how to gracefully close sockets to avoid data loss.

#### 2.9.5.7 Receiving Messages
Technical details on how the Network Engine handles incoming messages, including parsing, validation, and processing.

#### 2.9.5.8 Sending Messages
Overview of the message-sending process, including formatting, encryption, and delivery assurance.

### 2.9.7 Bastion Engine

#### 2.9.7.1 Introduction to the Bastion Engine
An introduction to the Bastion Engine, describing its role in fortifying the network against attacks and ensuring robust security.

#### 2.9.7.2 Receiving Messages
Details on how the Bastion Engine processes incoming messages, including threat detection and response mechanisms.

### 2.9.8 Incoming Engine

#### 2.9.8.1 Introduction to the Incoming Engine
Overview of the Incoming Engine, highlighting its importance in handling inbound network traffic.

#### 2.9.8.2 Receiving Messages
Technical details on how the Incoming Engine processes incoming messages, including filtering, queuing, and routing.

### 2.9.9 Outgoing Engine

#### 2.9.9.1 Introduction to the Outgoing Engine
Introduction to the Outgoing Engine, explaining its role in managing outbound network traffic.

#### 2.9.9.2 Sending Messages
Overview of the process for sending messages through the Outgoing Engine, including scheduling, prioritization, and delivery confirmation.

### 2.9.10 Network Startup Engine

#### 2.9.10.1 Introduction to the Network Startup Engine
Overview of the Network Startup Engine, describing its role in initializing network connections and services.

#### 2.9.10.2 Creating and Solving Client Puzzles
Details on the use of client puzzles for preventing DoS attacks, including how they are created and solved during the startup process.

#### 2.9.10.3 Starting Onion Services
Instructions on how to initiate Onion Services during network startup, including configuration and troubleshooting.

#### 2.9.10.4 Connecting with First Degree Connections
Explanation of how the system establishes connections with first-degree nodes during startup, ensuring reliable and secure initial networking.

### 2.9.11 DoS Guard Manager

#### 2.9.11.1 Introduction to the DoS Guard Manager
Overview of the DoS Guard Manager, highlighting its importance in protecting the network from denial-of-service attacks.

#### 2.9.11.2 Introduction to the Client Puzzle Engine
Introduction to the Client Puzzle Engine, explaining how it generates puzzles to mitigate DoS attacks.

#### 2.9.11.3 Creating and Solving Client Puzzles
Technical details on the creation and solving of client puzzles, including algorithms and complexity considerations.

#### 2.9.11.4 Querying and Verifying Client Puzzle Challenges and Solutions
Methods for querying and verifying client puzzle challenges and solutions to ensure their effectiveness in preventing DoS attacks.

#### 2.9.11.5 DoS Guard Engine
Overview of the DoS Guard Engine, describing its role in monitoring and responding to potential DoS attacks.

#### 2.9.11.6 Receiving Bastion Engine Alarms
Explanation of how the DoS Guard Manager processes alarms from the Bastion Engine and coordinates defensive actions.

<br><br>

# 3. Practical Examples <a name="practical-examples"></a>

<br>

## 3.1 Introduction to the Practical Examples
The 2WAY system is designed to be a versatile and decentralized solution for identity, reputation, and access management. This section provides a collection of real-world examples demonstrating how 2WAY can be applied across different industries and use cases. These examples illustrate its flexibility in managing secure communications, verifying identities, preventing fraud, and facilitating trust between users in a peer-to-peer environment.

Each example highlights a specific aspect of the system's functionality, such as contact management, secure messaging, key revocation, and decentralized market transactions. By following these practical scenarios, users and developers can gain a deeper understanding of how 2WAY operates and how it can be adapted to meet unique requirements.

Whether used for managing social connections, preventing Sybil attacks, or verifying digital assets, 2WAY provides a robust framework that prioritizes privacy, security, and decentralization. The following sections will walk through these use cases in detail, explaining how 2WAY's core components interact to create a reliable and tamper-resistant system.

<br>

## 3.2 Installing 2WAY

The 2WAY system is designed for ease of installation, requiring minimal setup to get started. With a web-based installation wizard handling the initial configuration, users can quickly deploy their server and begin using 2WAY without worrying about complex backend setup. This guide will walk through the installation process, covering prerequisites, installation steps, and troubleshooting tips.  

#### **Prerequisites**

Before installing 2WAY, ensure that your system meets the following requirements:  

- **Operating System**: Linux, macOS, or Windows
- **Python**: Version 3.10 or later
- **Pip**: Latest version of Python package manager
- **Tor**: Required for secure, decentralized networking (optional but recommended)
- **Git**: Needed if installing from a source repository  

#### **Installation Steps**

1. **Clone the Repository (Optional, if installing from source)**  
   If you're installing from a GitHub repository, clone it using:  

   ```sh
   git clone https://github.com/livegnik/2WAY.git
   cd 2WAY
   ```

2. **Set Up a Virtual Environment (Recommended)**  
   Using a virtual environment keeps dependencies isolated. Run:  

   ```sh
   python -m venv venv
   source venv/bin/activate  # macOS/Linux
   venv\Scripts\activate     # Windows
   ```

3. **Install Dependencies**  
   The system requires several Python packages. Install them using the `requirements.txt` file:  

   ```sh
   pip install -r requirements.txt
   ```

4. **Run 2WAY for the First Time**  
   Start the server:

   ```sh
   python run.py
   ```
   Start the server on windows:

   ```sh
   start.bat
   ```

   This will initialize the system and launch the web-based installation wizard.

5. **Complete the Web-Based Installation Wizard**  
   Once the server is running, open a browser and navigate to:  

   ```
   http://localhost:5000
   ```

   The setup wizard will guide you through:  
   - Setting up a secure administrator account  
   - Configuring network and privacy settings  
   - Enabling/disabling plugins  
   - Setting up Tor (optional)  

   After completing the wizard, you will be redirected to the 2WAY dashboard, where you can further configure your system, install custom plugins, add contacts, and start interacting with the network.

#### **Post-Installation Setup**  

- Access the Dashboard: Once setup is complete, log into the dashboard to manage your identity, contacts, and applications.  
- Enable/Disable Plugins: Configure built-in plugins or install custom ones to extend 2WAY’s functionality.  
- Connect with Other Users: Add contacts and start using decentralized applications such as social feeds, markets, and messaging.  
- Explore the various features of 2WAY, including:
  - Secure end-to-end encrypted messaging
  - Graph-based social feeds and content discovery
  - Trust-based market participation
  - Key management and cryptographic verification 

With 2WAY up and running, you’re ready to take full control of your digital identity and decentralized interactions!

<br>

## 3.3 Managing Contacts

In the 2WAY system, managing contacts is fundamental to establishing trust-based interactions. Users can add, edit, and remove contacts while also organizing them into groups for better control over their network. Since 2WAY operates as a decentralized, cryptographic identity system, all contacts are stored securely within the 2WAY Graph, allowing users to manage their digital relationships while maintaining privacy and security.  

### **3.3.1 Adding Contacts**  

To add a new contact, users need the contact’s public key (pubkey) and optionally their Onion address (if they use Tor for networking). The system ensures that contacts are verified cryptographically before establishing a trusted connection.  

#### **Steps to Add a Contact**  

1. **Navigate to Contacts in the Dashboard**  
   - Open the 2WAY dashboard and go to the Contacts section.  
2. **Click "Add Contact"**  
   - Enter the contact’s public key (required).  
   - If available, enter their Onion address to enable direct communication.  
3. **Assign a Display Name & Group (Optional)**  
   - Set a recognizable name.  
   - Organize contacts by assigning them to a group (e.g., Friends, Family, Work, Communities).  
4. **Send an Invitation (Optional)**  
   - If the contact is known to use 2WAY, you can send an invitation request, allowing them to acknowledge the connection.  
5. **Verify Contact**  
   - Once added, the contact is stored as a node in the 2WAY Graph.  
   - If mutual verification is required, they will need to add your pubkey as well.  

### **3.3.2 Editing Contacts**  

Contacts can be modified at any time to update their display name, group, or additional attributes such as notes.  

#### **Steps to Edit a Contact**  

1. Open the Contacts List  
2. Select a Contact and Click “Edit”  
3. Modify Contact Information  
   - Update the display name, group, or additional metadata.  
   - If a contact has changed their Onion address, update it accordingly.  
4. Save Changes  

Changes are immediately reflected in the 2WAY Graph and affect how the contact appears in all related applications, including messaging and reputation tracking.  

### **3.3.3 Removing Contacts**  

If a contact is no longer relevant, they can be removed, revoking their access to previously shared data (depending on Access Control List permissions). Removing a contact does not delete their existence in the 2WAY Graph but simply disassociates them from your personal graph.  

#### **Steps to Remove a Contact**  

1. Navigate to Contacts in the Dashboard  
2. Select the Contact to Remove  
3. Click "Remove Contact"  
   - A confirmation dialog will appear to prevent accidental deletions.  
4. Confirm the Action  

Once removed, the contact will no longer appear in the user’s network. However, if a user wishes to reinstate the contact, they will need to add them again manually.  

### **3.3.4 Organizing Contacts into Groups**  

2WAY allows users to group contacts for easier access and management. These groups can also play a role in reputation filtering, social feeds, and message visibility.  

#### **Default Groups**  
- Friends: Close personal connections.  
- Family: Trusted family members.  
- Work: Professional contacts and colleagues.  
- Communities: Groups related to social or professional interests.  

#### **Custom Groups**  
Users can create custom groups, such as:  
- Verified Buyers (for marketplaces)  
- Trusted Reviewers (for content validation)  
- Developers (for open-source collaboration)  

Each contact can belong to multiple groups, making it easy to organize connections based on context.  

#### **Steps to Assign Contacts to Groups**  

1. Go to the Contacts Section  
2. Select a Contact  
3. Choose "Edit" and Assign to a Group  
4. Save Changes  

Groups can be used for filtering social feeds, managing who sees posts, and prioritizing messages from trusted contacts.  

### **3.3.5 Managing Personal Identities (Personas)**  

The 2WAY system is designed to support multiple cryptographic identities, allowing users to maintain separate **personas** for different purposes, such as keeping work and personal identities distinct. Each persona functions as an independent public key identity, ensuring privacy and compartmentalization across various interactions.  

#### **Personas in the Proof-of-Concept**  

While the 2WAY architecture allows for seamless management of multiple identities, the current proof-of-concept does not yet include a built-in persona-switching feature. Instead, users must log out and log back in with a different cryptographic identity to switch between personas.  

#### **Using Multiple Identities in the Proof-of-Concept**  

1. Log Out of the Dashboard
2. Create a New User Identity (if not already set up)
  - This generates a new cryptographic key-pair and register it as a separate identity.
3. Log In with the New Identity  
4. Interact as a Different Persona  

Each identity remains independent, ensuring that no personal data, social connections, or activity overlap unless explicitly linked by the user. Future iterations of 2WAY may introduce built-in persona management for seamless switching without requiring a logout/login process.

<br>

## 3.4 Synchronizing Data  

The 2WAY system enables users to synchronize data securely across multiple devices and platforms while maintaining privacy and consistency. Synchronization is achieved through peer-to-peer (P2P) networking, the 2WAY Graph, and end-to-end (e2e) encrypted communications. This ensures that user data remains available, up-to-date, and accessible only to authorized devices.  

2WAY utilizes public key (pubkey) Attributes and Onion addresses stored in the Graph, along with Access Control Lists (ACLs) and the Network Manager, to facilitate secure and private data synchronization. This approach ensures that only trusted devices within a user's graph receive and update data.  

### 3.4.1 How Synchronization Works  

Data synchronization in 2WAY follows a P2P model, where devices communicate directly without relying on a centralized server. The process works as follows:  

1. Device discovery  
   - The system retrieves pubkey and Onion Attributes from the 2WAY Graph to identify trusted devices.  
   - The Network Manager establishes secure connections between devices using the Tor network (if enabled) or a direct connection.  

2. Data verification and permissions  
   - The system verifies the identity of connected devices using cryptographic signatures.  
   - Access Control Lists (ACLs) determine which data each device can access and modify.  

3. State synchronization  
   - Devices exchange cryptographic proofs to verify data consistency.  
   - The Graph Manager ensures that updates are applied in a structured, conflict-free manner.  

4. End-to-end encrypted communication  
   - All data transfers are protected with e2e encryption, ensuring that only the intended recipient can decrypt the information.  
   - Key exchanges between devices guarantee message authenticity.  

### 3.4.2 Adding a New Device for Synchronization  

To synchronize data with a new device, the user must link it to their existing identity using a cryptographic key-pair.  

#### Steps to add a new device  

1. Generate a new device key-pair  
   - Each device must have a unique key-pair that is tied to the user’s primary identity.  
   - This prevents unauthorized devices from accessing data.  

2. Register the device in the 2WAY Graph  
   - The user logs into their primary device and adds the new device’s pubkey to their 2WAY Graph.  
   - If using Tor, the device’s Onion address is also stored.  

3. Approve synchronization via the dashboard  
   - The user must verify and approve the new device from their existing dashboard.  
   - The system ensures that ACLs permit synchronization.  

4. Initial data sync  
   - Once approved, the primary device pushes initial data to the new device.  
   - The Storage Manager and Graph Manager handle this process securely.  

### 3.4.3 Managing Data Synchronization  

Once a device is linked, it will automatically sync data based on the user’s graph connections and ACL settings.  

#### Managing sync settings  

1. Enable/disable sync for specific data  
   - Users can choose which data categories (contacts, messages, social feeds, marketplace activity, etc.) to synchronize.  

2. Set sync frequency  
   - Synchronization can occur in real-time or at scheduled intervals.  

3. Remove a device from synchronization  
   - If a device is lost or compromised, it can be removed from the graph, revoking access to future updates.  

### 3.4.4 Handling Conflicts and Data Integrity  

Since 2WAY is a distributed system, conflicts may arise when multiple devices modify data simultaneously. The Graph Manager and Storage Manager handle conflict resolution as follows:  

1. Timestamp-based resolution  
   - The system prioritizes the most recent change if conflicting edits occur.  

2. User-approved merging  
   - For critical updates, the system requests user approval before merging conflicting data.  

3. Immutable logging  
   - The Log Manager records all changes, ensuring that past versions remain accessible.  

### 3.4.5 Secure Data Recovery  

If a device is lost or data is corrupted, users can recover information by re-syncing with their trusted network.  

#### Steps to recover data  

1. Log into a trusted device  
2. Retrieve latest graph data  
   - The device queries the 2WAY Graph for the most recent version of stored data.  
3. Verify integrity  
   - Data authenticity is confirmed using cryptographic signatures.  
4. Rebuild local storage  
   - The system restores data and syncs missing entries.  

### 3.4.6 Next Steps  

Once synchronization is set up, users can:  

- Access their data seamlessly across all linked devices.  
- Use encrypted messaging, social feeds, and marketplace apps with consistent data.  
- Revoke access for lost or compromised devices to maintain security.  

The decentralized nature of 2WAY ensures that synchronization remains private, secure, and under full user control without reliance on third parties.

<br>

## 3.5 Key Revocation, Re-Issuance, and Propagation  

The 2WAY system provides a secure mechanism for handling key revocation and re-issuance to maintain the integrity of user identities. Since cryptographic keys are fundamental to authentication and secure communications, any compromised, lost, or outdated key must be replaced without disrupting the user's connections.  

To facilitate secure key transitions, 2WAY implements a **multi-signature (multi-sig) alarm system**, where **2 out of 3 alarm keys** can signal to a user’s contacts that a key has been compromised and should no longer be trusted. This system ensures that key revocation and propagation are handled reliably, preventing unauthorized access while maintaining trust.  

### 3.5.1 When Key Revocation is Necessary  

A user may need to revoke their cryptographic key in the following situations:  

1. **Key compromise**  
   - If an attacker gains access to a user’s private key, all associated communications and actions could be forged.  

2. **Device loss or theft**  
   - If a device containing the private key is lost or stolen, the user must revoke the key to prevent unauthorized use.  

3. **Key rotation for security**  
   - Periodic key changes reduce the risk of long-term exposure and strengthen security.  

4. **User-controlled deactivation**  
   - A user may wish to retire an old identity or transition to a new one.  

### 3.5.2 Multi-Sig Alarm Mechanism  

To prevent unauthorized revocations, 2WAY uses a **multi-sig alarm system** that requires **2 out of 3 alarm keys** to confirm a key revocation request. These alarm keys are generated and stored separately from the main identity key to ensure security.  

- Each user has **three alarm keys**, which can be stored on different devices or shared with trusted contacts.  
- When **at least two alarm keys** are used, the system marks the primary key as revoked and propagates the update through the 2WAY Graph.  
- The revocation notice is cryptographically signed and automatically distributed to the user’s contacts.  

### 3.5.3 Revoking a Key  

If a key needs to be revoked, the user (or trusted contacts) must activate the multi-sig alarm mechanism.  

#### Steps to revoke a key  

1. **Access the key management interface**  
   - Log into a trusted device or have two trusted contacts sign the revocation request.  

2. **Initiate the multi-sig alarm process**  
   - Use at least two of the three alarm keys to sign the revocation request.  

3. **Broadcast the revocation to the 2WAY Graph**  
   - The system updates the user’s contact list and notifies them that the key is no longer valid.  
   - The Network Manager stops accepting messages signed with the revoked key.  

4. **Confirm revocation**  
   - Affected contacts will receive a signed notice marking the key as compromised or retired.  

### 3.5.4 Re-Issuing a Key  

After revocation, the user must generate a new key-pair and distribute it securely.  

#### Steps to issue a new key  

1. **Generate a new cryptographic key-pair**  
   - The system creates a fresh public-private key-pair for the user.  

2. **Register the new key in the 2WAY Graph**  
   - The new key is linked to the user’s identity and replaces the revoked key.  

3. **Sign the update with an alarm key**  
   - This ensures authenticity and prevents unauthorized key replacements.  

4. **Notify contacts of the key change**  
   - A signed update is sent to all trusted contacts, informing them of the new key.  
   - The Network Manager ensures that all future communications use the updated key.  

### 3.5.5 Propagation of Revoked and Re-Issued Keys  

The 2WAY system ensures that key changes propagate efficiently through the user’s network.  

1. **Immediate notification**  
   - Contacts receive an automated update about the revoked key and its replacement.  

2. **Graph-based trust validation**  
   - Users can verify the authenticity of the new key through the 2WAY Graph, ensuring it was issued by the legitimate owner.  

3. **Network-wide enforcement**  
   - Once a key is revoked, the system prevents any further use of the compromised key for authentication, messaging, or transactions.  

### 3.5.6 Next Steps  

After a successful key re-issuance, users should:  

- Ensure that **all linked devices** are updated with the new key.  
- Manually verify the key change with **critical contacts**.  
- Store the **new alarm keys** securely for future emergencies.  

The multi-sig alarm system provides a **secure and trust-based approach to key revocation and propagation**, ensuring that users remain protected against compromised credentials while maintaining continuity in their digital interactions.

<br>

## 3.6 Zero-Knowledge Proofs  

Zero-knowledge proofs (ZKPs) allow users to prove they possess certain information without revealing the information itself. In the 2WAY system, ZKPs enable privacy-preserving verification, ensuring that trust can be established without exposing sensitive data. This is essential for maintaining anonymity, preventing fraud, and enabling secure interactions without requiring a centralized authority.  

### 3.6.1 How Zero-Knowledge Proofs Work  

A ZKP consists of three main properties:  

1. **Completeness**  
   - If the statement is true, an honest verifier will be convinced by the proof.  

2. **Soundness**  
   - If the statement is false, a dishonest prover cannot trick the verifier into accepting it as true.  

3. **Zero-Knowledge**  
   - The verifier learns nothing beyond the fact that the statement is true.  

### 3.6.2 Use Cases in the 2WAY System  

ZKPs in 2WAY enhance security and privacy across various applications, including identity verification, access control, and decentralized transactions.  

#### Examples of ZKP Use Cases in 2WAY:  

1. **Verifying Identity Without Revealing Information**  
   - Users can prove they are over a certain age without revealing their exact birth date.  
   - A user can confirm they belong to a trusted group without exposing their group membership details.  

2. **Access Control Without Credential Disclosure**  
   - Instead of sharing a password, users can prove they have permission to access a system using a ZKP.  

3. **Private Reputation Verification**  
   - Users can demonstrate a strong reputation score without disclosing individual ratings or interactions.  

4. **Fraud Prevention in Decentralized Marketplaces**  
   - Buyers and sellers can verify transaction history without exposing the full details of past trades.  

### 3.6.3 Implementing ZKPs in 2WAY  

ZKPs are integrated into 2WAY using cryptographic techniques that ensure privacy while enabling verifiable proofs.  

#### Steps in a Zero-Knowledge Proof Interaction  

1. **Prover generates proof**  
   - The user (prover) creates a cryptographic proof that a statement is true without revealing any private details.  

2. **Verifier validates proof**  
   - The recipient (verifier) checks the proof using cryptographic algorithms to ensure it is mathematically sound.  

3. **Decision is made**  
   - If the proof is valid, access is granted or the verification is accepted.  
   - No additional information beyond the proof is revealed.  

### 3.6.4 Example: Anonymous Group Membership Verification  

A common application of ZKPs in 2WAY is proving membership in a group without revealing individual identities.  

#### Scenario: Proving You Are a Member of a Verified Business Network  

1. **The user (prover) generates a ZKP**  
   - They create a proof that their public key exists in the verified business network without revealing which entry it corresponds to.  

2. **The recipient (verifier) checks the proof**  
   - They validate the cryptographic proof without needing to see the entire list of verified members.  

3. **Access is granted based on verification**  
   - The user can now participate in restricted business transactions while maintaining anonymity.  

### 3.6.5 Benefits of ZKPs in 2WAY  

1. **Enhanced privacy**  
   - Users can verify claims without exposing unnecessary details.  

2. **Reduced risk of data leaks**  
   - Sensitive user data is never directly shared or stored.  

3. **Increased trust in decentralized interactions**  
   - Users can prove authenticity while remaining anonymous.  

4. **Fraud prevention**  
   - Prevents unauthorized users from making false claims.  

### 3.6.6 Next Steps  

By leveraging ZKPs, 2WAY ensures that users can securely prove their identity, permissions, and reputation while maintaining complete privacy. Future updates may expand ZKP capabilities for advanced authentication, secure voting, and additional decentralized verification scenarios.

<br>

## 3.7 Private Messaging  

The 2WAY system provides end-to-end encrypted (E2EE) private messaging, ensuring that only the intended recipients can read messages while preventing interception by third parties. Messaging in 2WAY is built on public key cryptography, the 2WAY Graph, and peer-to-peer (P2P) networking, allowing users to communicate securely without relying on centralized servers.  

### 3.7.1 How Private Messaging Works  

Messages in 2WAY are encrypted and signed before being transmitted over the network. The encryption ensures privacy, while digital signatures provide message integrity and authenticity.  

1. **Message encryption**  
   - Messages are encrypted using the recipient’s public key, ensuring only they can decrypt it.  

2. **Message signing**  
   - Each message is signed with the sender’s private key to prevent tampering and verify authenticity.  

3. **P2P delivery through the Network Manager**  
   - Messages are transmitted over Tor-based networking or direct P2P connections, ensuring anonymity and security.  

4. **Graph-based contact verification**  
   - The system ensures that messages are only exchanged between verified contacts within the user’s 2WAY Graph.  

### 3.7.2 Sending a Private Message  

To send a private message, the sender encrypts the message with the recipient’s public key and signs it with their own private key.  

#### Steps to send a message  

1. **Select a contact from the 2WAY dashboard**  
   - The recipient must be a verified contact with a stored public key.  

2. **Compose the message**  
   - The message is written and prepared for encryption.  

3. **Encrypt the message**  
   - The message is encrypted using the recipient’s public key.  
   - Only the recipient can decrypt it using their private key.  

4. **Sign the message**  
   - The sender signs the encrypted message with their private key.  

5. **Transmit the message**  
   - The message is routed through the Network Manager using P2P connections or Onion routing.  

### 3.7.3 Receiving and Decrypting a Private Message  

When a recipient receives a message, they must decrypt it using their private key and verify its authenticity.  

#### Steps to receive and decrypt a message  

1. **Retrieve the encrypted message**  
   - The message is received through the Network Manager.  

2. **Verify the sender’s signature**  
   - The system checks the sender’s signature to confirm the message was not altered.  

3. **Decrypt the message**  
   - The recipient uses their private key to decrypt and read the message.  

4. **Respond securely**  
   - The recipient can reply using the same encrypted and signed process.  

### 3.7.4 Ensuring Message Integrity and Privacy  

To maintain security, 2WAY applies additional protections to private messaging.  

1. **End-to-end encryption**  
   - Messages remain encrypted throughout the transmission process.  

2. **Forward secrecy**  
   - Each conversation generates unique encryption keys to prevent past messages from being decrypted if a key is compromised.  

3. **Tamper-proof messaging**  
   - Signed messages prevent unauthorized modifications or impersonation.  

4. **Self-destructing messages (optional)**  
   - Users can set messages to delete after a certain period, ensuring no long-term storage of sensitive communications.  

### 3.7.5 Handling Offline Messaging  

If a recipient is offline, messages are temporarily stored in encrypted form within the sender’s local queue and transmitted when the recipient comes online.  

#### Steps for offline messaging  

1. The sender encrypts and signs the message  
2. The message is held in the sender’s encrypted outbox  
3. When the recipient reconnects, the message is transmitted  
4. The recipient decrypts and verifies the message as usual  

### 3.7.6 Preventing Metadata Leaks  

Unlike traditional messaging platforms, 2WAY minimizes metadata exposure:  

- Messages are routed through Onion addresses or direct P2P connections.  
- No centralized logging of message transactions exists.  
- Encrypted payloads prevent third parties from analyzing message contents or frequencies.  

### 3.7.7 Next Steps  

With private messaging enabled, users can:  

- Communicate securely without exposing personal information  
- Exchange encrypted files and sensitive data  
- Verify messages cryptographically before trusting them  

Future enhancements may include group messaging, anonymous broadcasting, and decentralized storage for message history, all while maintaining user privacy and security.

<br>

## 3.8 Social Feed  

The 2WAY system includes a decentralized social feed that allows users to share updates, interact with posts, and follow trusted contacts without relying on a central server. Social interactions occur within the 2WAY Graph, ensuring that users receive updates only from verified contacts while maintaining control over their visibility and privacy.  

Unlike traditional social media platforms, the 2WAY social feed does not store posts on a central database. Instead, messages are signed and transmitted to other servers in batches, optimizing efficiency while ensuring authenticity.  

### 3.8.1 How the Social Feed Works  

The social feed aggregates posts and interactions from a user’s direct and extended connections. Messages are exchanged over the network, ensuring real-time updates while maintaining privacy and decentralization.  

1. Users create posts that are stored locally until they are sent.  
2. Messages are signed before being transmitted along with other pending messages.  
3. The recipient's server verifies the messages and integrates them into their local graph.  
4. Updates propagate through the user’s network based on their graph connections.  

### 3.8.2 Posting an Update  

Users can post updates that will be visible to their contacts, with privacy settings allowing control over who receives them.  

#### Steps to post an update  

1. Navigate to the social feed in the dashboard.  
2. Enter the post content.  
3. Select the audience:  
   - Public (visible to all contacts)  
   - Private (visible only to selected groups)  
4. Submit the post.  
5. The system queues the post and signs it when messages are ready to be transmitted.  

Once the message is sent, it appears in the feeds of connected users based on their relationship in the 2WAY Graph.  

### 3.8.3 Receiving and Displaying Posts  

When a server receives a batch of messages, it verifies their signatures and integrates valid posts into the user’s feed.  

#### Steps to receive and display posts  

1. The server receives a batch of messages, including social updates.  
2. The system verifies message signatures before processing.  
3. The social feed updates with new posts from verified contacts.  
4. Posts are displayed in chronological order, with filtering options based on relevance or trust scores.  

### 3.8.4 Interacting with Posts  

Users can engage with posts by reacting, commenting, or resharing updates from their network.  

#### Types of interactions  

- Reactions: Users can acknowledge posts with positive or neutral signals.  
- Comments: Replies to posts are encrypted and follow the same transmission process as private messages.  
- Resharing: Users can propagate posts further in their network while preserving the original signature.  

### 3.8.5 Managing Social Feed Visibility  

Users control their feed by filtering posts based on trust levels, reputation, and network distance.  

#### Filtering options  

- Show posts only from direct contacts.  
- Limit visibility to certain groups.  
- Exclude posts from flagged or low-reputation sources.  

### 3.8.6 Handling Real-Time Updates  

Since posts are transmitted in batches, real-time updates depend on the frequency of outgoing messages. Users receive updates at regular intervals without overwhelming the network.  

#### Steps for real-time synchronization  

1. The system checks for new messages at defined intervals.  
2. Verified messages are processed and added to the feed.  
3. The dashboard updates dynamically with new content.  

### 3.8.7 Next Steps  

With the social feed enabled, users can:  

- Share updates without relying on centralized platforms.  
- Interact with trusted connections while maintaining privacy.  
- Control the visibility and propagation of their posts.  

Future enhancements may include media attachments, event-based notifications, and additional filtering mechanisms to improve relevance and engagement.

<br>

## 3.9 Solving for Sybil Attacks  

A Sybil attack occurs when an entity creates multiple fake identities to manipulate a system, infiltrate trust networks, or disrupt normal operations. In centralized systems, Sybil resistance relies on verification methods such as CAPTCHAs, identity checks, or account limits. However, in decentralized systems like 2WAY, preventing Sybil attacks requires a trust-based approach that does not rely on a central authority.  

2WAY mitigates Sybil attacks using whitelisting principles and graph-based filtering by degrees of separation. Instead of blacklisting malicious accounts, which is ineffective in a decentralized system, 2WAY ensures that users interact only with identities that have strong, verifiable trust links. The system enables users to control their own visibility and exposure by defining how far outside their trusted graph they allow interactions.  

### 3.9.1 How 2WAY Mitigates Sybil Attacks  

1. **Whitelisting instead of blacklisting**  
   - Users receive and interact only with content from known, trusted connections.  
   - Unlike traditional systems that attempt to detect and ban fake accounts, 2WAY defaults to filtering out unknown entities until a trust relationship is formed.  

2. **Filtering by degrees of separation**  
   - Users can configure visibility settings to allow interactions only from first-degree (direct) contacts or second-degree (friends of friends) while excluding unknown or weakly connected entities.  
   - This makes it computationally expensive for an attacker to establish enough strong trust relationships to influence real users.  

3. **Graph-based Sybil detection**  
   - The User Graph Visualization helps users recognize unnatural connection patterns.  
   - A Sybil swarm typically consists of multiple weakly connected identities that only reference each other but lack strong links to real, well-connected users.  

4. **Trust propagation limitations**  
   - In 2WAY, trust does not automatically extend beyond direct and explicitly verified relationships.  
   - Even if a real user unknowingly connects to a Sybil identity, their network does not automatically trust that identity’s other connections.  

5. **Reputation constraints**  
   - Reputation is earned through interactions with established users, making it difficult for a Sybil attacker to fabricate legitimacy.  
   - Users can set thresholds requiring minimum reputation scores before engaging with new identities.  

### 3.9.2 Recognizing Sybil Swarms in the User Graph  

Sybil swarms attempt to blend into a network by creating many fake accounts that reference one another, hoping to appear legitimate. The User Graph Visualization enables users to spot these patterns by highlighting unnatural clusters.  

#### Characteristics of Sybil swarms:  

- Dense clusters of accounts that only connect to each other.  
- Few or no connections to long-established users.  
- Disproportionate number of newly created accounts with no history.  
- Rapid network expansion without meaningful interactions.  

#### Steps to identify and filter Sybil identities:  

1. Open the User Graph Visualization in the dashboard.  
2. Set visibility to first-degree contacts only and gradually expand to second-degree if needed.  
3. Examine weakly connected clusters with minimal external trust links.  
4. Restrict interactions with users outside of your configured trust radius.  

### 3.9.3 Trust-Based Filtering and Sybil Resistance  

By default, users only see messages, reputation scores, and social feed updates from verified connections. If an unknown user attempts to interact, their content is hidden unless explicitly allowed.  

#### How filtering prevents Sybil attacks:  

- First-degree filtering: Users only interact with contacts they have personally verified.  
- Second-degree filtering: Extends visibility but still ensures that all interactions originate from someone you trust.  
- Reputation-based filtering: Users can require a minimum trust level before accepting interactions.  

This model ensures that no single attacker can mass-generate fake accounts and insert them into the network without first gaining real trust from multiple independent users, which is computationally difficult at scale.  

### 3.9.4 Next Steps  

With trust-based filtering in place, users can:  

- Automatically exclude Sybil swarms by restricting visibility to verified connections.  
- Use graph visualization tools to analyze new connections before trusting them.  
- Adjust trust-based filters to control exposure to unknown identities while maintaining flexibility.  

Future improvements may include automated anomaly detection, pattern-based flagging of suspicious clusters, and stronger reputation-based trust metrics to further enhance Sybil attack prevention.

<br>

## 3.10 Wallet Plugin  

The wallet plugin in the 2WAY system provides users with a secure and decentralized way to manage digital assets, including cryptocurrencies and digital identity credentials. Unlike traditional wallets that rely on centralized providers, the 2WAY wallet operates within the decentralized framework of the system, ensuring full user control over private keys and transactions.  

Beyond standalone functionality, the wallet plugin is designed to integrate with other plugins, enabling extended features such as secure payments, reputation-based transactions, and automated identity verification. Other plugins can either leverage the wallet plugin’s capabilities or extend its functionalities for specialized use cases.  

### 3.10.1 How the Wallet Plugin Works  

The wallet plugin functions as a self-custodial wallet, meaning users retain full control over their private keys without third-party intermediaries.  

1. Users generate a cryptographic key-pair for their wallet.  
2. Funds and identity credentials are stored locally and signed transactions are broadcast over the network.  
3. Transactions are secured using the same cryptographic framework that underpins 2WAY’s identity system.  
4. Other plugins can access wallet features via secure API calls, allowing decentralized applications to perform payments, deposits, and trust-based transactions.  

### 3.10.2 Setting Up the Wallet  

The wallet plugin is available in the dashboard and can be set up in a few steps.  

#### Steps to create a wallet  

1. Open the wallet section in the 2WAY dashboard.  
2. Generate a new wallet key-pair or import an existing one.  
3. Securely back up the private key.  
4. Set transaction preferences, such as fee settings and network selection.  

Once set up, the wallet can send and receive funds, sign identity attestations, or integrate with other plugins to facilitate trusted interactions.  

### 3.10.3 Sending and Receiving Funds  

Users can send transactions securely through the wallet interface.  

#### Steps to send funds  

1. Enter the recipient’s public key or address.  
2. Specify the amount and transaction details.  
3. The system signs the transaction with the sender’s private key.  
4. The transaction is broadcast to the network and recorded in the appropriate ledger.  

#### Steps to receive funds  

1. Share the wallet’s public key or address with the sender.  
2. Incoming transactions are verified and recorded.  
3. The wallet notifies the user of the new balance update.  

### 3.10.4 Integrating the Wallet Plugin with Other Plugins  

The wallet plugin is designed to be modular, allowing other plugins to either use its functionality or extend its features.  

#### Examples of integrations:  

- **Marketplace plugin**  
  - Enables users to buy and sell goods using wallet-stored assets.  
  - Allows transactions to be linked to trust scores for reputation-based pricing.  

- **Reputation and identity verification plugins**  
  - Lets users pay for identity attestations with cryptocurrency.  
  - Allows users to prove reputation without revealing transaction details.  

- **Subscription-based access control**  
  - Enables premium access to features based on wallet balance or payments.  

- **Automated smart contract execution**  
  - Other plugins can trigger wallet transactions based on pre-defined conditions.  

### 3.10.5 Extending the Wallet Plugin’s Functionality  

Other plugins can build upon the wallet plugin to introduce specialized functionality.  

#### Examples of extensions:  

- **Multi-signature transactions**  
  - A security-focused plugin could add multi-sig wallet support for shared accounts.  

- **Tokenized assets and credentials**  
  - A plugin could introduce non-fungible tokens (NFTs) or identity-linked verifiable credentials.  

- **Time-locked transactions**  
  - A contract-based plugin could enable time-locked payments or automated withdrawals.  

### 3.10.6 Security and Privacy Considerations  

The wallet plugin follows strict security measures to prevent unauthorized access and ensure safe transactions.  

1. End-to-end encryption for private keys and transaction data.  
2. Local key storage with no third-party access.  
3. Signed transactions to prevent tampering.  
4. Integration with access control lists (ACLs) to define wallet permissions.  

### 3.10.7 Next Steps  

With the wallet plugin enabled, users can:  

- Securely store and transfer digital assets within 2WAY.  
- Use the wallet for trust-based payments and identity verifications.  
- Extend wallet functionality through integrations with other plugins.  

Future enhancements may include decentralized escrow services, cross-chain compatibility, and programmable financial interactions that further expand the wallet’s role in the 2WAY ecosystem.

<br>

## 3.11 Verifying Binaries  

The 2WAY system provides an automated mechanism for verifying binaries before installation or execution, ensuring software integrity and authenticity without requiring user intervention. This process leverages the 2WAY Graph to validate that a binary originates from a trusted source and has not been tampered with.  

Binary verification is handled entirely in the background, requiring no manual input from the user. The system automatically checks the signatures and integrity of files against known records in the 2WAY Graph, preventing unauthorized or malicious modifications from being executed.  

### 3.11.1 How Binary Verification Works  

1. A binary file is downloaded or executed on the user’s system.  
2. The system automatically retrieves metadata related to the binary, such as its cryptographic hash and signing key.  
3. The 2WAY Graph is queried to check if the binary’s hash and signature match a verified entry.  
4. If a match is found, the binary is considered authentic and allowed to execute.  
5. If the verification fails or the binary is unknown, the system can warn the user or block execution based on security settings.  

### 3.11.2 Verifying Software Authenticity in the Background  

Since verification is integrated into the 2WAY framework, users do not need to manually verify files or signatures. Instead, the system automatically cross-references known records to determine whether a binary can be trusted.  

#### Automated verification process:  

1. Before installation or execution, the binary's hash and signature are checked against trusted records.  
2. The Graph Manager queries the 2WAY Graph, retrieving the expected hash and signers for the binary.  
3. The system compares the downloaded binary to the recorded information.  
4. If there is a mismatch or an unknown signature, the system flags the file as potentially unsafe.  

### 3.11.3 Trust-Based Verification Using the 2WAY Graph  

Binary verification in 2WAY relies on whitelisted sources and trust-based validation.  

- If the binary is published by a trusted developer, the system recognizes it as safe.  
- If multiple users in the network approve the binary, it gains additional trustworthiness.  
- If a file is modified or mismatched, the system prevents execution or warns the user.  

Since trust is inherited within the 2WAY Graph, verification does not rely on a single authority. Users can choose to trust binaries signed by their own contacts, limiting exposure to potentially compromised files.  

### 3.11.4 Handling Unverified Binaries  

If a binary does not have a known record in the 2WAY Graph, the system takes precautionary measures.  

1. The binary is flagged as unverified.  
2. The user can request validation from trusted sources.  
3. If the binary gains trust through additional verification, it is added to the Graph for future reference.  

Unknown binaries are not automatically blocked, but their execution depends on the user’s security preferences and the trust levels within their network.  

### 3.11.5 Integrating Verification with Other Plugins  

The binary verification system can be extended by other plugins to enhance security and usability.  

#### Examples of integrations:  

- **Marketplace plugin**  
  - Ensures that software purchased through decentralized markets is authentic.  

- **Reputation and trust plugins**  
  - Allows binaries to gain trust through endorsements from reputable developers.  

- **Automated patch management**  
  - Verifies that software updates come from legitimate sources before applying them.  

### 3.11.6 Next Steps  

With automatic binary verification enabled, users can:  

- Ensure that only trusted binaries run on their system.  
- Prevent execution of malicious or tampered files.  
- Use trust-based validation instead of relying on a central authority.  

Future enhancements may include sandboxed execution of unverified binaries, automatic removal of flagged files, and extended verification through decentralized reputation tracking.

<br>

## 3.12 Market Plugin  

The market plugin in the 2WAY system enables decentralized, trust-based transactions without the need for intermediaries. Unlike traditional marketplaces, which rely on centralized servers and public listings, 2WAY’s market is entirely peer-to-peer, where the items and sellers available to a user are determined by their existing contacts and shared listings.  

The market plugin is modular, allowing other plugins to hook into it for specialized use cases, such as a ride-sharing plugin, a job board, or a digital goods exchange. Users have full control over their privacy, identity, and transaction visibility, ensuring that only trusted contacts see their listings and offers.  

### 3.12.1 How the Market Plugin Works  

1. A seller creates a listing, which is stored in the 2WAY Graph and shared with selected contacts.  
2. The buyer browses listings only from their trusted network—there is no global public marketplace.  
3. A buyer initiates a transaction, and the system handles payment, verification, and reputation tracking.  
4. The purchase record is shared only between buyer and seller, unless the buyer chooses to allow recommendations based on past purchases.  

Since listings are private by default, a user’s market is unique to their connections. Expanding available items means forming new trusted relationships rather than searching a central directory.  

### 3.12.2 Creating and Managing Listings  

Sellers can create new listings that are visible only to selected contacts or groups.  

#### Steps to create a listing  

1. Open the market section in the 2WAY dashboard.  
2. Click "Create New Listing".  
3. Enter item details, including title, description, price, and accepted payment methods.  
4. Choose who can see the listing:  
   - Direct contacts only  
   - Contacts of contacts (second-degree connections)  
   - Specific groups (e.g., "Frequent Buyers")  
5. Publish the listing.  

Once created, the listing is stored in the seller’s graph and propagated only to those within the selected visibility range.  

### 3.12.3 Buying an Item  

Since all transactions are private, buyers interact directly with sellers without exposing their identity unless they choose to.  

#### Steps to buy an item  

1. Browse available listings from trusted contacts in the market section.  
2. Select an item and click "Initiate Purchase".  
3. Generate a new key-pair for the transaction:  
   - Single-use key for full anonymity.  
   - Per-seller key to allow personalized recommendations.  
4. Send payment securely via the integrated wallet plugin.  
5. The seller verifies the transaction and confirms delivery.  

### 3.12.4 Privacy and Transaction Keys  

2WAY allows users to control how much identity information is shared in each transaction.  

- **Fully anonymous purchase**  
  - A new key-pair is generated for every purchase, unlinking transactions from a persistent identity.  

- **Per-seller purchase identity**  
  - A buyer generates a dedicated key-pair for transactions with a specific seller.  
  - This enables future recommendations without exposing all past purchases.  

- **Trusted identity purchases**  
  - Buyers use their primary key to build a verifiable reputation over time.  
  - Ideal for repeat buyers who want access to exclusive listings.  

Each transaction remains private within the buyer-seller relationship unless explicitly shared.  

### 3.12.5 Integrating Other Plugins with the Market  

The market plugin serves as a foundation for more specialized marketplaces. Other plugins can hook into it to extend functionality.  

#### Examples of market integrations  

- **Ride-sharing plugin**  
  - Users can list rides, request transportation, and pay securely through the market.  

- **Job board plugin**  
  - Freelancers and employers can create trust-based job postings and accept verified payments.  

- **Decentralized auction plugin**  
  - Supports time-based bidding within private, invitation-only auctions.  

- **Reputation and identity verification plugins**  
  - Allows sellers to offer discounts or prioritize buyers with high trust scores.  

### 3.12.6 Payment and Dispute Resolution  

Since payments occur between users, there is no built-in escrow system. However, buyers and sellers can:  

1. Use reputation-based filtering to avoid untrusted sellers.  
2. Require deposits or staged payments for high-value transactions.  
3. Leverage external escrow services, integrated via other plugins.  

### 3.12.7 Next Steps  

With the market plugin, users can:  

- Buy and sell goods securely within their trusted network.  
- Control who sees their listings and who can interact with them.  
- Use transaction-based identities for added privacy.  
- Extend the market plugin’s functionality with specialized integrations.  

Future enhancements may include smart contract-based escrow, automated reputation weighting, and decentralized delivery tracking.

<br>

## 3.13 P2P Advertising  

The 2WAY system introduces a peer-to-peer (P2P) advertising model that works opposite to traditional, centralized advertising systems. Instead of advertisers targeting users based on invasive tracking and personal data harvesting, 2WAY allows users to opt-in to receive advertisements, ensuring that ads are always relevant and spam-free.  

In the 2WAY network, advertising is a mutual exchange of value. Users do not see ads unless they explicitly choose to, and advertisers must offer something beneficial to maintain visibility. If an advertiser is no longer valuable to the user, they can be down-voted or removed from the user’s contacts, which immediately stops all future ads from that advertiser.  

This voluntary participation model ensures that advertising in 2WAY achieves near-100% engagement with a relevant audience, as users have already expressed interest in a specific type of ad content before they ever see an ad.  

### 3.13.1 How P2P Advertising Works  

1. Users opt-in to receive advertisements from selected advertisers or advertising networks.  
2. Advertisers share promoted listings, offers, or content, which are only seen by users who have opted in.  
3. Users engage with ads based on personal preferences, wishlists, or specific items they are actively looking for.  
4. If an advertiser is no longer relevant, the user can remove them from their contacts or down-vote them, instantly stopping all future messages from that advertiser.  

Since there is no global ad network force-feeding users ads, spam cannot exist in the 2WAY system. Advertisers must earn and maintain user trust to remain visible.  

### 3.13.2 Opting into Advertisements  

Users can decide exactly who they receive advertisements from and how those ads are delivered.  

#### Ways users can opt into ads:  

- **Following specific advertisers**  
  - Users can manually add businesses or advertisers as contacts if they wish to receive offers from them.  

- **Wishlists and item requests**  
  - Users can list specific products or services they are looking for, allowing advertisers to respond with matching offers.  

- **Browsing promoted items**  
  - Users can explore publicly available promoted content, choosing to engage only with relevant advertisers.  

- **Reputation-based advertising**  
  - Users can opt to receive ads only from advertisers with a strong reputation in their trusted network.  

### 3.13.3 Controlling and Filtering Ads  

Since ads function as peer-to-peer messages, users maintain complete control over their visibility.  

#### Methods to manage ads:  

1. **Down-voting an advertiser**  
   - Users can down-vote an advertiser’s contact entry, preventing future ads from appearing.  

2. **Removing advertisers from contacts**  
   - This instantly stops all future ads from that advertiser.  

3. **Filtering based on trust levels**  
   - Ads can be limited to only trusted sources within the user’s network.  

4. **Adjusting ad frequency settings**  
   - Users can define how often they want to receive promotional content.  

### 3.13.4 Why Opt-In Ads Achieve Near-100% Engagement  

Since ads are only shown to users who have explicitly chosen to receive them, engagement rates are significantly higher than in traditional systems.  

- Users are already interested in the product or service being advertised.  
- No wasted impressions, as ads only reach a pre-qualified audience.  
- Higher conversion rates, since users have signaled intent before seeing an ad.  

This makes advertising in 2WAY more efficient and cost-effective than traditional models, as there is no need to bombard users with unwanted content in the hope of catching their attention.  

### 3.13.5 Integration with Other Plugins  

The P2P advertising model can be extended through other plugins to enhance functionality.  

#### Examples of plugin integrations:  

- **Market plugin**  
  - Advertisers can promote listings directly to users with matching wishlists.  

- **Reputation and trust plugins**  
  - Ads can be prioritized based on the advertiser’s reputation score.  

- **Social feed plugin**  
  - Users can choose to see promoted posts from businesses they trust.  

- **Subscription-based advertising networks**  
  - Users can opt into category-based advertising, such as tech deals, local services, or freelance job listings.  

### 3.13.6 Next Steps  

With P2P advertising, users can:  

- Receive only the ads they find valuable, without being tracked.  
- Maintain full control over who can advertise to them.  
- Remove irrelevant advertisers instantly by down-voting them.  
- Participate in highly targeted, interest-based advertising networks.  

Future enhancements may include automated ad matching, private bidding systems, and smart contract-based ad payments, further optimizing decentralized advertising in the 2WAY ecosystem.

<br>

## 3.14 Collaborative Document Editing
Guide on implementing real-time collaborative document editing within the 2WAY system, including conflict resolution strategies and user management.

<br>

## 3.15 IoT Device Management
Managing IoT devices using the 2WAY system, including device registration, communication protocols, and security measures.

<br>

## 3.16 Document Notarization
Technical and legal aspects of document notarization within the 2WAY system, ensuring authenticity and tamper-proof records.

<br>

## 3.17 Decentralized Finance
Exploration of decentralized finance (DeFi) applications within the 2WAY system, such as lending, trading, and insurance, highlighting their implementation and benefits.

<br>

## 3.18 Access Control Systems
Implementing digital and physical access control systems using the 2WAY system, ensuring secure and efficient access management.

<br>

## 3.19 Real Estate Transactions
Using the 2WAY system for real estate transactions, including smart contracts and the role of blockchain technology in ensuring secure and transparent property transfers.

<br>

## 3.20 Event Ticketing Systems
Addressing challenges in event ticketing, such as counterfeit tickets, using the 2WAY system to implement secure and verifiable ticketing solutions.

<br>

## 3.21 Resource Sharing Networks
Examples of resource-sharing networks within the 2WAY system, such as shared computing resources, storage, and bandwidth, and how they are managed and monetized.

<br>

## 3.22 Video Gaming
Exploration of 2WAY system applications in video gaming, focusing on in-game assets, player identities, and secure transactions.

<br><br>

# 4. Conclusion <a name="document-conclusion"></a>

The 2WAY system introduces a decentralized and trust-based framework for identity, reputation, and interaction, eliminating the need for central authorities while ensuring security, privacy, and user control. By leveraging cryptographic proofs, graph-based structures, and peer-to-peer networking, 2WAY creates a resilient system where users define their own trust networks and control their data visibility. This approach addresses fundamental challenges in digital identity management, messaging, social interactions, market transactions, and content verification.  

The architecture of 2WAY is designed to be modular and extensible, allowing new functionalities to be integrated through plugins that interact with core system components. The storage and verification of all interactions within the 2WAY Graph ensure that information remains tamper-resistant and transparently linked to its source. This design provides an alternative to traditional centralized platforms, where control over data and interactions is often dictated by third parties.  

Security and privacy are at the foundation of the system. End-to-end encryption ensures that communications remain confidential, while access control mechanisms define precisely who can see or interact with a user’s data. The system’s approach to key management enables users to revoke and replace cryptographic identities securely, mitigating the risks associated with compromised credentials. Through the integration of zero-knowledge proofs, users can verify information without exposing sensitive details, ensuring that trust can be established without compromising privacy.  

Decentralized applications built on 2WAY operate under the principle of user-defined trust. Private messaging allows encrypted communication within a network of verified contacts. The social feed ensures that information is only visible to those explicitly included in a user’s trusted network. Sybil attack prevention mechanisms reinforce the integrity of the system by restricting visibility and interactions to accounts with strong, verifiable relationships.  

The market plugin provides a peer-to-peer commerce system where listings and transactions are only visible within the user’s trust network. The wallet plugin integrates seamlessly to facilitate secure payments while preserving transaction privacy. The binary verification system ensures that software installations and updates originate from trusted sources, preventing malicious modifications. The advertising model shifts control entirely to the user, requiring advertisers to provide value before gaining visibility, ensuring that advertising remains relevant and voluntary rather than intrusive.  

The design of 2WAY challenges the conventional models of digital interaction by placing the user at the center of all decision-making. Trust is established organically through network relationships rather than enforced by centralized policies. Visibility and participation in the system are determined by explicit user consent, ensuring that no entity can impose itself on another without permission. The decentralized architecture ensures that the system remains resistant to censorship, fraud, and data exploitation.  

By removing dependencies on central intermediaries, 2WAY establishes a digital environment where privacy is preserved, security is enforced by design, and participation is voluntary. Future expansions of the system may introduce additional optimizations in network synchronization, automated trust scoring, and advanced data indexing, but the core principles of self-sovereignty, transparency, and decentralized control will remain. This document provides the foundation for a system where users can interact, transact, and communicate with confidence, knowing that their digital presence is fully under their control.

<br><br><br><br>
