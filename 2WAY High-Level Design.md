



# 2WAY: Protocol Architecture and Flask Implementation Blueprint

<br><br><br>

# Table of Contents
[Introduction](#introduction)
1. [Frontend](#frontend)<br>
  1.1 [Introduction to the Frontend](#11-introduction-to-the-frontend)<br>
  1.2 [Flask](#12-flask)<br>
  1.3 [Plugins](#13-plugins)<br>
  1.4 [Pre-Installed Plugins](#14-pre-installed-plugins)<br>
  1.5 [Custom Plugins](#15-custom-plugins)

2. [Backend](#backend)<br>
  2.1 [Introduction to the Backend](#21-introduction-to-the-backend)<br>
  2.2 [2WAY Graph](#22-2way-graph)<br>
  2.3 [2WAY Objects](#23-2way-objects)<br>
  2.4 [Database Schemas](#24-database-schema)<br>
  2.5 [Graph Manager](#25-graph-manager)<br>
  2.6 [Storage Manager](#26-storage-manager)<br>
  2.7 [Key Manager](#27-key-manager)<br>
  2.8 [Log Manager](#28-log-manager)<br>
  2.9 [Network Manager](#29-network-manager)<br>

3. [Practical Examples](#practical-examples)

3. [Conclusion](#conclusion)

<br><br><br>

# Introduction <a name="introduction"></a>

In today's digital landscape, centralized identity and reputation systems are everywhere, forming the foundation of online interactions. These systems manage user accounts and evaluate the credibility or reliability of users, products, services, and other entities based on various criteria. They operate similarly to algorithms used by popular platforms to establish and maintain user identities. While these systems offer convenience, they also introduce significant vulnerabilities and limitations that affect both users and third-party service providers. From privacy concerns to regulatory compliance challenges, centralized systems pose significant risks and costs to all stakeholders.

For users, centralized identity and reputation systems often require the disclosure of sensitive personal information to third-party intermediaries. This reliance raises privacy concerns and exposes users to data breaches and unauthorized access. Additionally, users may face restrictions on their digital freedoms, as centralized systems are subject to censorship and control by a single authority.

For third-party service providers, managing and securing vast amounts of user data within centralized systems incurs significant costs related to data storage, security measures, and regulatory compliance. As these systems grow, they become more susceptible to attacks, posing reputational risks and potential legal liabilities.

Decentralizing identity and reputation management can mitigate these risks and costs for both users and service providers. By distributing user data across a decentralized network, the need for central intermediaries is reduced, minimizing the risk of data breaches and unauthorized access. Decentralized systems offer greater transparency and security, as user data is cryptographically secured and managed with the help of decentralized graphs.

For service providers, decentralizing applications can streamline operations and reduce overhead costs associated with data management and security. Leveraging decentralized technologies like distributed graphs and peer-to-peer (P2P) networks enhances data privacy, reduces regulatory burdens, and mitigates the risk of cyber attacks.

<br>

Enter 2WAY, a proposal for a pioneering free and open-source proof-of-concept that reimagines electronic identity and reputation management in a fully peer-to-peer (P2P) environment. At its core, 2WAY empowers users to take control of their digital identities, manage linked data securely, and establish direct communication channels without relying on intermediaries. Through the seamless integration of digital signatures, a graph structure, and a decentralized P2P network, 2WAY offers users the ability to curate their digital personas, filter information for relevance, and engage securely with trusted parties, all within familiar interfaces.

The foundation of 2WAY lies in its distributed identity, reputation, and access management server, which leverages cryptographic proof to verify message authenticity and establish secure communication channels between servers. Through a decentralized network of trusted servers, users can exchange data with confidence, knowing that their identities and interactions are protected by robust cryptographic mechanisms.

Furthermore, 2WAY is designed with extensibility in mind, allowing developers to build plugins that serve as applications within the 2WAY system. These plugins can leverage the platform's core functionalities, enabling a diverse range of applications and services to be built on top of the 2WAY infrastructure.

Drawing inspiration from the principles of privacy by design, 2WAY ensures that personally identifiable information is processed minimally, with private messages and data shared only with consent and encrypted for the intended recipient. Public messages can be broadcast on a best-effort basis, though this remains outside the scope of this proof-of-concept.

Designed to be lightweight, 2WAY can run both the frontend (client) and backend (server) on a desktop computer, making it accessible and practical for a wide range of users. Although the main goal of the 2WAY proof-of-concept is to demonstrate the 2WAY protocol, the platform leverages the Flask framework for both the frontend and backend, merging them into a single application. This integrated approach simplifies development and deployment. Once the proof-of-concept has proven effective, the backend could be implemented as a daemon or service in a low-level language, and the frontend could be developed using any language or framework.

2WAY ensures scalability through a distributed architecture, leveraging decentralized technologies like distributed graphs and P2P networks to distribute workload across multiple servers. This enables horizontal scaling by adding more servers, accommodating growing user demands without performance degradation. Efficient data storage and retrieval mechanisms further enhance scalability while maintaining responsiveness. Additionally, 2WAY prioritizes user-friendly interfaces, designed with intuitive principles to simplify digital identity and data management. Clear interfaces guide users through tasks, reducing the need for technical expertise and fostering greater adoption and engagement.

<br>

This document navigates through the intricate layers of the 2WAY system, beginning with an exploration of its frontend infrastructure and extending to its backend architecture.

Within the Frontend section, we explain the Flask framework, the backbone of the 2WAY proof-of-concept, and examine the concept of plugins, from pre-installed options to the development of custom plugins.

Transitioning to the Backend section, we uncover the foundational elements of the 2WAY Graph, alongside the management of core 2WAY Objects such as Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). Additionally, we describe the Database Schema and dive deep into the functionalities of essential backend components, including the Graph Manager, Storage Manager, Network Manager, and more.

Finally, within the Practical Examples section, we illustrate the real-world applications of 2WAY across various scenarios, demonstrating its versatility and efficacy in managing contacts, messaging, social interactions, addressing security challenges like Sybil attacks, navigating markets, verifying binaries, and handling key management tasks.

In summary, 2WAY offers a groundbreaking approach to electronic identity and reputation management by decentralizing these processes and empowering users with greater control and security. By eliminating the need for centralized third parties, 2WAY reduces the risks and costs associated with managing and securing user data, benefiting both users and service providers. This proof-of-concept demonstrates the potential of running both frontend and backend on a single desktop computer, leveraging the Flask framework for a seamless, integrated experience. With its extensible plugin architecture, 2WAY provides a versatile platform for developers to create a wide range of applications, fostering a resilient and user-centric digital ecosystem. This document will guide you through the detailed workings of 2WAY, highlighting its potential to revolutionize the way we manage digital identities and interactions in a secure, decentralized manner.

<br><br>

# 1. Frontend <a name="frontend"></a>

<br>

## 1.1 Introduction to the Frontend <a name="11-introduction-to-the-frontend"></a>

The frontend of the 2WAY system acts as the primary interface for users to access and interact with the platform's diverse array of features and functionalities. It serves as the gateway through which users manage their identities, associated data, and access controls within the decentralized network.

Powered by the Flask framework, the frontend facilitates the development of dynamic web applications that are both robust and scalable, catering to a broad spectrum of user needs.

One of the standout features of the 2WAY frontend is the integration of plugins, which significantly augment its capabilities. These plugins extend and personalize the frontend experience, offering additional functionalities tailored to individual preferences. With pre-installed plugins providing essential features, users can immediately access a range of functionalities. Moreover, users and developers have the flexibility to create custom plugins, ensuring that the platform remains versatile and adaptable to evolving requirements.

In addition to individual plugin functionalities, the system's architecture enables seamless inter-plugin data access through established Access Control Lists (ACLs). These ACLs empower plugins to utilize or combine each other's data in the database, fostering interoperability and enriching the array of available features.

Furthermore, the frontend streamlines user experience by consolidating notifications from various plugins into a unified interface, offering users a comprehensive view of their system activity. Alongside notifications, logs and errors are also accessible from a single view, providing users with valuable insights and facilitating efficient troubleshooting.

The pre-installed Library plugin serves as a robust search tool, empowering users to query and filter information within the system effortlessly. Leveraging degrees of separation within the 2WAY Graph, users can navigate and explore interconnected data sets with ease, enhancing the platform's searchability and usability.

The Contacts plugin acts as an intuitive contact list or address book, allowing users to manage their network connections seamlessly. Integrated with the 2WAY Graph, the Contacts plugin provides a user-friendly interface for organizing and accessing contacts, facilitating smooth communication and collaboration.

Building upon the Contacts plugin, the Messages plugin offers peer-to-peer messaging capabilities, leveraging contact information and network connections from the 2WAY Graph. This enables real-time message exchanges, fostering effective communication within the platform.

Moreover, the Social plugin enhances user experience by providing a centralized social feed that aggregates the latest messages from contacts. This feed offers users a consolidated view of their interactions and conversations, keeping them informed about relevant discussions and activities within their network.

Operating both the frontend and backend locally on a user's machine ensures optimal performance in terms of storing and retrieving data. Unlike traditional web applications that rely on remote servers for processing, local hosting facilitates faster response times and enhanced efficiency. Users can register accounts, log in with familiar credentials, and reset passwords seamlessly, contributing to an overall seamless user experience.

In summary, the frontend of the 2WAY system, with its reliance on Flask and the integration of plugins, provides a versatile, efficient, and personalized platform for users to engage with. Through inter-plugin data access, consolidated notifications, and robust search functionalities, the frontend empowers users to effectively manage their interactions within the decentralized network, while logs, errors, and a visual representation of the user's graph offer valuable insights and enhance user experience.

<br>

## 1.2 Flask <a name="12-flask"></a>

Flask serves as the cornerstone of the 2WAY system's architecture, offering a versatile and lightweight framework for web application development. Traditionally known for backend development, Flask is uniquely employed in 2WAY to power both the server-side components and the client-side user interface. This approach merges the frontend and backend into a cohesive unit, simplifying development and deployment processes while promoting code reusability and maintainability.

Using Flask for both frontend and backend operations streamlines communication between the user interface and the server infrastructure, facilitating seamless data exchange and interaction. Flask's intuitive syntax and extensive ecosystem of extensions empower developers to create responsive, dynamic, and feature-rich web applications. Key extensions such as Flask-RESTful for building APIs, Flask-SQLAlchemy for database integration, and Flask-WTF for form handling contribute to the system's robustness and flexibility.

In the context of 2WAY, Flask's versatility and lightweight nature are particularly relevant for supporting the platform's comprehensive identity, reputation, and access management framework. By leveraging Flask's capabilities, developers can ensure that the frontend experience seamlessly interacts with backend services, providing users with a cohesive and intuitive interface. This is crucial for enhancing user engagement and efficiency in utilizing the platform's features and functionalities.

Furthermore, Flask's support for custom routing and middleware enables efficient handling of various frontend and backend functionalities within the 2WAY system. This ensures smooth navigation and interaction for users, contributing to a positive user experience.

Additionally, Flask's ability to manage sessions and authentication mechanisms is essential for ensuring secure access to 2WAY's functionalities. With Flask, developers can implement robust authentication mechanisms to safeguard user data and maintain the integrity of the platform.

Moreover, Flask's support for template rendering and dynamic content generation enhances the creation of dynamic and engaging user interfaces within 2WAY. This enables developers to deliver personalized and interactive experiences to users, further enriching their engagement with the platform.

Overall, Flask's simplicity, flexibility, and scalability make it an ideal choice for the unified architecture of the 2WAY system. By leveraging Flask's capabilities, developers can create a powerful and user-centric platform that meets the unique requirements of identity management, reputation building, and access control within a decentralized network.

<br>

## 1.3 Plugins <a name="13-plugins"></a>

In the 2WAY proof-of-concept, plugins demonstrate how applications can function on top of the 2WAY protocol, showcasing the broader potential of integrating various applications with the system. Through these plugins, the proof-of-concept illustrates the capabilities and versatility of the 2WAY protocol in supporting diverse application needs and enhancing user interactions.

These Flask plugins streamline communication with the backend Graph Manager, enabling efficient data handling within the application. Integrated into the Flask framework, they offer modular architectures for managing data and user interactions effectively. Powered by the Flask ecosystem, these plugins establish connections with the Graph Manager, facilitating real-time updates and data synchronization between frontend and backend.

The Graph Manager processes incoming requests from the frontend, executing necessary operations to create, retrieve, manipulate, or query data stored within the 2WAY Graph, and returning the results to the frontend. This includes tasks such as creating and retrieving objects, querying for relevant information, and managing access control and permissions.

To further enhance the functionality and efficiency of the 2WAY system, plugins can create and manage objects as well. This allows for centralized creation and management of objects, reducing redundancy and saving space in the graph. When plugins create these objects, they are automatically granted access permissions to all or designated users, including new users joining the system. This is managed through the Access Control List (ACL) object, ensuring proper access control and seamless integration of new objects. All operations conducted by plugins are securely authenticated using their unique cryptographic key-pairs, ensuring data integrity and security.

By leveraging Flask plugins, the frontend application can seamlessly interact with the Graph Manager and access the full range of functionalities offered by backend services. This enables users to perform actions such as creating new objects, updating existing data, querying information, and collaborating with other users, all while maintaining a responsive and intuitive user experience.

Overall, Flask plugins play a crucial role in bridging the gap between the frontend and backend components of the 2WAY system. They enable efficient communication and data exchange between the user interface and the server infrastructure. Through their integration into the Flask framework, these plugins empower developers to build rich, interactive applications that leverage the full capabilities of the 2WAY platform, ensuring a seamless and intuitive user experience.

<br>

## 1.4 Pre-Installed Plugins <a name="14-pre-installed-plugins"></a>

The 2WAY system's frontend comes with several pre-installed plugins designed to enhance user experience and provide essential functionality. These plugins integrate seamlessly with backend services, facilitating various interactions within the platform.

The Contacts plugin acts as a contact list or address book, allowing users to manage their network connections within the 2WAY system. Utilizing the 2WAY Graph, the Contacts plugin provides an intuitive interface for organizing and accessing contacts, enabling seamless communication and collaboration.

The Messages plugin builds on the Contacts plugin to offer peer-to-peer messaging capabilities. By leveraging contact information and network connections from the 2WAY Graph, the Messages plugin enables real-time message exchanges, fostering communication within the platform.

The Library plugin offers a comprehensive interface for browsing, searching, and filtering all objects from various plugins. Using degrees of separation within the 2WAY Graph, the Library plugin makes data management and retrieval intuitive and efficient, allowing users to easily locate and interact with information.

The Social plugin enriches the user experience by providing a social feed that aggregates the latest messages from contacts. This feed gives users a centralized view of their interactions and conversations, keeping them updated on relevant discussions and activities within their network. It enhances collaboration and communication by providing a platform for users to interact and share updates.

All of these plugins ensure data privacy and security by adhering to Access Control Lists (ACLs), which define users' permissions to access and manage their data.

These pre-installed plugins provide essential functionality for managing contacts, exchanging messages, and staying connected within the 2WAY platform. By leveraging the 2WAY Graph and integrating with backend services, these plugins enhance the overall user experience and contribute to the platform's effectiveness as a communication and collaboration tool.

<br>

## 1.5 Custom Plugins <a name="15-custom-plugins"></a>

Beyond the default functionality provided by the pre-installed plugins, the 2WAY system supports custom plugins, enabling developers to extend the platform's capabilities and tailor the user experience to specific needs. Custom plugins allow developers to introduce new features, integrate third-party services, and customize the frontend interface according to user requirements.

Built using the Flask framework, custom plugins can leverage Flask extensions and libraries to streamline development. This flexibility allows developers to create a wide range of plugins, from specialized communication tools to advanced data visualization and analytics.

One common use case for custom plugins is integrating external services or APIs. For instance, developers might create plugins that connect with social media platforms, enabling users to share content, import contacts, or interact with external communities seamlessly. These plugins can integrate with the system's Access Control Lists (ACLs) to ensure secure access to data across plugins, maintaining data privacy and security.

Custom plugins can also be tailored to specific industries, providing solutions for niche markets or specialized user groups. Examples include plugins for project management, customer relationship management (CRM), or e-commerce, allowing organizations to use the 2WAY platform for their business needs. Inter-plugin communication enables seamless integration between different plugins, allowing them to work together to provide comprehensive solutions.

Additionally, custom plugins can enhance user engagement by introducing gamification elements, personalized experiences, or advanced collaboration features. They can generate notifications or alerts to keep users informed about relevant events or updates within the system, providing users with a centralized view of their system activity. Proper error handling mechanisms ensure smooth operation and user experience.

Overall, custom plugins significantly enhance the functionality and versatility of the 2WAY platform. By supporting custom plugin development, the 2WAY system empowers developers to innovate and create solutions that meet unique user requirements, driving engagement and satisfaction.

<br><br>

# 2. Backend <a name="backend"></a>

<br>

## 2.1 Introduction to the Backend <a name="21-introduction-to-the-backend"></a>

The backend of the 2WAY system is the cornerstone of its decentralized identity, reputation, and access management framework. It is designed to handle the complex processes required to maintain secure, efficient, and reliable operations within the 2WAY ecosystem. This backend infrastructure supports the creation, management, and verification of cryptographic identities and facilitates secure data exchanges between trusted servers in a peer-to-peer (P2P) network.

At the core of the backend lies the 2WAY Graph, a comprehensive data structure integrating both the User Graphs and the Server Graph. The User Graph represents individual user interactions, while the Server Graph aggregates all User Graphs on a particular server, encapsulating a subset of the network’s decentralized data.

The backend manages various types of 2WAY Objects essential to the system's operation, including Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). Attributes are key-value pairs with a "type" and a "value". Ratings store reputation scores. Parents contain Attributes who can have one or more other Attributes as their children, and Edges establish the relationships between a Parent and its children. ACLs define and manage access permissions within the system. Each object can be up or down-voted indefinitely, influencing its visibility in the graph.

Several crucial components support the functionality and security of the 2WAY backend. The Database Schema ensures efficient data organization and structure. The Graph Manager handles message reception from the frontend, backend, or any connected application, ensuring secure and reliable communication. It manages changes to the 2WAY Graph in general and maintains the Graph in RAM, ensuring the integrity and updates of the active data structure, while the overall 2WAY Graph is stored to disk with the help of the Storage Manager. The Key Manager is responsible for signing logs, signing and verifying messages between servers, and handling the encryption and decryption of communications, ensuring secure interactions within the system.

The Network Manager manages network connections between servers, ensuring efficient data exchange. It tracks synchronized data with other servers and manages data pending synchronization on the next connection. It also protects the system from Denial of Service (DoS) attacks using proof-of-work-based client-puzzle challenges with dynamic difficulty levels to maintain network performance and availability.

Additional components enhance the backend's robustness and reliability. The Storage Manager handles physical data storage. The Log Manager records system activities for auditing and troubleshooting. The Installation and Startup Managers facilitate the deployment and initialization of the 2WAY system.

In essence, the 2WAY backend is a sophisticated and modular system that provides the secure and decentralized foundation needed for the 2WAY platform's operations. It integrates various components and data structures to create a resilient and efficient framework for managing digital identities and associated data in a P2P network. This section explains each element in detail, offering a comprehensive understanding of the backend architecture and its critical role within the 2WAY system.

<br>

## 2.2 2WAY Graph <a name="22-2way-graph"></a>

### 2.2.1 Introduction to the 2WAY Graph

The 2WAY Graph lies at the core of the 2WAY system, serving as a dynamic and interconnected framework for representing and organizing data.

At its essence, the 2WAY Graph is a directed graph-based data model that uses nodes and edges to model relationships and interactions between various entities within the system. Nodes represent individual objects such as Attributes, Parents, Ratings, and Access Control Lists (ACLs). Edge objects denote the connections and associations between Parent objects and their child Attributes.

The 2WAY Graph is decentralized and distributed, allowing users to create, share, and collaborate on data in a flexible and scalable manner. This graph-based approach facilitates intuitive navigation, exploration, and discovery of interconnected data. Users can traverse relationships and uncover valuable insights within their social or organizational networks.

This decentralized architecture ensures robustness and resilience, as data is not reliant on a single central server. Instead, it is distributed across multiple nodes, enhancing data security and availability. Moreover, the graph-based structure supports complex queries and analyses, enabling users to identify patterns and correlations that might be difficult to detect using traditional data models.

<br>

### 2.2.2 User Graph

The User Graph in the 2WAY system represents each user's unique network of nodes and edges, encapsulating their personal data, connections, and interactions. This graph reflects each user's contributions and relationships within the broader context of the Server Graph, which is the aggregate of all User Graphs in the system. Each User Graph is distinct, depicting specific interactions, preferences, and network connections.

Users always query data from their zeroth degree, meaning they primarily interact with and retrieve data directly relevant to them or within their immediate network connections. When querying the Server Graph, users explore their own graph, accessing relationships, application data, and interactions pertinent to them.

From the user's perspective, data in other User Graphs that don't overlap with their own is essentially invisible. Users only perceive and interact with data within their own User Graph or data directly connected to them through their network connections. Data outside their immediate network or areas of interest remains inaccessible.

This approach ensures users maintain a focused and personalized view of the data within the 2WAY system. It allows them to efficiently navigate and interact with information relevant to their needs and interests. By querying from their zeroth degree within the Server Graph, users can effectively manage their data, discover relevant connections, and collaborate with others in their network while maintaining privacy and control over their personal information.

Plugins in the 2WAY system can also create and manage objects through the Graph Manager. Each plugin has its own cryptographic key-pair, effectively making them users within the system. This allows plugins to function similarly to human users, with their own unique User Graphs, nodes, and edges. Plugins can create objects on behalf of multiple users, ensuring that not every user needs to create these objects individually, thus saving space in the graph.

When plugins create or manage objects, either all users or designated users receive access to them. New users can automatically receive access to these plugin-created objects as well. The relevant Access Control List (ACL) objects are updated to ensure proper permissions are set for these plugin-created objects, maintaining seamless integration and efficient access management.

By incorporating plugins as users with their own cryptographic key-pairs, the 2WAY system enhances its flexibility and scalability, allowing automated processes to contribute to the graph while ensuring secure and controlled access to data.

<br>

### 2.2.3 Server Graph

The Server Graph in the 2WAY system represents the aggregation of all individual User Graphs stored on the server. Each user maintains a directed graph comprising nodes and edges that represent their objects and relationships. The Server Graph consolidates these individual User Graphs into a comprehensive network of interconnected data.

At its core, the Server Graph serves as a unified repository that encompasses the system's data landscape. It includes objects such as Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs), all contributed by users. By consolidating User Graphs into a centralized repository, the Server Graph facilitates seamless communication, collaboration, and data sharing among users.

The Server Graph is dynamic and continually evolving, reflecting real-time interactions and updates made by users. As users create, modify, hide, or delete objects within their graphs, these changes are propagated to the Server Graph, ensuring it remains synchronized and up-to-date with the latest data from all users.

The Server Graph is the backbone of the 2WAY system, embodying the collective intelligence and contributions of its user base. By unifying individual User Graphs, it enables efficient data management, discovery, and collaboration, while ensuring privacy, security, and access control based on user-defined permissions and network connections.

<br>

### 2.2.4 Graph on Disk

The Graph on Disk in the 2WAY system refers to the storage mechanism used to persist the Server Graph, which comprises aggregated data from all individual User Graphs, onto disk. This disk-based representation ensures the durability, accessibility, and scalability of the system's data, enabling efficient storage and retrieval of information across the entire user base.

The Server Graph, in its entirety, is stored on disk using the SQL schema discussed in "2.4 Database Schema". This schema design organizes data into pre-defined separate tables for each plugin, corresponding to specific object types such as Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). By leveraging a relational database management system (RDBMS) like SQLite3, the Server Graph can be efficiently persisted and managed on disk, facilitating seamless data storage and retrieval operations.

The Graph on Disk serves as the authoritative source of truth for the 2WAY system, housing the complete dataset that encompasses the collective intelligence and contributions of users. Updates, modifications, and interactions made by users are reflected in real-time within the Server Graph on disk, ensuring that data remains synchronized and up-to-date with the latest user activity.

Furthermore, the Graph on Disk enables efficient querying, filtering, and analysis of data within the 2WAY system, empowering users to explore connections, discover insights, and collaborate effectively within their network. By persisting the Server Graph to disk using the established SQL schema, the 2WAY system maintains data integrity, consistency, and reliability while facilitating seamless data management and scalability for future growth and expansion.

<br>

### 2.2.5 Graph in RAM

In the 2WAY system, the Graph in RAM serves as an in-memory representation of a subset of the Server Graph, temporarily stored in the system's Random Access Memory (RAM). It employs the NetworkX library, a robust tool for Python, to populate and manage graph data structures efficiently.

One pivotal function of the Graph in RAM is to store the table record IDs of public key Attributes from the disk-based database. These attributes function as nodes in the graph, each representing a user within the system. By retaining these record IDs in memory, the system can swiftly retrieve and access relevant nodes during query operations, thereby facilitating efficient traversal and exploration of the Server Graph.

The design of the Graph in RAM is optimized for expeditious querying of data from the disk-based Server Graph. When a query is initiated, the system first fetches pertinent nodes from the in-memory graph, based on the specified degree of separation. These nodes serve as starting points for traversing the Server Graph on disk, enabling the system to narrow down the query scope and retrieve only essential data.

Moreover, the Graph in RAM can be dynamically extended with additional 2WAY objects as required to accelerate querying for specific data. For instance, frequently queried Attributes or Parents within a user's immediate network could be cached in memory to expedite subsequent query operations. However, it's important to note that this caching mechanism falls beyond the scope of this proof-of-concept.

It's imperative to acknowledge that maintaining a Graph in RAM entails a relatively high resource cost compared to directly accessing data from the SQL database. While in-memory operations offer speed advantages, they consume system resources and memory, potentially affecting overall system performance. Therefore, the Graph in RAM should be used judiciously, focusing on caching frequently accessed data or optimizing specific query patterns to enhance overall responsiveness and user experience within the 2WAY system.

<br>

## 2.3 2WAY Objects <a name="23-2way-objects"></a>

### 2.3.1 Introduction to 2WAY Objects

In 2WAY, a small set of simple data structures are used to construct objects. These objects, represented as nodes and edges within the 2WAY Graph, encompass all the data stored within the system. The flexibility of these objects allows the system to model a wide range of applications and data structures, with the graph structure facilitating data organization and relationships.

The following objects are used to construct the system in its entirety:

1. **Attribute**: A key-value pair consisting of a "type" (the key, not to be confused with any cryptographic keys) and a "value". Attributes represent the basic units of information. For example, an Attribute could be a public key (`{"type": "pubkey", "value": "ABC123"}`), a username (`{"type": "username", "value": "alice"}`), or any other required entity.

2. **Parent**: A Parent Attribute that is connected to one or more child Attributes via an Edge object. This allows the organization of Attributes into hierarchical structures. For instance, a Parent Attribute could represent a user by its public key, with child Attributes representing their various properties like username and email address, a group containing members, a category and its products, etc.

3. **Edge**: An Edge represents a connection between a single Parent Attribute and one or more child Attributes. Edges define relationships within the graph, enabling complex data structures. For example, an Edge might connect a user Attribute to their various properties, a group to its members, or a category to its products.

4. **Rating**: A score with a rating scale and/or comment, pointing at an Attribute or Parent. Ratings provide a way to evaluate and rank Attributes. The specific scores and scales for ratings are defined by the plugins, allowing for customization based on the needs of different applications. For example, one plugin might use ratings to represent a user's reputation score, while another might use ratings to indicate the ranking of a movie or book. This flexibility allows developers to implement any rating system required by their application.

5. **Access Control List (ACL)**: The ACL in 2WAY is a key mechanism for managing user permissions within the system. It links a user's public key, or "pubkey", Attribute to specific Attributes or Parents for which they have read permissions. During state synchronization between servers, the ACL determines which data is synchronized based on established permissions, ensuring users only receive data they are authorized to access. This maintains data privacy and security within the system.

Using these objects, any required application can be modeled atop the 2WAY platform. The object model is both flexible and extensible, allowing developers to create custom structures and relationships tailored to their specific needs. The combination of Attributes, Parents, Edges, Ratings, and ACLs provides a robust foundation for building decentralized applications that prioritize security, privacy, and user control.

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
  "app_id": "hashed_app_identifier",
  "type": "name",
  "value": "Alice",
  "vote": "1"
}
```

In this JSON structure:
- `object` indicates that this is an Attribute.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Attribute. `0` = self, for "pubkey" Attributes.
- `app_id` signifies the hashed application identifier to ensure uniqueness and prevent naming collisions.
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
  "app_id": "hashed_app_identifier",
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
- `app_id` signifies the hashed application identifier to ensure uniqueness and prevent naming collisions.
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

## 2.4 Database Schemas <a name="24-database-schema"></a>

### 2.4.1 Introduction to the Database Schemas

The database schema for the 2WAY system encompasses both the frontend and backend structures, meticulously designed to support seamless data management across the entire platform. This schema is implemented using SQLite3, chosen for its versatility and compatibility across various systems, aligning perfectly with 2WAY’s lightweight and accessible nature. While future iterations may explore alternative databases, SQLite3 currently demonstrates the protocol’s scalability and efficiency, particularly as it transitions to more robust environments.

In the frontend schema, the central `users` table plays a pivotal role in managing user data within 2WAY. Key columns include `id`, serving as the primary identifier in the database, and `user_id`, which references the record ID of the user’s public key Attribute stored in the backend. Other essential columns include `email`, `password`, `roles`, `is_active`, and `email_confirmed_at`, ensuring comprehensive user management capabilities.

Alongside the `users` table, the schema incorporates tables crucial for Flask-User's role functionality. These include the `roles` table, defining unique role names with an auto-incrementing primary key (`id`). The `user_roles` table establishes relationships between users and roles, ensuring seamless role assignment and management. Foreign key constraints (`REFERENCES users(id) ON DELETE CASCADE` for `user_id` and `REFERENCES roles(id) ON DELETE CASCADE` for `role_id`) maintain data integrity by cascading deletions when users or roles are removed from the system.

In the backend, data segmentation into distinct tables and establishment of relationships via foreign keys ensure robust data integrity and facilitate efficient querying and retrieval operations within SQLite3. This schema framework supports the creation, modification, storage, and retrieval of diverse objects critical to 2WAY’s operation, including user data, reputation metrics, access controls, and other pertinent information, structured in a cohesive manner.

Each plugin in the 2WAY ecosystem adheres to a consistent schema design within the backend database, as detailed in section 2.4.3, "Backend Database Schema Design". This approach prevents conflicts between plugins and enables seamless data access and utilization across different modules, fostering collaboration and synergy.

To ensure distinctiveness and recognizability of plugin-specific tables, each plugin is assigned a unique `app_id`, secured by a SHA2 hash. For example, the Contacts plugin may use `0e532062ea04fa80e54a0c3cda66f72c7c173f20b73f72541210da8a` as its `app_id`, resulting in tables like `0e532062ea04fa80e54a0c3cda66f72c7c173f20b73f72541210da8a_attributes` and `0e532062ea04fa80e54a0c3cda66f72c7c173f20b73f72541210da8a_parents`.

This meticulous schema design fosters interoperability and seamless integration among plugins within the 2WAY system. By maintaining consistent naming conventions and structural guidelines, plugins can easily interact and share data, promoting code reuse and simplifying the development process while ensuring compatibility across diverse plugin functionalities.

The flexibility of assigning multiple `app_id` identifiers to a single application allows for the inclusion of various plugin configurations within the same database environment. This capability ensures that plugins can coexist harmoniously while maintaining data isolation and encapsulation, empowering developers to tailor plugin combinations to specific use cases effectively. Ultimately, this approach enhances the platform’s versatility, adaptability, and scalability.

In essence, the replication of database schema per plugin underscores 2WAY’s commitment to modularity, flexibility, and interoperability. It enables developers to extend the platform with new features seamlessly while upholding consistency and compatibility across the entire ecosystem.

<br>

### 2.4.2 Frontend Database Schema Design

The frontend database schema for 2WAY is pivotal in managing user information and authentication, ensuring robust security and functionality. At its core, the schema includes the following tables:

1. **users Table**:
   - **id**: Unique identifier for each user.
   - **user_id**: Reference to the record ID of the user's public key in the backend.
   - **email**: Email address of the user.
   - **password**: Encrypted password for user authentication.
   - **roles**: Roles assigned to the user, facilitating role-based access control.
   - **is_active**: Flag indicating whether the user account is active.
   - **email_confirmed_at**: Timestamp indicating when the user's email was confirmed.

2. **roles Table**:
   - **id**: Auto-incrementing primary key for role identification.
   - **name**: Unique name of the role.

3. **user_roles Table**:
   - **id**: Auto-incrementing primary key for the user-role relationship.
   - **user_id**: Foreign key referencing the `id` column in the `users` table (`REFERENCES users(id) ON DELETE CASCADE`).
   - **role_id**: Foreign key referencing the `id` column in the `roles` table (`REFERENCES roles(id) ON DELETE CASCADE`).

This schema facilitates comprehensive user management within the frontend, supporting user registration, authentication, and role assignment through a structured approach. The `users` table stores essential user details, while the `roles` and `user_roles` tables enable effective role-based access control, ensuring secure and efficient operations within the 2WAY platform.

By leveraging SQLite3 for the frontend schema, 2WAY maintains compatibility and scalability, accommodating future enhancements and optimizations as the platform evolves. This frontend schema lays a solid foundation for user-centric functionalities, emphasizing security, performance, and usability across diverse user roles and interactions.

<br>

### 2.4.3 Backend Database Schema Design

Here are the core tables in the schema:

1. **Attributes Table**:
   - **id** INT: Unique identifier for the attribute.
   - **type** TEXT: Type of the attribute.
   - **signer** INT: Refers to the record ID that stores the public key (pubkey) of the user creating the Attribute. `0` = self.
   - **value** TEXT: Value of the attribute.
   - **vote** INT: Vote count for the attribute.
   - **timestamp** INT: Timestamp of the attribute creation or modification.
   - **hash** TEXT: Hash of the document.
   - **PRIMARY KEY (id)**: Primary key ensuring uniqueness.

2. **Parents Table**:
   - **id** INT: Unique identifier for the parent.
   - **type** TEXT: Type of the parent.
   - **signer** INT: Refers to the record ID that stores the public key (pubkey) of the user creating the Parent.
   - **parent_id** INT: Identifier of the parent.
   - **vote** INT: Vote count for the parent.
   - **timestamp** INT: Timestamp of the parent creation or modification.
   - **hash** TEXT: Hash of the document.
   - **PRIMARY KEY (id)**: Primary key ensuring uniqueness.
   - **FOREIGN KEY (parent_id) REFERENCES twoway_connections_attributes(id) ON DELETE CASCADE**: Ensures referential integrity with the Attributes table.

3. **Edges Table**:
   - **id** INT: Unique identifier for the edge.
   - **type** TEXT: Type of the edge.
   - **signer** INT: Refers to the record ID that stores the public key (pubkey) of the user creating the Edge.
   - **parent_id** INT: Identifier of the parent node.
   - **child_ids** TEXT: Comma-separated list of child node IDs.
   - **vote** INT: Vote count for the edge.
   - **timestamp** INT: Timestamp of the edge creation or modification.
   - **hash** TEXT: Hash of the document.
   - **PRIMARY KEY (id)**: Primary key ensuring uniqueness.
   - **FOREIGN KEY (parent_id) REFERENCES twoway_connections_parents(id) ON DELETE CASCADE**: Ensures referential integrity with the Parents table.

4. **Rating Table**:
   - **id** INT: Unique identifier for the rating entry.
   - **type** TEXT: Type of the rating entry.
   - **signer** INT: Refers to the record ID that stores the public key (pubkey) of the user creating the Rating.
   - **attribute_id** INT: Identifier of the related attribute.
   - **parent_id** INT: Identifier of the related parent.
   - **comment** TEXT: Comment associated with the rating entry.
   - **score** TEXT: Score given in the rating entry.
   - **scale** TEXT: Scale of the score.
   - **timestamp** INT: Timestamp of the rating entry creation or modification.
   - **hash** TEXT: Hash of the document.
   - **PRIMARY KEY (id)**: Primary key ensuring uniqueness.
   - **FOREIGN KEY (attribute_id) REFERENCES twoway_connections_attributes(id) ON DELETE CASCADE**: Ensures referential integrity with the Attributes table.
   - **FOREIGN KEY (parent_id) REFERENCES twoway_connections_parents(id) ON DELETE CASCADE**: Ensures referential integrity with the Parents table.

5. **ACL Table**:
   - **id** INT: Unique identifier for the ACL entry.
   - **signer** INT: Refers to the record ID that stores the public key (pubkey) of the user creating the ACL.
   - **pubkey_id** INT: Identifier of the public key.
   - **permissions** TEXT: Permissions associated with the ACL entry.
   - **timestamp** INT: Timestamp of the ACL entry creation or modification.
   - **hash** TEXT: Hash of the document.
   - **PRIMARY KEY (id)**: Primary key ensuring uniqueness.
   - **FOREIGN KEY (pubkey_id) REFERENCES twoway_connections_attributes(id) ON DELETE CASCADE**: Ensures referential integrity with the Attributes table.

<br>

## 2.5 Graph Manager <a name="25-graph-manager"></a>

### 2.5.1 Introduction to the Graph Manager

In the 2WAY system, the Graph Manager is the central hub for managing graph data, including creating, querying, modifying, and deleting core objects like Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). It ensures efficient data handling and consistency through APIs.

Users interact with the frontend interface to create or manage objects, which sends API calls containing data such as Attribute key-value pairs or parent-child relationships to the backend's Graph Manager. The Graph Manager processes these requests, handles logging and signing by forwarding relevant information to the Key Manager and Log Manager, and maintains synchronization between the Graph in RAM and the disk-based Server Graph.

Querying objects is done through API calls to the Graph Manager, specifying parameters like the degree of separation from the user's public key and object type. The Graph Manager retrieves relevant nodes from the Graph in RAM and, if needed, fetches additional data from the disk with the Storage Manager. The queried data is then returned to the frontend.

By consolidating object management in the Graph Manager and exposing functionalities through APIs, the 2WAY system ensures consistency, security, and scalability. This approach simplifies database interactions, enhancing system usability and maintainability.

In this proof-of-concept, message signing on the frontend is not supported. Future versions may introduce frontend or hardware key signing for added security.

The Graph Manager synchronizes the Graph in RAM with the Server Graph during system initialization, shutdown, or significant updates, ensuring data consistency. It updates nodes and edges in the Graph in RAM when changes occur, such as adding or removing connections.

For query operations, the Graph Manager retrieves nodes by degree of separation from the user's public key within the Server Graph. Users query the Graph Manager to obtain table record IDs of relevant nodes for efficient data exploration.

The proof-of-concept focuses on storing record IDs of public key Attributes with `app_id` `0e532062ea04fa80e54a0c3cda66f72c7c173f20b73f72541210da8a` as a SHA2 hash in the table `0e532062ea04fa80e54a0c3cda66f72c7c173f20b73f72541210da8a_attributes`. For example, if Alice signs her own public key, it is stored as an Attribute with the record ID `1`, and a corresponding node is added to the Graph in RAM. If Alice adds Bob's public key as an Attribute with record ID `34`, a node and edge are added to the Graph in RAM. When a `pubkey` Attribute is down-voted, the node and edge are removed, unless edges from other nodes remain.

Future versions may allow adding and removing other Attributes or Parents to and from the Graph in RAM, but this is beyond the proof-of-concept's scope.

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
  "app_id": "hashed_app_identifier",
  "type": "name",
  "value": "Alice",
  "vote": "1"
}
```
In this JSON structure:
- `object` specifies the type of object being created, which is an `attribute`.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Attribute. `0` = self, for "pubkey" Attributes.
- `app_id` is the unique identifier for the application, hashed for security.
- `type` indicates the type of the attribute, in this case, `name`.
- `value` is the value of the attribute, here it is `Alice`.
- `vote` denotes the relevance or importance of the attribute, set to `1`.

### Creating Parents
```json
{
  "object": "parent",
  "action": "new",
  "signer": "user_id",
  "app_id": "hashed_app_identifier",
  "parent_id": 123,
  "vote": "1"
}
```
In this JSON structure:
- `object` specifies the type of object being created, which is a `parent`.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Parent.
- `app_id` is the unique identifier for the application, hashed for security.
- `parent_id` is the identifier for the Parent object.
- `vote` denotes the relevance or importance of the Parent, set to `1`.

### Creating Edges
```json
{
  "object": "edge",
  "action": "new",
  "signer": "user_id",
  "app_id": "hashed_app_identifier",
  "parent_id": 123,
  "child_ids": [456, 789],
  "vote": 1
}
```
In this JSON structure:
- `object` specifies the type of object being created, which is an `edge`.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`).
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user creating the Edge.
- `app_id` is the unique identifier for the application, hashed for security.
- `parent_id` is the identifier for the Parent node.
- `child_ids` is a list of identifiers for the child nodes.
- `vote` denotes the relevance or importance of the edge, set to `1`.

### Creating Ratings
```json
{
  "object": "rating",
  "action": "new",
  "signer": "user_id",
  "app_id": "hashed_app_identifier",
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
- `app_id` is the unique identifier for the application, hashed for security.
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
  "app_id": "hashed_app_identifier",
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
- `app_id` is the unique identifier for the application, hashed for security.
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
  "app_id": "hashed_app_identifier",
  "type": "name",
  "value": "Alice",
  "vote": "0"
}
```

In this JSON structure:
- `object` specifies the type of object being updated or down-voted, which is an `attribute`.
- `action` describes the interaction with the object (`new`, `edit`, or `delete`), in this case `edit`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user making the change.
- `app_id` is the unique identifier for the application, hashed for security.
- `type` indicates the type of the attribute, in this case, `name`.
- `value` is the value of the attribute, here it is `Alice`.
- `vote` denotes the relevance or importance of the attribute, set to `0` indicating down-vote.

In case of logging, upon receiving this JSON document, the Graph Manager forwards the document to the Key Manager for signing.

```json
{
  "object": "attribute",
  "action": "edit",
  "signer": "user_id",
  "app_id": "hashed_app_identifier",
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
  "app_id": "hashed_app_identifier",
  "type": "book_title",
  "value": "",
  "degree": 2,
  "vote": 1
}
```

In this JSON structure:
- `object` specifies the type of object being queried, which is an `attribute`.
- `signer` refers to the record ID of the Attribute that stores the public key (pubkey) of the user querying the data.
- `app_id` is the unique identifier for the application, hashed for security.
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
  "app_id": "hashed_app_identifier",
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
  "app_id": "hashed_app_identifier",
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
- `app_id` is the unique identifier for the application, hashed for security.
- `criteria` is an object that contains the specific parameters for filtering:
  - `type` indicates the type of the Attribute, in this case, `first_name`.
  - `value` is the value of the Attribute to filter by, here it is `Alice`.
  - `degree` specifies the degree of separation for the query, set to `3`.
  - `vote` denotes the relevance or importance of the Attribute, set to `1`.

Upon receiving this JSON document, the Graph Manager applies the specified filtering criteria to the queried data, returning only the objects that match the given criteria. This enables users to efficiently retrieve and analyze data based on their specific requirements.

### Filtering by Parent

To filter objects based on Parents, users can specify criteria for Parents in their query. Below is an example of a JSON document for filtering objects that have a specific parent relationship:

```json
{
  "object": "parent",
  "signer": "user_id",
  "app_id": "hashed_app_identifier",
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
- `app_id` is the unique identifier for the application, hashed for security.
- `criteria` is an object that contains the specific parameters for filtering:
  - `parent_type` indicates the type of the parent object to filter by, in this case, `book_title`.
  - `parent_value` specifies the value of the parent object, which is left empty in this example.
  - `degree` specifies the degree of separation for the query, set to `1`.
  - `vote` denotes the relevance or importance of the parent relationship, set to `1`.

### Filtering by Ratings

To filter objects based on Ratings, users can specify criteria for Ratings in their query. Below is an example of a JSON document for filtering objects that have positive ratings:

```json
{
  "object": "rating",
  "signer": "user_id",
  "app_id": "hashed_app_identifier",
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
- `app_id` is the unique identifier for the application, hashed for security.
- `criteria` is an object that contains the specific parameters for filtering:
  - `min_score` indicates the minimum score to filter by, set to `6`.
  - `scale` specifies the scale of the Rating, in this case, `out-of-10`.
  - `degree` specifies the degree of separation for the query, set to `1`.
  - `vote` denotes the relevance or importance of the Rating, set to `1`.

### Filtering by ACL

To filter objects based on Access Control Lists (ACLs), users can specify criteria for ACLs in their query. Below is an example of a JSON document for filtering objects that meet certain ACL criteria:

```json
{
  "object": "acl",
  "signer": "user_id",
  "app_id": "hashed_app_identifier",
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
- `app_id` is the unique identifier for the application, hashed for security.
- `criteria` is an object that contains the specific parameters for filtering:
  - `type` indicates the type linked to the ACL, left empty in this case, returning all relevant objects.
  - `value` specifies the value linked to the ACL, left empty in this case, returning all relevant objects.
  - `permissions` indicates the level of permissions required, set to `1`.
  - `degree` specifies the degree of separation for the query, set to `1`.
  - `vote` denotes the relevance or importance of the ACL, set to `1`.

### Comprehensive Filtering

Here is a more extensive and potentially UX-friendly search query example that demonstrates filtering based on various criteria, including Attributes, Ratings, and relationships:

**Goal:** Retrieve all "phone numbers" (Attributes with type=”phone_number” and any value) of "restaurants" (Parent object), apart from "The French Cock" (attribute; type="restaurant" and value="The French Cock"), with "positive ratings" (Rating object) from "Friends" (Parent object) and "Family" (Parent object), but not "people with bad taste in food" (Parent object) in zeroth degree, and signed by anyone within 2 degrees of separation or less.

```json
{
  "object": "attribute",
  "signer": "user_id",
  "app_id": "hashed_app_identifier",
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
- `app_id` is the unique identifier for the application, hashed for security.
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

When a user, such as Alice, initially stores her own public key, an Attribute is created with a distinct record ID stored in the `0e532062ea04fa80e54a0c3cda66f72c7c173f20b73f72541210da8a_attributes` table.

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
  "app_id": "hashed_app_identifier",
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
  "app_id": "hashed_app_identifier",
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
- `app_id` is the hashed identifier for the application for security purposes.
- `criteria` contains specific parameters for filtering:
  - `type` specifies the type of attribute being queried, in this case, `first_name`.
  - `value` indicates the value to filter by, which is `Alice`.
  - `degree` denotes the degree of separation for the query, set to `2`.
  - `vote` specifies the relevance or importance of the attribute, set to `1`.
  - `connections` is an array of record IDs representing the `pubkey` Attributes retrieved from the Graph in RAM.

This query effectively retrieves data from the Graph on Disk based on the user's original query and the specific "pubkey" Attributes identified in the previous step. The Storage Manager ensures that the queried data matches the specified criteria, providing accurate and relevant results to the user.

The Graph Manager formats this data and sends it back to the frontend interface for user interaction. An example of the JSON document representing the query results might look like this:

Certainly! Here's an explanation for the provided JSON document:

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
  "app_id": "hashed_app_identifier",
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
- `app_id` is the hashed identifier for the application for security purposes.
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

<br><br>

## 2.6 Storage Manager <a name="26-storage-manager"></a>

### 2.6.1 Introduction to the Storage Manager

The Storage Manager in the 2WAY system is a pivotal component designed to manage the efficient storage and retrieval of data from the Graph on Disk. Its primary role is to interface between the Graph in RAM, which handles dynamic and transient data, and the persistent storage layer, ensuring that data integrity, accessibility, and performance are maintained across the system.

At its core, the Storage Manager is responsible for persisting data that is critical for long-term access and analysis. This includes user Attributes, relationships, and various metadata that constitute the Graph in RAM. When users interact with the system, the Graph Manager first processes their queries in RAM, utilizing the fast, in-memory graph structures to provide immediate responses. However, for any data that needs to be persisted, referenced later, or queried with more complex criteria, the Storage Manager comes into play, managing the transition between volatile and non-volatile storage.

When a user initiates a query, the Graph Manager retrieves relevant nodes from the Graph in RAM, focusing on the specified degrees of separation and filtering criteria. For instance, a user might request nodes within two degrees of separation that represent public key Attributes and have been upvoted. Once the Graph Manager identifies these nodes, represented as record IDs, the Storage Manager takes over to fetch the comprehensive data from the Graph on Disk. This two-tiered approach leverages the speed of in-memory processing while ensuring the durability and richness of disk-based storage.

The Storage Manager uses a sophisticated indexing system to quickly locate and retrieve the necessary data. Each record ID from the Graph in RAM corresponds to an entry in the disk storage, where detailed information about Attributes, such as public keys, names, and other user-defined properties, is stored. This allows the Storage Manager to efficiently assemble the full dataset required by the user's query. For example, if the initial query returned nodes with record IDs [34, 56, 78, 102], the Storage Manager would use these IDs to pull detailed records from the Graph on Disk, including timestamps, votes, and any other relevant metadata.

Furthermore, the Storage Manager is equipped to handle complex queries that involve hierarchical relationships between Attributes. Consider a scenario where a user wishes to retrieve full names associated with specific public key Attributes returned in a previous query. The Storage Manager can interpret and execute nested queries that define parent-child relationships between Attributes. By processing these relationships, it can link public key Attributes to their associated full names or any other related data, providing a comprehensive view of the interconnected Attributes stored within the system.

The robustness of the Storage Manager also extends to ensuring data integrity and consistency. It implements various mechanisms to safeguard against data corruption and to maintain synchronization between the Graph in RAM and the Graph on Disk. This is crucial in a system like 2WAY, where real-time updates and historical data need to coexist seamlessly. By maintaining a coherent and synchronized state across different storage layers, the Storage Manager guarantees that the data users interact with is both current and accurate.

In summary, the Storage Manager is an indispensable element of the 2WAY system, bridging the gap between transient in-memory data and persistent disk storage. It provides the necessary infrastructure to store, retrieve, and manage complex user data efficiently, ensuring that the system can handle both immediate query responses and long-term data persistence. By managing the detailed Attributes and relationships within the Graph on Disk, the Storage Manager supports the system's overarching goal of delivering a responsive, reliable, and scalable user experience.

<br>

### 2.6.2 Storage Engine

#### 2.6.2.1 Create Database and Tables

#### 2.6.2.2 Storage and Retrieval

<br>

## 2.7 Key Manager <a name="27-key-manager"></a>

### 2.7.1 Introduction to the Key Manager

The Key Manager within the 2WAY system is designed to securely generate, manage, and utilize cryptographic keys for users, underpinning the system's robust security architecture. It facilitates a range of cryptographic operations such as key generation, signature verification, message signing, encryption, and decryption, ensuring the integrity, authenticity, and confidentiality of user interactions.

Each user within the 2WAY system can manage multiple cryptographic key-pairs, supporting a variety of applications under a single identity. This is achieved through the implementation of Hierarchical Deterministic (HD) Keys, which create a structured, tree-like hierarchy where a single master key can generate multiple child keys. This structure simplifies key management, enabling users to derive new keys as needed without compromising the security of the master key.

Hierarchical Deterministic Keys are essential for maintaining an organized and efficient key management system. Each derived key serves a unique purpose and is cryptographically linked to the master key, providing a secure means to handle multiple cryptographic tasks. For instance, users can employ one key for authenticating their identity, another for signing messages, and additional keys for interactions with trusted third parties. This hierarchical approach compartmentalizes cryptographic functions, enhancing both security and usability.

The Key Manager also incorporates Zero-Knowledge Proofs (ZKPs), a powerful cryptographic technique that allows users to prove the validity of certain information without revealing the information itself. ZKPs are integral to preserving privacy and security within the 2WAY system, enabling secure user authentication, transaction verification, and protected communications. By leveraging ZKPs, the Key Manager ensures that sensitive information remains confidential and is not exposed during verification processes.

Integration with the parent-child relationships within the 2WAY system further enhances the functionality of the Key Manager. Users can manage their keys effectively by aligning them with these relationships, using a primary key for identity verification and secondary keys for specific tasks like message signing or encryption. This hierarchical and relational approach streamlines key management and strengthens security by isolating different cryptographic functions.

The Key Manager provides seamless integration for key generation, ensuring that keys are securely created and stored. For message signing and verification, the Key Manager uses advanced algorithms to maintain the authenticity and integrity of communications. Encryption and decryption operations are performed with cutting-edge cryptographic techniques, protecting the confidentiality of user data against unauthorized access.

Revocation and re-issuance of keys are crucial functionalities supported by the Key Manager. In the event of key compromise or the need for key updates, the Key Manager facilitates the revocation of the old key and the issuance of a new one. This process is critical for maintaining the long-term security and reliability of the 2WAY system, ensuring that users can continue their interactions securely without disruption.

In summary, the Key Manager is a pivotal component of the 2WAY system, providing comprehensive cryptographic support to secure and streamline user interactions. By implementing Hierarchical Deterministic Keys and Zero-Knowledge Proofs, the Key Manager ensures robust key management, secure communications, and effective integration with the hierarchical structure of the 2WAY system. This empowers users to confidently manage their cryptographic needs, knowing their interactions within the 2WAY ecosystem are safeguarded by state-of-the-art security practices.

<br>

### 2.7.2 Key Engine

#### 2.7.2.1 Generate Keys

#### 2.7.2.2 Verify Signatures

#### 2.7.2.3 Sign Messages

#### 2.7.2.4 Encrypt Messages

#### 2.7.2.5 Decrypt Messages

### 2.7.3 Revocation and Re-Issuance

<br>

## 2.8 Log Manager <a name="28-log-manager"></a>

### 2.8.1 Introduction to the Log Manager

The Log Manager is a critical component of the 2WAY system, designed to ensure the integrity, reliability, and security of the platform by meticulously recording and managing logs of various operational activities. It functions as the central repository for all logging activities, capturing detailed information about system events, including successful operations, errors, warnings, and other significant occurrences. This comprehensive logging mechanism is essential for maintaining the system's health, troubleshooting issues, and providing a reliable audit trail for security and compliance purposes.

In the 2WAY system, the Log Manager interfaces seamlessly with various components, including the Network Manager and its Bastion Engine, the Graph Manager, the Storage Manager, the Key Manager, and other subsystems. It ensures that all significant events, particularly those involving failed operations, failed Bastion messages, and failed incoming and outgoing messages, are accurately logged and stored for future reference.

One of the primary roles of the Log Manager is to handle logging for failed operations within the system. Failed operations can encompass a wide range of issues, from minor warnings to critical errors that may impact system functionality. By logging these events, the Log Manager provides valuable insights into system performance, helping administrators identify and resolve issues promptly. This logging capability is instrumental in maintaining the overall stability and reliability of the 2WAY platform.

Another crucial aspect of the Log Manager's functionality is the logging of failed Bastion messages. The Bastion Engine, a vital part of the Network Manager, plays a pivotal role in establishing secure connections between servers. It employs client-puzzle challenges to authenticate first-degree network connections, dynamically adjusting the difficulty of these puzzles based on the number of incoming connections to mitigate Denial of Service (DoS) attacks. When a client-puzzle challenge fails or a Bastion message does not get delivered, the Log Manager records these events, ensuring that any issues in the authentication process are documented for analysis and troubleshooting.

In addition to Bastion message logging, the Log Manager also captures logs of failed incoming and outgoing messages handled by the Network Manager. Once a connection is authenticated via the Bastion Engine, subsequent communications are managed by the Incoming Engine and Outgoing Engine. These engines handle message delivery, ensuring that data is transmitted securely and reliably between users and servers. Any failures in this message delivery process, whether due to network issues, server errors, or other disruptions, are meticulously logged by the Log Manager. This logging ensures that administrators have a clear view of message flow within the system and can address any communication problems that arise.

The Log Manager adheres to best practices in logging and monitoring, ensuring that logs are comprehensive, secure, and easily accessible for authorized personnel. Logs are typically timestamped and include detailed metadata, such as the source of the log entry, the nature of the event, and any relevant contextual information. This level of detail is crucial for effective troubleshooting and forensic analysis, enabling administrators to trace issues back to their root cause and implement corrective measures.

Security is a paramount concern in the design of the Log Manager. Logs often contain sensitive information, and it is essential to protect them against unauthorized access and tampering. The Log Manager employs robust security measures, including encryption and access controls, to safeguard log data. These measures ensure that only authorized personnel can access logs and that the integrity of the log data is maintained at all times.

Furthermore, the Log Manager supports integration with external monitoring and alerting systems. By providing real-time log data to these systems, the Log Manager enables proactive monitoring of the 2WAY platform. Administrators can set up alerts for specific events or patterns, allowing them to respond swiftly to potential issues and mitigate risks before they escalate into significant problems.

In summary, the Log Manager is an indispensable component of the 2WAY system, providing comprehensive logging capabilities that enhance system reliability, security, and operational transparency. By meticulously recording failed operations, failed Bastion messages, and failed incoming and outgoing messages, the Log Manager ensures that administrators have the information they need to maintain the health and performance of the platform. Its adherence to best practices in logging and security further solidifies its role as a cornerstone of the 2WAY system's infrastructure.

<br>

### 2.8.2 Log Engine

#### 2.8.2.1 Logging Failed Operations

#### 2.8.2.2 Logging Failed Bastion Messages

#### 2.8.2.3 Logging Failed Incoming Messages

<br>

## 2.9 Network Manager <a name="29-network-manager"></a>

### 2.9.1 Introduction to the Network Manager

The Network Manager is a pivotal component of the 2WAY system, responsible for managing network connections, ensuring data integrity, and facilitating secure communication between servers. Within the 2WAY infrastructure, the Network Manager oversees the establishment, maintenance, and security of network interactions, ensuring that data flows seamlessly and securely between interconnected servers. This role is critical for maintaining the overall health and efficiency of the network, enabling the system to function as a cohesive and robust platform.

At its core, the Network Manager handles the complexities of networking, leveraging advanced protocols and network topologies to enable efficient and secure data routing. The servers within the 2WAY system only connect to other servers that are part of the Server Graph, a network map that defines the relationships and connections between servers. For a server to establish a connection with another server, it must possess the public key of one of the users associated with that server and the server's Onion address. The Onion address, a key part of the Tor network, is used to maintain anonymity and secure communications. When this address is a child attribute of a public key, or "pubkey," parent attribute, the server will attempt to establish a connection.

The process of establishing a connection between servers involves several critical steps managed by the Network Manager. Initially, servers connect to each other’s Bastion Engine. The Bastion Engine is responsible for handling client-puzzle challenges, which serve as a defense mechanism against Denial of Service (DoS) attacks. These puzzles are designed to be computationally intensive, requiring effort to solve and thereby limiting the ability of an attacker to flood the server with requests. The difficulty of these puzzles adjusts dynamically based on the number of incoming connections, increasing during periods of high traffic to provide enhanced protection. Once a server solves the client-puzzle challenge, the connection is considered authenticated and secure, allowing for subsequent messages to be communicated via the Incoming Engine and Outgoing Engine.

The Network Manager also includes the State Engine, which is crucial for maintaining and synchronizing the state across the network. This component ensures that all servers within the network have a consistent view of the data, managing state changes, resolving conflicts, and ensuring data consistency. Through the State Engine, the Network Manager facilitates querying and sharing state information between servers, enabling efficient data synchronization and consistency across the network.

Another critical component of the Network Manager is the Network Engine, which manages network services and ensures efficient communication between servers. This engine handles the creation, starting, stopping, and revoking of Onion services, which are essential for maintaining secure and anonymous communication channels within the network. The Network Engine also manages socket connections, ensuring that data is transmitted and received reliably and securely.

The Bastion Engine plays a defensive role within the Network Manager, fortifying the network against attacks and ensuring robust security. It processes incoming messages, detecting and responding to potential threats, and works in tandem with the DoS Guard Manager to monitor and mitigate DoS attacks. The DoS Guard Manager employs client puzzles to prevent DoS attacks, generating and verifying puzzles to ensure their effectiveness. When a server detects a DoS attack on its Bastion Engine, it will revoke the compromised Onion service, create a new one, and communicate this change to other connected servers via the Outgoing Engine.

The Incoming Engine and Outgoing Engine handle the flow of inbound and outbound network traffic, respectively. The Incoming Engine processes incoming messages, filtering, queuing, and routing them to their appropriate destinations. The Outgoing Engine manages the sending of messages, ensuring that they are properly formatted, encrypted, and delivered. Both engines play a vital role in maintaining the reliability and security of communications within the 2WAY system.

Additionally, the Network Startup Engine is responsible for initializing network connections and services. It handles the creation and solving of client puzzles during the startup process, ensuring that servers establish secure connections with their first-degree connections. This engine is critical for bootstrapping the network and ensuring that all necessary services are up and running efficiently.

Overall, the Network Manager is integral to the 2WAY system, providing a robust framework for managing network connections, securing data transmissions, and ensuring the seamless operation of the network. By leveraging best practices in networking, encryption, and security, the Network Manager ensures that the 2WAY system remains resilient, efficient, and secure, capable of supporting the complex interactions and communications required in a decentralized and highly interconnected environment.

### 2.9.2 Networking
Explanation of the networking fundamentals used in the 2WAY system, including protocols, network topologies, and the mechanisms used for node discovery and data routing.

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

# 3 Practical Examples <a name="practical-examples"></a>

<br>

## 3.1 Introduction to the Practical Examples
This section provides a high-level overview of the various practical applications of the 2WAY system, highlighting its versatility and potential across different industries and use cases.

<br>

## 3.2 Installing 2WAY
Step-by-step guide to installing the 2WAY system, including prerequisites, installation steps, and troubleshooting tips to ensure a smooth setup process.

<br>

## 3.3 Managing Contacts
Explanation of how to manage contacts within the 2WAY system, including adding, editing, and removing contacts, as well as organizing them into groups. This includes user management of the user's own personas.

<br>

## 3.4 Synchronizing Data
Guide on how to synchronize data across multiple devices and platforms using the 2WAY system, ensuring data consistency and availability, with the help of P2P networking, the 2WAY Graph, and e2e encrypted communications with the help of collected "pubkey" and "onion" Attributes stored in the Graph, ACLs, and the Network Manager.

<br>

## 3.5 Key Revocation, Re-Issuance, and Propagation
Detailed scenarios and examples of when and why key revocation and re-issuance are necessary, and how the 2WAY system handles these processes securely through a multi-sig mechanism where 2 out of 3 alarm keys can signal to their contacts that one or more keys belonging to a user have been compromised.

<br>

## 3.6 Zero Knowledge Proofs
Explanation of zero-knowledge proofs, their significance in the 2WAY system, and practical examples of their implementation for privacy-preserving verification.

<br>

## 3.7 Private Messaging
How to implement private messaging within the 2WAY system, focusing on encryption, message integrity, and privacy.

<br>

## 3.8 Social Feed
Technical implementation and user interface design for creating a social feed within the 2WAY system, including real-time updates and interaction features.

<br>

## 3.9 Solving for Sybil Attacks
Case studies and specific methods used by the 2WAY system to address and mitigate Sybil attacks, ensuring network integrity and trust, with the help of visualizing the User Graph.

<br>

## 3.10 Wallet Plugin
Implementation of a wallet plugin within the 2WAY system, covering both cryptocurrency wallets and digital identity wallets, with a focus on security and ease of use.

<br>

## 3.11 Verifying Binaries
Automated binary verification processes using the 2WAY system to ensure software integrity and authenticity before installation or execution.

<br>

## 3.12 Market Plugin
Creating a decentralized market plugin within the 2WAY system, enabling secure and trustless transactions between users.

<br>

## 3.13 P2P Advertising
Implementation of peer-to-peer advertising within the 2WAY system, focusing on decentralized ad networks and user-to-user advertising.

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

# 4 Conclusion <a name="conclusion"></a>








<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>











[ ] Improve "2.5 Object Manager"
[ ] Messages appended --> updated in database and can be logged to Log Manager
[ ] Latest message --> Update database records to newest state and log messages to Log Manager
[ ] Add "Modify Objects" between "2.5.2 Creating Objects" and "2.5.3 Hiding Objects"
[ ] "signing_key" --> "signer": "user_id"
[ ] ""5,9,12,13,14"," to array such as "[5,9,12]"
[ ] Capitalize all objects (attributes, parents, edges, ratings)
[ ] Add user_id description
[ ] Change user_public_key to user_id where needed
[ ] Querying Objects --> Vote = empty to query both up and down-voted objects
[ ] Improve all the JSON documents where needed
[ ] Breakdown all the JSON documents like under "2.5.5 Filtering Objects"
[ ] 2.5.4 "latest" not described, 1 = latest object version and 0 = all object versions
[ ] Add "latest" to "2.5.5 Filtering Objects"
[ ] Change database schema to prevent plugin name collision in table name




[X] Rename Message Manager to Object Manager
[X] ",." --> "",.
[X] Remove mentions of ACL Manager
[X] Remove mentions of State Manager
[X] PoC, proof-of-concept
[X] Change "2WAY" to "twoway" where needed
[X] Change "Contacts" to "connections" where needed
[X] public key, pubkey, "pubkey"
[X] Add Library plugin paragraph to "1.4 Pre-Installed Plugins"
[X] Improve "2.3 2WAY Objects"
[X] Remove mentions of Denial of Service (DoS) Guard Manager
[X] node --> server, where relevant
[X] Improve "1. Frontend"
[X] Improve "2.1 Introduction to the Backend"
[X] Improve "2.2 Graph"
[X] Log Manager --> JSON document should contain "created", "modified", or "deleted"
[X] Plugin cryptographic key-pairs, objects, and permissions
[X] Improve "2.4.1 Introduction to the Database Schema"
[X] Add frontend schema to "2.4 Database Schema"

