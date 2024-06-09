



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
  2.4 [Database Schema](#24-database-schema)<br>
  2.5 [Object Manager](#25-object-manager)<br>
  2.6 [Graph Manager](#26-graph-manager)<br>
  2.7 [Storage Manager](#27-storage-manager)<br>
  2.8 [Key Manager](#28-key-manager)<br>
  2.9 [Network Manager](#29-network-manager)<br>
  2.10 [Log Manager](#210-log-manager)<br>

3. [Practical Examples](#practical-examples)

<br><br><br>

# Introduction <a name="introduction"></a>

In today's digital landscape, centralized identity and reputation systems are everywhere, forming the foundation of online interactions. These systems, similar to algorithms used by popular platforms, assess the credibility or reliability of entities like users, products, services, and other entities based on various factors. While these systems offer convenience, they also introduce inherent vulnerabilities and limitations that impact both users and third-party service providers. From privacy concerns to regulatory compliance challenges, centralized systems pose significant risks and costs to all stakeholders.

For users, centralized identity and reputation systems often require the disclosure of sensitive personal information to third-party intermediaries. This reliance raises privacy concerns and exposes users to data breaches and unauthorized access. Additionally, users may face restrictions on their digital freedoms, as centralized systems are subject to censorship and control by a single authority.

For third-party service providers, managing and securing vast amounts of user data within centralized systems incurs significant costs related to data storage, security measures, and regulatory compliance. As these systems grow, they become more susceptible to attacks, posing reputational risks and potential legal liabilities.

Decentralizing identity and reputation management can mitigate these risks and costs for both users and service providers. By distributing user data across a decentralized network, the need for central intermediaries is reduced, minimizing the risk of data breaches and unauthorized access. Decentralized systems offer greater transparency and security, as user data is cryptographically secured and managed with the help of decentralized graphs.

For service providers, decentralizing applications can streamline operations and reduce overhead costs associated with data management and security. Leveraging decentralized technologies like distributed graphs and peer-to-peer (P2P) networks enhances data privacy, reduces regulatory burdens, and mitigates the risk of cyber attacks.

<br>

Enter 2WAY, a pioneering proof-of-concept that reimagines electronic identity and reputation management in a fully peer-to-peer (P2P) environment. At its core, 2WAY empowers users to take control of their digital identities, manage linked data securely, and establish direct communication channels without relying on intermediaries. Through the seamless integration of digital signatures, a graph structure, and a decentralized P2P network, 2WAY offers users the ability to curate their digital personas, filter information for relevance, and engage securely with trusted parties, all within familiar interfaces.

The foundation of 2WAY lies in its distributed identity, reputation, and access management server, which leverages cryptographic proof to verify message authenticity and establish secure communication channels between servers. Through a decentralized network of trusted servers, users can exchange data with confidence, knowing that their identities and interactions are protected by robust cryptographic mechanisms.

Furthermore, 2WAY is designed with extensibility in mind, allowing developers to build plugins that serve as applications within the 2WAY system. These plugins can leverage the platform's core functionalities, enabling a diverse range of applications and services to be built on top of the 2WAY infrastructure.

Drawing inspiration from the principles of privacy by design, 2WAY ensures that personally identifiable information is processed minimally, with private messages and data shared only with consent and encrypted for the intended recipient. Public messages can be broadcast on a best-effort basis, though this remains outside the scope of this proof-of-concept.

Designed to be lightweight, 2WAY can run both the frontend (client) and backend (server) on a desktop computer, making it accessible and practical for a wide range of users. Although the main goal of the 2WAY proof-of-concept is to demonstrate the 2WAY protocol, the platform leverages the Flask framework for both the frontend and backend, merging them into a single application. This integrated approach simplifies development and deployment. Once the proof-of-concept has proven effective, the backend could be implemented as a daemon or service in a low-level language, and the frontend could be developed using any language or framework.

2WAY ensures scalability through a distributed architecture, leveraging decentralized technologies like distributed graphs and P2P networks to distribute workload across multiple servers. This enables horizontal scaling by adding more servers, accommodating growing user demands without performance degradation. Efficient data storage and retrieval mechanisms further enhance scalability while maintaining responsiveness. Additionally, 2WAY prioritizes user-friendly interfaces, designed with intuitive principles to simplify digital identity and data management. Clear interfaces guide users through tasks, reducing the need for technical expertise and fostering greater adoption and engagement.

<br>

This document navigates through the intricate layers of the 2WAY system, beginning with an exploration of its frontend infrastructure and extending to its backend architecture.

Within the Frontend section, we explain the Flask framework, the backbone of 2WAY's frontend, and examine the concept of plugins, from pre-installed options to the development of custom plugins.

Transitioning to the Backend section, we uncover the foundational elements of the 2WAY Graph, alongside the management of core 2WAY Objects such as Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). Additionally, we describe the Database Schema and dive deep into the functionalities of essential backend components, including the Object Manager, Graph Manager, Storage Manager, Network Manager, and more.

Finally, within the Practical Examples section, we illustrate the real-world applications of 2WAY across various scenarios, demonstrating its versatility and efficacy in managing contacts, messaging, social interactions, addressing security challenges like Sybil attacks, navigating markets, verifying binaries, and handling key management tasks.

In summary, 2WAY offers a groundbreaking approach to electronic identity and reputation management by decentralizing these processes and empowering users with greater control and security. By eliminating the need for centralized third parties, 2WAY reduces the risks and costs associated with managing and securing user data, benefiting both users and service providers. This proof-of-concept demonstrates the potential of running both frontend and backend on a single desktop computer, leveraging the Flask framework for a seamless, integrated experience. With its extensible plugin architecture, 2WAY provides a versatile platform for developers to create a wide range of applications, fostering a resilient and user-centric digital ecosystem. This document will guide you through the detailed workings of 2WAY, highlighting its potential to revolutionize the way we manage digital identities and interactions in a secure, decentralized manner.

<br><br>

# 1. Frontend <a name="frontend"></a>

<br>

## 1.1 Introduction to the Frontend <a name="11-introduction-to-the-frontend"></a>

The frontend of the 2WAY system serves as the user-facing interface, providing a gateway to interact with the platform's features and functionalities. It is designed to offer an intuitive and responsive experience, enabling users to seamlessly manage their identities, reputations, and access controls within the decentralized network.

This section describes the infrastructure that powers the frontend, beginning with the Flask framework. Flask is chosen for its lightweight and flexible nature, making it an ideal foundation for building dynamic web applications. It supports the development of robust, scalable frontends that can cater to a wide range of user requirements.

We also explore the concept of plugins, which significantly extend the frontend's capabilities. Plugins enhance the frontend's versatility and modularity, allowing for a tailored user experience. Pre-installed plugins come bundled with the system, providing essential functionalities out of the box. Additionally, the architecture supports the development of custom plugins, enabling users and developers to create and integrate new features according to specific needs and preferences.

By leveraging the flexibility of Flask and the extensibility provided by plugins, the frontend of the 2WAY system can be customized and expanded to meet the diverse demands of its user base, ensuring a personalized and efficient interaction with the platform.

<br>

## 1.2 Flask <a name="12-flask"></a>

Flask serves as the cornerstone of the 2WAY system's architecture, offering a versatile and lightweight framework for web application development. Traditionally known for backend development, Flask is uniquely employed in 2WAY to power both the server-side components and the client-side user interface. This approach merges the frontend and backend into a cohesive unit, simplifying development and deployment processes while promoting code reusability and maintainability.

Using Flask for both frontend and backend operations streamlines communication between the user interface and the server infrastructure, facilitating seamless data exchange and interaction. Flask's intuitive syntax and extensive ecosystem of extensions empower developers to create responsive, dynamic, and feature-rich web applications. Key extensions such as Flask-RESTful for building APIs, Flask-SQLAlchemy for database integration, and Flask-WTF for form handling contribute to the system's robustness and flexibility.

By integrating Flask into the 2WAY system, developers can build a user-centric frontend experience that seamlessly interacts with backend services. This ensures a cohesive and intuitive interface for users, enhancing their ability to engage with the platform's features and functionalities efficiently. Flask's simplicity, flexibility, and scalability make it an ideal choice for the unified architecture of the 2WAY system, providing a strong foundation for its comprehensive identity, reputation, and access management framework.

<br>

## 1.3 Plugins <a name="13-plugins"></a>

Within the 2WAY system, Flask plugins on the frontend facilitate seamless communication with the Object Manager on the backend. These plugins act as intermediaries, enabling efficient data retrieval and display within the frontend application.

Flask plugins encapsulate various functionalities designed to enhance the user experience and streamline interactions with backend systems. Integrated into the frontend application built on the Flask framework, they provide a modular and extensible architecture for managing data and user interactions.

At their core, Flask plugins leverage the capabilities of the Flask ecosystem to establish connections with the backend's Object Manager, the central hub for handling all data operations. Through these connections, the frontend can send requests and receive responses, enabling real-time updates and synchronization of data between the user interface and the server infrastructure.

The Object Manager processes incoming requests from the frontend, executing necessary operations to retrieve, manipulate, or query data stored within the Server Graph, and returning the results to the frontend. This includes tasks such as creating and retrieving objects, updating graph structures, querying for relevant information, and managing access control and permissions.

By leveraging Flask plugins, the frontend application can seamlessly interact with the Object Manager and access the full range of functionalities offered by backend services. This enables users to perform actions such as creating new objects, updating existing data, querying information, and collaborating with other users, all while maintaining a responsive and intuitive user experience.

Overall, Flask plugins play a crucial role in bridging the gap between the frontend and backend components of the 2WAY system. They enable efficient communication and data exchange between the user interface and the server infrastructure. Through their integration into the Flask framework, these plugins empower developers to build rich, interactive applications that leverage the full capabilities of the 2WAY platform, ensuring a seamless and intuitive user experience.

<br>

## 1.4 Pre-Installed Plugins <a name="14-pre-installed-plugins"></a>

The 2WAY system's frontend comes with several pre-installed plugins designed to enhance user experience and provide essential functionality. These plugins integrate seamlessly with backend services, facilitating various interactions within the platform.

The Contacts plugin acts as a contact list or address book, allowing users to manage their network connections within the 2WAY system. Utilizing the 2WAY graph, the Contacts plugin provides an intuitive interface for organizing and accessing contacts, enabling seamless communication and collaboration.

The Messages plugin builds on the Contacts plugin to offer peer-to-peer messaging capabilities. By leveraging contact information and network connections from the 2WAY graph, the Messages plugin enables real-time message exchanges, fostering communication within the platform.

The Library plugin offers a comprehensive interface for browsing, searching, and filtering all objects from various plugins. Using degrees of separation within the 2WAY graph, the Library plugin makes data management and retrieval intuitive and efficient, allowing users to easily locate and interact with information.

The Social plugin enriches the user experience by providing a social feed that aggregates the latest messages from contacts. This feed gives users a centralized view of their interactions and conversations, keeping them updated on relevant discussions and activities within their network.

These pre-installed plugins provide essential functionality for managing contacts, exchanging messages, and staying connected within the 2WAY platform. By leveraging the 2WAY graph and integrating with backend services, these plugins enhance the overall user experience and contribute to the platform's effectiveness as a communication and collaboration tool.

<br>

## 1.5 Custom Plugins <a name="15-custom-plugins"></a>

Beyond the default functionality provided by the pre-installed plugins, the 2WAY system supports custom plugins, enabling developers to extend the platform's capabilities and tailor the user experience to specific needs. Custom plugins allow developers to introduce new features, integrate third-party services, and customize the frontend interface according to user requirements.

Built using the Flask framework, custom plugins can leverage Flask extensions and libraries to streamline development. This flexibility allows developers to create a wide range of plugins, from specialized communication tools to advanced data visualization and analytics.

One common use case for custom plugins is integrating external services or APIs. For instance, developers might create plugins that connect with social media platforms, enabling users to share content, import contacts, or interact with external communities seamlessly.

Custom plugins can also be tailored to specific industries, providing solutions for niche markets or specialized user groups. Examples include plugins for project management, customer relationship management (CRM), or e-commerce, allowing organizations to use the 2WAY platform for their business needs.

Additionally, custom plugins can enhance user engagement by introducing gamification elements, personalized experiences, or advanced collaboration features. This flexibility allows developers to experiment with new ideas, gather user feedback, and continuously improve the user experience.

Overall, custom plugins significantly enhance the functionality and versatility of the 2WAY platform. By supporting custom plugin development, the 2WAY system empowers developers to innovate and create solutions that meet unique user requirements, driving engagement and satisfaction.

<br><br>

# 2. Backend <a name="backend"></a>

<br>

## 2.1 Introduction to the Backend <a name="21-introduction-to-the-backend"></a>

The backend of the 2WAY system is the cornerstone of its decentralized identity, reputation, and access management framework. It is designed to handle the complex processes required to maintain secure, efficient, and reliable operations within the 2WAY ecosystem. This backend infrastructure supports the creation, management, and verification of cryptographic identities and facilitates secure data exchanges between trusted servers in a peer-to-peer (P2P) network.

At the core of the backend lies the 2WAY Graph, a comprehensive data structure integrating both the User Graphs and the Server Graph. The User Graph represents individual user interactions, while the Server Graph aggregates all User Graphs on a particular server, encapsulating a subset of the network’s decentralized data.

The backend manages various types of 2WAY Objects essential to the system's operation, including Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). Attributes are key-value pairs with a "type" and a "value". Ratings store reputation scores. Parents can have one or more Attributes as children, and Edges establish the relationships between a Parent and its children. ACLs define and manage access permissions within the system. Each object can be up or down-voted indefinitely, influencing its visibility in the graph.

Several crucial components support the functionality and security of the 2WAY backend. The Database Schema ensures efficient data organization and structure. The Object Manager handles message reception from the frontend, backend, or any connected application, ensuring secure and reliable communication. The Graph Manager oversees the Graph in RAM, maintaining the integrity and updates of the active data structure, while the overall 2WAY Graph is stored to disk. The Key Manager handles the signing and verification of messages, as well as the encryption and decryption of communications.

Additional components enhance the backend's robustness and reliability. The Storage Manager handles physical data storage. The Network Manager manages network connections between servers, ensuring efficient data exchange. It tracks synchronized data with other servers and manages data pending synchronization on the next connection. It also protects the system from Denial of Service (DoS) attacks using proof-of-work-based client-puzzle challenges with dynamic difficulty levels to maintain network performance and availability. The Log Manager records system activities for auditing and troubleshooting. The Installation and Startup Managers facilitate the deployment and initialization of the 2WAY system.

In essence, the 2WAY backend is a sophisticated and modular system that provides the secure and decentralized foundation needed for the 2WAY platform's operations. It integrates various components and data structures to create a resilient and efficient framework for managing digital identities and associated data in a P2P network. This section explains each element in detail, offering a comprehensive understanding of the backend architecture and its critical role within the 2WAY system.

<br>

## 2.2 2WAY Graph <a name="22-2way-graph"></a>

### 2.2.1 Introduction to the 2WAY Graph

The 2WAY Graph lies at the core of the 2WAY system, serving as a dynamic and interconnected framework for representing and organizing data.

At its essence, the 2WAY Graph is a directed graph-based data model that uses nodes and edges to model relationships and interactions between various entities within the system. Nodes represent individual objects such as Attributes, Parents, Ratings, and Access Control Lists (ACLs). Edges denote the connections and associations between Parent objects and Attributes.

The 2WAY Graph is decentralized and distributed, allowing users to create, share, and collaborate on data in a flexible and scalable manner. This graph-based approach facilitates intuitive navigation, exploration, and discovery of interconnected data. Users can traverse relationships and uncover valuable insights within their social or organizational networks.

<br>

### 2.2.2 User Graph

The User Graph in the 2WAY system represents each user's unique network of nodes and edges. It contains the user's personal data, connections, and interactions, reflecting their contributions and relationships within the broader context of the Server Graph. The Server Graph is the aggregate of all User Graphs within the system. Each User Graph is unique, representing the user's specific interactions, preferences, and network connections.

A key aspect of the User Graph is that users always query data from their zeroth degree, meaning they primarily interact with and retrieve data that directly pertains to them or is within their immediate network connections. When querying the Server Graph, users explore their own graph, accessing relationships, application data, and interactions that are directly relevant to them.

From the user's perspective, data in other User Graphs that doesn't overlap with their own User Graph is essentially invisible. Users only perceive and interact with data within their own User Graph or that is directly connected to them through their network connections. Data outside of their immediate network or areas of interest is inaccessible.

This approach ensures users maintain a focused and personalized view of the data within the 2WAY system. It allows them to efficiently navigate and interact with information directly relevant to their needs and interests. By querying from their zeroth degree within the Server Graph, users can effectively manage their data, discover relevant connections, and collaborate with others within their network while maintaining privacy and control over their personal information.

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

In 2WAY, a small set of simple data structures are used to construct objects. These objects, represented as nodes and edges within the 2WAY graph, encompass all the data stored within the system. The flexibility of these objects allows the system to model a wide range of applications and data structures, with the graph structure facilitating data organization and relationships.

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

Attributes are dynamically defined, either through API communication from the frontend or directly by the backend.

When a user generates an Attribute on the frontend, it's transmitted to the backend's Object Manager API as a JSON document. For example:

```json
{
  "object": "attribute",
  "signing_key": "user_public_key",
  "app_hash": "hashed_app_identifier",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "1"
}
```

In this JSON structure:
- `object` indicates that this is an Attribute.
- `signing_key` refers to the public key of the user creating the Attribute.
- `app_hash` signifies the hashed application identifier, along with the sub-ID, to ensure uniqueness and prevent naming collisions.
- `attribute_type` and `attribute_value` define the key-value pair of the Attribute.
- `vote` is a boolean value indicating the object's relevance (`1` for relevant, `0` for irrelevant).

The `vote` value aids in managing the object's lifecycle; an object with a vote of `0` in its latest version is disregarded in future queries unless explicitly requested.

Once received, the Object Manager commences the creation process of various object types within the system by authorized users. The newly formed Attribute is connected to the user's public key through an implicit edge. This connection is inherent since the public key is stored as an Attribute, and the new Attribute contains the signer's public key and signature.

Optionally, each individual change can be logged to the Log Manager before updating the unsigned object to the Graph on Disk. Logged changes can be signed before storage by passing through the Key Manager, ensuring data integrity and authenticity.

The Object Manager also facilitates Attribute querying, enabling users to filter results based on the degree of separation and additional contextual criteria.

When queried, the newly created Attribute object is returned:

```json
{
  "id": 1,
  "version": 1,
  "signing_key": "Alice's public key",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "document hash"
}
```

In this JSON structure:
- `id` represents the unique identifier assigned to the Attribute.
- `version` denotes the version of the Attribute.
- `signing_key` indicates the public key of the user generating the Attribute.
- `app_hash` signifies the hashed application identifier, along with the sub-ID, ensuring uniqueness and preventing naming collisions.
- `attribute_type` and `attribute_value` define the key-value pair of the Attribute.
- `vote` is a boolean value indicating the relevance of the Attribute (`1` for relevant, `0` for irrelevant).
- `timestamp` shows the time when the Attribute was created.
- `hash` represents the hash of the document.

When the change is queried from the Log Manager, the log presents the following response:

```json
{
  "id": 56,
  "signing_key": "Alice's public key",
  "attribute_id": "1",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "document hash",
  "signature": "cryptographic signature"
}
```

In this JSON structure:
- `id` stands for the unique identifier assigned to the log entry.
- `signing_key` indicates the public key of the user generating the log entry.
- `attribute_id` refers to the unique identifier of the Attribute associated with this log entry.
- `attribute_type` and `attribute_value` define the key-value pair of the Attribute.
- `vote` is a boolean value indicating the relevance of the Attribute (`1` for relevant, `0` for irrelevant).
- `timestamp` shows the time when the log entry was created.
- `hash` represents the hash of the document.
- `signature` signifies the cryptographic signature of the log entry.

<br>

### 2.3.3 Parent

A Parent in the 2WAY system consists of a single parent Attribute connected to one or more child Attributes and/or other Parents. This hierarchical structure allows for the organization and management of complex data relationships. For example:

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
      "child_value": "Enterprise LLC"
    }
  ]
}
```

In this example:
- `parent_type` is "pubkey", and `parent_value` is "Alice's public key".
- `children` array contains various child Attributes, each with its type and value, establishing specific information linked to the parent.

Typically, users in the 2WAY system are identified by their public key (the "pubkey" Attribute). A user's parent Attribute might thus appear as `{"type": "pubkey", "value": "Alice's public key"}`. Child Attributes like `{"type": "username", "value": "Alice"}` or `{"type": "email", "value": "alice@gmail.com"}` are then associated with this parent, establishing the necessary relationships to organize and retrieve user data effectively.

To create objects other than users, define the required parent Attribute accordingly. For example, to store blog articles, you might use `{"type": "Post", "value": "Blog Post Title"}`. For a marketplace, start with `{"type": "category", "value": "Books"}`, followed by relevant child Attributes. A blog post could have children like `{"type": "title", "value": "Post Title"}`, `{"type": "author", "value": "Author Name"}`, and `{"type": "content", "value": "Post Content"}`. Similarly, a book might include children like `{"type": "author", "value": "Author Name"}`, `{"type": "ISBN", "value": "ISBN Code"}`, and `{"type": "content", "value": "Book Content"}`.

When creating a parent object, the following JSON structure might be used:

```json
{
  "id": 1,
  "version": 1,
  "signing_key": "Alice's public key",
  "parent_id": "4",
  "parent_version": "1",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document"
}
```

In this JSON structure:
- `id` and `version` identify the object and its version.
- `signing_key` is the public key of the user creating the object.
- `parent_id` and `parent_version` reference the parent Attribute object.
- `vote` indicates the relevance of the object (`1` for relevant, `0` for irrelevant).
- `timestamp` records the time of creation.
- `hash` provides a unique identifier for the document.

As with the Attribute object, changes can be signed and sent to the Log Manager.

<br>

### 2.3.4 Edge

In the 2WAY system, an Edge is established whenever a new attribute or parent-child relationship is created. These Edges connect objects within the graph, ensuring the structural integrity and facilitating efficient data organization and retrieval.

When a new attribute or parent-child relationship is formed, an Edge is established between the newly created object and the Attribute containing the public key of the signer. Similarly, Edges are created between parent and child Attributes to denote their relationship within the graph.

While Edges between parents and children are stored separately to maintain clarity and organization, Edges between newly created attributes and public keys are established within the attributes themselves. This is because the linked public key is already present within the Attribute. The same principle applies to reputation ratings and access control lists (ACLs), which also contain associated public keys within themselves.

Here's an example JSON document illustrating the establishment of a parent-child Edge:

```json
{
  "id": 1,
  "version": 1,
  "signing_key": "Alice's public key",
  "parent_id": "4",
  "parent_version": "2",
  "child_ids": "5,9,12,13,14",
  "child_versions": "1,1,2,1,1",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document"
}
```

In this JSON structure:
- `id` and `version` identify the object and its version.
- `signing_key` is the public key of the user creating the object.
- `parent_id` and `parent_version` reference the parent object.
- `child_ids` and `child_versions` specify the IDs and versions of child objects.
- `vote` indicates the relevance of the object (`1` for relevant, `0` for irrelevant).
- `timestamp` records the time of creation.
- `hash` provides a unique identifier for the document.

As with the Attribute object, changes can be signed and sent to the Log Manager.

<br>

### 2.3.5 Rating

In 2WAY, user or entity reputation can be effectively managed through structured JSON documents known as ratings. These ratings encapsulate various reputation metrics, including comments, scores, and scales, to provide a comprehensive assessment of user or entity reputation within the system.

The rating data structure includes the following fields:

- **comment**: Allows users to provide comments or feedback about the rated entity.
- **score**: Indicates the assigned score based on a rating scale predefined by the plugin.
- **scale**: Specifies the type or category of the rating scale used for assigning scores, predefined by the plugin.

This flexible data structure accommodates diverse rating types and scales, ensuring adaptability to different rating contexts. Once structured, the rating document points at an Attribute or Parent within the system.

Here's an example JSON document illustrating the establishment of a rating:

```json
{
  "id": 1,
  "version": 1,
  "signing_key": "Alice's public key",
  "attribute_id": "1",
  "attribute_version": "1",
  "parent_id": "",
  "parent_version": "",
  "comment": "Wow, this is really great!",
  "score": "13",
  "scale": "out-of-10-but-up-to-13",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document"
}
```

In this JSON structure:
- `id` and `version` identify the rating object and its version.
- `signing_key` represents the public key of the user providing the rating.
- `attribute_id` and `attribute_version` specify the rated attribute.
- `comment`, `score`, and `scale` capture the details of the rating.
- `vote` denotes the relevance of the rating.
- `timestamp` records the time of creation.
- `hash` provides a unique identifier for the document.

As with the Attribute object, changes can be signed and sent to the Log Manager.

<br>

### 2.3.6 Access Control List (ACL)

In 2WAY, the Access Control List (ACL) plays a pivotal role in managing user permissions within the system. This structured data entity acts as a bridge between a user's "pubkey" Attribute and the specific attributes or parents they are authorized to access.

The ACL document follows a structured format, containing entries that define access permissions granted to each user. These entries typically include:

- **pubkey_id**: The public key of the user for whom permissions are being defined.
- **permissions**: An array specifying the attributes or parents that the user is permitted to read.

Each entry in the ACL document establishes a direct link between a user's public key and the attributes or parents they have access to.

During state synchronization between users, the ACL plays a critical role in determining synchronized data for each connection in the User Graph. By referencing the ACL associated with each user, the system efficiently identifies permitted data for synchronization based on established permissions. This mechanism ensures that users only receive data for attributes or parents they have explicit read permissions for, thereby upholding data privacy and security.

Here's an example JSON document illustrating the establishment of an ACL:

```json
{
  "id": 1,
  "version": 1,
  "signing_key": "Alice's public key",
  "pubkey_id": "1",
  "permissions_attribute": "3,5",
  "permissions_parent": "7,8",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document"
}
```

In this JSON structure:
- `id` and `version` identify the ACL object and its version.
- `signing_key` represents Alice's public key.
- `pubkey_id` links the ACL to a specific user.
- `permissions_attribute` and `permissions_parent` specify the attributes or parents the user can access.
- `vote` denotes the relevance of the ACL.
- `timestamp` records the time of creation.
- `hash` provides a unique identifier for the document.

As with the Attribute object, changes can be signed and sent to the Log Manager here as well.

<br>

## 2.4 Database Schema <a name="24-database-schema"></a>

### 2.4.1 Introduction to the Database Schema

The database schema for the 2WAY system mirrors the structure and relationships of the discussed objects, employing SQLite3 as the underlying database technology. SQLite3 was chosen for its versatility and compatibility with various systems, aligning perfectly with the lightweight and accessible nature of 2WAY. While future iterations may explore alternative databases, starting with SQLite3 showcases the protocol's scalability and efficiency, especially as it transitions to more robust and performant environments.

By segmenting data into distinct tables and establishing relationships via foreign keys, the schema ensures data integrity and facilitates seamless querying and retrieval operations within the SQLite3 database. Moreover, integration of versioning fields allows for effective tracking of changes over time and management of data revisions. This schema framework supports the creation, storage, and retrieval of diverse objects within the 2WAY system, providing a robust infrastructure for managing user data, reputation metrics, access controls, and other pertinent information in a structured manner.

In the 2WAY ecosystem, each plugin is responsible for creating its own set of tables within the backend database, adhering to the schema delineated in section 2.4.2, "Database Schema Design". This approach not only prevents plugins from interfering with each other but also enables them to access and utilize data from other plugins, fostering synergy and collaboration.

To accomplish this, each plugin is assigned a unique "app_id" and can optionally have one or more "app_sub_id" identifiers. These identifiers are utilized to name the tables within the database, ensuring the distinctiveness and recognizability of each plugin's tables. For instance, the default Contacts plugin in 2WAY might be associated with the app_id "twoway" and the app_sub_id "connections", resulting in table names like "twoway_connections_attributes", "twoway_connections_parents", and so forth.

The schema design for plugins is meticulously crafted to promote interoperability and seamless integration between different components within the system. By adhering to consistent naming conventions and structural guidelines, plugins can easily interact with one another and share data as required. This adherence to a uniform schema design facilitates code reuse and simplifies plugin development, enabling developers to focus on implementing unique functionalities without grappling with low-level database management intricacies.

Furthermore, the utilization of app_id and app_sub_id identifiers allows plugins to coexist harmoniously within the same database environment while safeguarding the isolation and encapsulation of data. This approach empowers developers to mix and match plugins according to their specific needs, crafting bespoke configurations tailored to their distinct use cases.

In essence, replicating the database schema per plugin underscores the principles of modularity, flexibility, and interoperability within the 2WAY framework. It empowers developers to extend and enrich the platform with new features while upholding consistency and compatibility across diverse plugins.

<br>

### 2.4.2 Database Schema Design

Here are the core tables in the schema:

1. **Attributes Table**:
   - **id** INT: Unique identifier for the attribute.
   - **version** INT: Version number for the attribute.
   - **type** TEXT: Type of the attribute.
   - **signing_key** TEXT: Key used to sign the attribute.
   - **attribute_type** TEXT: Key of the attribute.
   - **attribute_value** TEXT: Value of the attribute.
   - **vote** INT: Vote count for the attribute.
   - **timestamp** INT: Timestamp of the attribute creation or modification.
   - **hash** TEXT: Hash of the attribute.
   - **signature** TEXT: Signature of the attribute.
   - **PRIMARY KEY (id, version)**: Composite primary key ensuring uniqueness per version.

2. **Parents Table**:
   - **id** INT: Unique identifier for the parent.
   - **version** INT: Version number for the parent.
   - **type** TEXT: Type of the parent.
   - **signing_key** TEXT: Key used to sign the parent.
   - **parent_id** INT: Identifier of the parent.
   - **parent_version** INT: Version number of the parent.
   - **vote** INT: Vote count for the parent.
   - **timestamp** INT: Timestamp of the parent creation or modification.
   - **hash** TEXT: Hash of the parent.
   - **signature** TEXT: Signature of the parent.
   - **PRIMARY KEY (id, version)**: Composite primary key ensuring uniqueness per version.
   - **FOREIGN KEY (parent_id, parent_version) REFERENCES twoway_connections_attributes(id, version)**: Ensures referential integrity with the Attributes table.

3. **Edges Table**:
   - **id** INT: Unique identifier for the edge.
   - **version** INT: Version number for the edge.
   - **type** TEXT: Type of the edge.
   - **signing_key** TEXT: Key used to sign the edge.
   - **parent_id** INT: Identifier of the parent node.
   - **parent_version** INT: Version number of the parent node.
   - **child_ids** TEXT: Comma-separated list of child node IDs.
   - **child_versions** TEXT: Comma-separated list of child node versions.
   - **vote** INT: Vote count for the edge.
   - **timestamp** INT: Timestamp of the edge creation or modification.
   - **hash** TEXT: Hash of the edge.
   - **signature** TEXT: Signature of the edge.
   - **PRIMARY KEY (id, version)**: Composite primary key ensuring uniqueness per version.
   - **FOREIGN KEY (parent_id, parent_version) REFERENCES twoway_connections_parents(id, version)**: Ensures referential integrity with the Parents table.

4. **Rating Table**:
   - **id** INT: Unique identifier for the rating entry.
   - **version** INT: Version number for the rating entry.
   - **type** TEXT: Type of the rating entry.
   - **signing_key** TEXT: Key used to sign the rating entry.
   - **attribute_id** INT: Identifier of the related attribute.
   - **attribute_version** INT: Version number of the related attribute.
   - **parent_id** INT: Identifier of the related parent.
   - **parent_version** INT: Version number of the related parent.
   - **comment** TEXT: Comment associated with the rating entry.
   - **score** TEXT: Score given in the rating entry.
   - **scale** TEXT: Scale of the score.
   - **timestamp** INT: Timestamp of the rating entry creation or modification.
   - **hash** TEXT: Hash of the rating entry.
   - **signature** TEXT: Signature of the rating entry.
   - **PRIMARY KEY (id, version)**: Composite primary key ensuring uniqueness per version.
   - **FOREIGN KEY (attribute_id, attribute_version) REFERENCES twoway_connections_attributes(id, version)**: Ensures referential integrity with the Attributes table.
   - **FOREIGN KEY (parent_id, parent_version) REFERENCES twoway_connections_parents(id, version)**: Ensures referential integrity with the Parents table.

5. **ACL Table**:
   - **id** INT: Unique identifier for the ACL entry.
   - **version** INT: Version number for the ACL entry.
   - **signing_key** TEXT: Key used to sign the ACL entry.
   - **pubkey_id** INT: Identifier of the public key.
   - **permissions** TEXT: Permissions associated with the ACL entry.
   - **timestamp** INT: Timestamp of the ACL entry creation or modification.
   - **hash** TEXT: Hash of the ACL entry.
   - **signature** TEXT: Signature of the ACL entry.
   - **PRIMARY KEY (id, version)**: Composite primary key ensuring uniqueness per version.
   - **FOREIGN KEY (pubkey_id) REFERENCES twoway_connections_attributes(id, version)**: Ensures referential integrity with the Attributes table.

<br>

## 2.5 Object Manager <a name="25-object-manager"></a>

### 2.5.1 Introduction to the Object Manager

In the 2WAY system, the Object Manager serves as the central hub for creating and querying all the core objects, including Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). These objects are managed and accessed through APIs exposed by the backend's Object Manager, ensuring a streamlined and efficient handling of data interactions.

When users create objects such as Attributes or Parents, they interact with the frontend interface, which communicates with the backend's Object Manager via API calls. These API calls contain the necessary data to create the desired object, such as Attribute key-value pairs or parent-child relationships. Upon receiving these requests, the Object Manager processes the data, passes it to the Key Manager for signing, and then to the Storage Manager for the corresponding database operations to create the requested objects within the system. Additionally, it informs the Graph Manager of any relevant changes, ensuring that the system remains up-to-date and consistent.

Similarly, querying objects within the 2WAY system is initiated through the frontend interface, which sends API calls to the backend's Object Manager. These API calls specify the parameters for the desired query, including the degree of separation from the user's zeroth degree (their public key) and the type of object being queried. The Object Manager retrieves the relevant nodes from the Graph Manager (which manages the Graph in RAM), then uses the resulting record IDs to query data from the database with the help of the Storage Manager. The queried data is then returned to the frontend for user interaction.

By centralizing object creation and querying functionality within the Object Manager and exposing it through APIs, the 2WAY system ensures consistency, security, and scalability in managing various types of objects and data. This approach abstracts the complexities of database interactions and provides a unified interface for interacting with the system's objects, enhancing usability and maintainability.

It is important to note that for this proof-of-concept, messages are not signed on the frontend. In future versions, messages could potentially be signed on the frontend or with hardware keys, providing an additional layer of security and flexibility.

<br>

### 2.5.2 Creating Objects

To create objects within the 2WAY system, users interact with the frontend interface, which communicates with the backend's Object Manager through API calls. These API calls contain JSON documents specifying the details of the objects to be created. Below are examples of JSON documents for creating different types of objects based on the database schema:

1. **Creating Attributes:**
```json
{
  "object": "attribute",
  "app_id": "twoway, connections",
  "signing_key": "user_id",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "1"
}
```

2. **Creating Parents:**
```json
{
  "object": "parent",
  "app_id": "twoway, connections",
  "signing_key": "user_id",
  "parent_id": 123,
  "parent_version": 1,
  "vote": "1"
}
```
3. **Creating Edges:**
```json
{
  "object": "edge",
  "app_id": "twoway, connections",
  "signing_key": "user_id",
  "parent_id": 123,
  "parent_version": 1,
  "child_ids": [456, 789],
  "child_versions": [1, 2],
  "vote": 1
}
```

4. **Creating Ratings:**
```json
{
  "object": "rating",
  "app_id": "twoway, connections",
  "signing_key": "user_id",
  "attribute_id": 0,
  "attribute_version": 0,
  "parent_id": 456,
  "parent_version": 1,
  "comment": "Great experience!",
  "score": "5",
  "scale": "5",
  "vote": 1
}
```

5. **Creating ACLs:**
```json
{
  "object": "acl",
  "app_id": "twoway, connections",
  "signing_key": "user_id",
  "pubkey_id": 123,
  "access_to_id": [456, 789],
  "access_to_parent": 0,
  "permissions": 1
}
```

Upon receiving these JSON documents from clients or the backend/system itself, the Object Manager first forwards them to the Key Manager. The Key Manager timestamps them, generates a hash for each JSON document, and then signs the messages.

```json
{
  "object": "attribute",
  "app_id": "twoway, connections",
  "signing_key": "user_id",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "1",
  "timestamp": 1617000000,
  "hash": "generated_hash",
  "signature": "generated_signature"
}
```

Once signed, the messages are handed over to the Storage Manager, which appends them to the database. Additionally, any necessary updates to the Graph in RAM are handled by passing the message to the Graph Manager.

When the Object Manager receives a message from the Network Manager (i.e., from another server), it directly appends the message by forwarding it to the Storage Manager. Furthermore, any required updates to the Graph in RAM are managed by passing the message to the Graph Manager.

<br>

### 2.5.3 Hiding Objects

Objects within the 2WAY system are never deleted from the database. Instead, they can only be down-voted, which by default signifies their irrelevance or disapproval by the user. This approach ensures data integrity and historical traceability, as every interaction with an object is preserved. This is crucial because different users may have varying perspectives on the relevance or validity of an object, and preserving all objects allows the system to accommodate these differing opinions.

An examples of a JSON document for down-voting an Attribute, to be processed by the Object Manager:

```json
{
  "object": "attribute",
  "app_id": "twoway, connections",
  "signing_key": "user_id",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "0"
}
```

Upon receiving this JSON document, the Object Manager follows the standard procedure: it passes the document to the Key Manager for signing, timestamping, and hashing.

```json
{
  "object": "attribute",
  "app_id": "twoway, connections",
  "signing_key": "user_id",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "0",
  "timestamp": 1618000000,
  "hash": "generated_hash",
  "signature": "generated_signature"
}
```

The signed document is then appended to the database by the Storage Manager. The Graph Manager is updated as necessary to reflect the down-vote in the Graph in RAM.

By preserving all objects and utilizing a down-vote mechanism, the 2WAY system allows users to filter and prioritize data according to their own preferences and judgments. This ensures a more personalized and user-centric experience, where each individual can curate their digital environment without permanently removing information that might be relevant to others.

While the current proof-of-concept does not support automatic removal of objects, it is conceivable that future implementations could incorporate mechanisms for cleaning up the database. For example, duplicate objects, objects with an older version, or those beyond a certain age threshold could be automatically pruned to maintain database efficiency and manageability. However, such features are outside the scope of this proof-of-concept and would require careful consideration of criteria and processes to ensure consistency and data integrity.

<br>

### 2.5.4 Querying Objects

To query objects within the 2WAY system, users initiate requests through the frontend interface, which communicates with the backend's Object Manager via API calls. These API calls contain JSON documents specifying the parameters for the desired query, including the type of object and the degree of separation from the user's zeroth degree (their public key). By default, the system queries and returns the latest version of only the up-voted objects, ensuring that users receive the most relevant data.

Here is an example of a JSON document for querying up-voted objects:

```json
{
  "object": "attribute",
  "app_id": "twoway, connections",
  "signing_key": "user_public_key",
  "degree": 2,
  "vote": 1,
  "latest": 1
}
```

Upon receiving this JSON document, the Object Manager retrieves the relevant nodes from the Graph Manager and queries data from the database based on the specified parameters. The queried data is then returned to the frontend for user interaction.

If a user wishes to query down-voted objects, they can specify the vote parameter accordingly. Here's an example of a JSON document for querying down-voted objects:

```json
{
  "object": "attribute",
  "app_id": "twoway, connections",
  "signing_key": "user_public_key",
  "degree": 2,
  "vote": 0,
  "latest": 0
}
```

By setting the "vote" parameter to "0", the system will retrieve the latest versions of down-voted objects, allowing users to access data that they or others might have found less relevant or disagreed with. This functionality provides a comprehensive view of the data landscape within the 2WAY system, accommodating different perspectives and preferences.

Upon receiving these JSON documents, the Object Manager processes the request by first interacting with the Graph Manager to identify the relevant nodes within the Graph in RAM. It then uses the resulting record IDs to query data from the database with the help of the Storage Manager. The system ensures that the queried objects match the specified parameters, including object type, degree of separation, and vote status, before returning the data to the frontend.

This approach to querying objects ensures that users can access the most relevant and up-to-date information by default, while still providing the flexibility to explore a broader range of data as needed. By supporting queries for both up-voted and down-voted objects, the 2WAY system offers a balanced and user-centric method for data retrieval, enhancing overall user experience and data discoverability.

<br>

### 2.5.5 Filtering Objects

In addition to querying objects, users can filter objects within the 2WAY system based on specific criteria. This filtering functionality allows users to narrow down their search results and focus on the most relevant information. Filtering can be applied to Attributes, Ratings, and other object types within the system, with the ability to specify voting status (1 for up-voted, 0 for down-voted). 

Below is an example of a JSON document for filtering objects based on specific criteria:

```json
{
  "object": "attribute",
  "app_id": "twoway, connections",
  "signing_key": "user_public_key",
  "criteria": {
    "attribute_type": "email",
    "attribute_value": "example@email.com",
    "degree": 3,
    "vote": 1
  }
}
```

Upon receiving this JSON document, the Object Manager applies the specified filtering criteria to the queried data, returning only the objects that match the given criteria. This enables users to efficiently retrieve and analyze data based on their specific requirements.

### Filtering by Ratings

To filter objects based on Ratings, users can specify criteria for Ratings in their query. Below is an example of a JSON document for filtering objects that have positive ratings:

```json
{
  "object": "rating",
  "app_id": "twoway, connections",
  "signing_key": "user_public_key",
  "criteria": {
    "min_score": "1",
    "scale": "out-of-10",
    "degree": 1,
    "vote": 1
  }
}
```

### Comprehensive Filtering

Here is a more extensive and UX-friendly search query example that demonstrates filtering based on various criteria, including Attributes, Ratings, and relationships:

**Goal:** Retrieve all "phone numbers" (Attributes with type=”phone_number” and any value) of "restaurants" (Parent object), apart from "The French Cock" (attribute; type="restaurant" and value="The French Cock"), with "positive ratings" (Rating object) from "Friends" (Parent object) and "Family" (Parent object), but not "people with bad taste in food" (Parent object) in zeroth degree, and signed by anyone within 2 degrees of separation or less.

**JSON Document for Filtering:**

```json
{
  "object": "attribute",
  "app_id": "twoway, connections",
  "signing_key": "user_public_key",
  "degree": 2,
  "criteria": {
    "attribute_type": "phone_number",
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
    "exclude_parents": ["people with bad taste in food"],
    "degree": 0
  }
}
```

**Breakdown of Filtering Criteria:**

- **object**: Specifies the type of object to filter, which is "attribute" in this case.
- **app_id**: Specifies the application context, here it's "twoway, connections".
- **signing_key**: The public key of the user initiating the query.
- **degree**: Limits the query to objects signed by anyone within 2 degrees of separation.
- **criteria**: Contains the filtering parameters:
  - **attribute_type**: "phone_number", indicating we want attributes of this type.
  - **vote**: 1, indicating we only want up-voted objects.
  - **parent**: Specifies the type of parent object we are interested in ("restaurant"), and excludes a specific value ("The French Cock").
  - **ratings**: Specifies criteria for ratings:
    - **min_score**: "1.75", indicating we want objects with a minimum score of 1.75.
    - **scale**: "out-of-5-stars", specifying the scale of the ratings.
    - **vote**: 1, indicating only up-voted ratings.
    - **signed_by**: Specifies that we want ratings from "Friends" and "Family".
  - **exclude_parents**: Excludes objects associated with specific parents ("people with bad taste in food").
  - **degree**: 0, limiting "exclude_parents" objects to those signed by the user, in the zeroth degree.

Upon receiving this JSON document, the Object Manager processes the request by first interacting with the Graph Manager to identify relevant nodes within the Graph in RAM. It then uses the resulting record IDs to query data from the database with the help of the Storage Manager, applying all specified filtering criteria before returning the data to the frontend.

This approach to filtering objects ensures that users can refine their queries to retrieve the most relevant and useful information, tailored to their specific needs and preferences. By supporting complex filtering criteria, the 2WAY system offers a robust and flexible method for data retrieval, enhancing overall user experience and data discoverability.

<br><br>

## 2.6 Graph Manager <a name="26-graph-manager"></a>

### 2.6.1 Introduction to the Graph Manager

The Graph Manager in the 2WAY system manages the Graph in RAM and synchronizes it with the persistent disk-based Server Graph. It oversees storage, retrieval, and manipulation of graph data, ensuring efficient access and maintenance.

The Graph Manager handles the storage and retrieval of the in-memory graph to and from disk. During system initialization, shutdown, or significant updates, it transfers graph data between RAM and disk storage. This synchronization keeps the Graph in RAM aligned with the Server Graph for seamless data access and manipulation.

Additionally, the Graph Manager processes changes from the Object Manager, which handles object creation and querying by users. When changes occur, such as adding or removing nodes and edges, the Graph Manager updates the corresponding nodes and edges (not to be confused with the Edge object) in the Graph in RAM.

For example, when a user creates a new connection, the Graph Manager adds the corresponding node and edge with the table record ID that stores the Attribute of their public key to the Graph in RAM. Conversely, if a connection ("pubkey" Attribute) is down-voted, the Graph Manager removes the relevant node and edge from the Graph in RAM.

The Graph Manager also facilitates query operations by providing methods to retrieve nodes by degree of separation from the user's zeroth degree within the Server Graph. Users query the Object Manager, which then calls the Graph Manager to obtain table record IDs of relevant nodes within their User Graph, enabling efficient exploration and analysis.

The Graph Manager for this proof-of-concept focuses on storing record IDs of public key Attributes with app_id="twoway" and app_sub_id="connections" in the table "twoway_connections_attributes". For example, if Alice's first interaction is signing her own public key, storing it as an Attribute with the record ID "1" in the table, a node with the value "1" is added to the Graph in RAM. If Alice adds Bob's public key as an attribute with a record ID of "34", a node with the value "34" is added to the Graph in RAM, and an edge is established between nodes "1" and "34". When a "pubkey" Attribute is down-voted, it is removed from the Graph in RAM along with the edge between the two nodes.

Future versions of 2WAY may allow adding and removing other Attributes or Parents to and from the Graph in RAM, but this is outside the scope of the proof-of-concept.

By managing synchronization between the Graph in RAM and the Server Graph, as well as handling changes and query requests, the Graph Manager ensures the integrity, accessibility, and responsiveness of the graph data within the 2WAY system.

<br>

### 2.6.2 Storage and Retrieval

The Graph Manager in the 2WAY system is responsible for the storage and retrieval of the Graph in RAM, ensuring its synchronization with the persistent Server Graph. This process involves constructing the Graph in RAM from the Server Graph, storing it to disk, and retrieving it when necessary.

#### Construction of the Graph in RAM

The Graph in RAM is initially constructed from the Server Graph, utilizing the NetworkX library to create and manage graph data structures in Python. During initialization, the Graph Manager populates the in-memory graph with relevant nodes and edges based on the data stored in the Server Graph. These nodes can represent various objects such as Attributes, Parents, and connections between users.

#### Storage to Disk

Once constructed, the Graph in RAM can be stored to disk for persistence using the "nx.write_gpickle" function provided by NetworkX. This serialization process saves the graph data structure in a binary format, allowing it to be efficiently written to disk for long-term storage. Storing the graph to disk ensures that the latest state of the Graph in RAM is preserved even when the system is restarted or shut down.

#### Retrieval from Disk

When the system is initialized or when the Graph in RAM needs to be reconstructed, the Graph Manager retrieves the serialized graph data from disk using the "nx.read_gpickle" function. This deserialization process loads the graph structure back into memory, restoring it to its previous state. The retrieved graph can then be verified against the Server Graph to ensure consistency and accuracy.

#### Verification and Reconstruction

At any point, the Graph in RAM can be verified against the Server Graph to confirm that they are synchronized. This verification process involves comparing the nodes and edges in the in-memory graph with the corresponding data in the Server Graph. Discrepancies or inconsistencies can be identified and resolved to maintain data integrity.

Additionally, if the Graph in RAM becomes corrupted or needs to be reconstructed from scratch, the Graph Manager can rebuild it using data from the Server Graph. This reconstruction process involves fetching the relevant data from the Server Graph and populating the in-memory graph accordingly.

In summary, the Graph Manager handles the storage and retrieval of the Graph in RAM, ensuring its alignment with the persistent Server Graph. By utilizing serialization and deserialization techniques provided by the NetworkX library, the Graph Manager enables efficient data management and synchronization within the 2WAY system.

<br>

### 2.6.3 Changes to Graph in RAM

The 2WAY system's Graph Manager is designed to manage dynamic changes in the Graph in RAM, primarily focusing on the record IDs of public key Attributes with specific identifiers. This section details how nodes and edges are added or removed based on interactions within the 2WAY system, using JSON document examples to illustrate these changes.

#### Adding Nodes and Edges

When a user, such as Alice, first signs her own public key, an Attribute is created with a unique record ID stored in the `twoway_connections_attributes` table. This is represented by the following JSON document:

```json
{
  "id": 1,
  "version": 1,
  "type": "pubkey",
  "signing_key": "Alice's public key",
  "attribute_key": "pubkey",
  "attribute_value": "Alice's public key",
  "vote": 1,
  "timestamp": 1648062000,
  "hash": "hash of the document",
  "signature": "cryptographic signature"
}
```

Upon receiving this JSON document, the Graph Manager adds a node with the value "1" to the Graph in RAM, representing Alice's public key.

Next, if Alice adds Bob's public key as an attribute, another Attribute is created, resulting in a new record ID:

```json
{
  "id": 34,
  "version": 1,
  "type": "pubkey",
  "signing_key": "Alice's public key",
  "attribute_key": "pubkey",
  "attribute_value": "Bob's public key",
  "vote": 1,
  "timestamp": 1648062010,
  "hash": "hash of the document",
  "signature": "cryptographic signature"
}
```

The Graph Manager then adds a node with the value "34" to the Graph in RAM and creates a directed edge between nodes "1" (Alice) and "34" (Bob), establishing a connection between the two users, from Alice, to Bob.

#### Removing Nodes and Edges

If a "pubkey" Attribute or connection is down-voted, it signifies that the connection is no longer relevant or trusted. This down-vote action is represented by the following JSON document:

```json
{
  "id": 45,
  "version": 2,
  "type": "pubkey",
  "signing_key": "Alice's public key",
  "attribute_key": "pubkey",
  "attribute_value": "Bob's public key",
  "vote": 0,
  "timestamp": 1648062020,
  "hash": "hash of the document",
  "signature": "cryptographic signature"
}
```

Upon processing this JSON document, the Graph Manager queries the old Attributes for Bob's "pubkey", and verifies the previously oldest version of the Attribute is up-voted and exist in the Graph in RAM, to then remove the node "34" and the edge between nodes "1" and "34" from the Graph in RAM. This ensures that the in-memory graph only reflects active and trusted connections.

#### Future Extensions

While the current proof-of-concept focuses on managing connections represented by public key Attributes, future versions of 2WAY could potentially allow for the addition and removal of other types of Attributes or Parents from the Graph in RAM. However, these enhancements are beyond the scope of this proof-of-concept and would require additional considerations for implementation.

In summary, the Graph Manager in the 2WAY system dynamically adjusts the Graph in RAM to reflect changes in connections, ensuring data accuracy and efficient query operations. The use of JSON documents facilitates the management of nodes and edges, highlighting the flexibility and scalability of the system.

<br>

### 2.6.4 Querying Nodes from RAM

In the 2WAY system, querying nodes from the Graph in RAM is an essential operation for efficiently retrieving user connections and relationships. The Graph Manager plays a crucial role in this process by interacting with the Object Manager to handle user queries and return the relevant data. This section explains how nodes are queried from the Graph in RAM using JSON document examples to illustrate the process.

#### Query Process Overview

When a user initiates a query, it is done through the frontend interface, which sends a request to the Object Manager. The Object Manager then communicates with the Graph Manager to retrieve the relevant nodes from the Graph in RAM based on the specified parameters.

The query request includes details such as the object type, degree of separation, and any specific filtering criteria. Below is an example of a JSON document representing a query request:

```json
{
  "object": "attribute",
  "app_id": "twoway, connections",
  "signing_key": "user_public_key",
  "degree": 2,
  "criteria": {
    "attribute_type": "pubkey",
    "vote": 1
  }
}
```

In this example, the user is querying for public key attributes within two degrees of separation from their own public key, with only up-voted attributes considered.

#### Querying Nodes

Upon receiving the query request from the Object Manager, the Graph Manager processes the request by retrieving the relevant nodes from the Graph in RAM. The degree of separation specifies how far the query should traverse from the user's node. For example, if the degree is set to 2, the Graph Manager retrieves nodes that are directly connected to the user's node (first-degree) as well as nodes connected to those nodes (second-degree).

The filtering criteria specified in the query request further refine the results. In the provided example, only nodes representing public key attributes that have been up-voted are retrieved.

The Graph Manager returns a set of nodes, categorized by their degree of separation, to the Object Manager. This set includes record IDs of the nodes along with their respective degrees.

```json
{
  "query_result": {
    "degrees": [
      {
        "degree": 1,
        "nodes": [2, 3, 4]
      },
      {
        "degree": 2,
        "nodes": [5, 6, 7, 8]
      },
      {
        "degree": 3,
        "nodes": [9, 10]
      }
    ]
  }
}
```

In this example, the nodes are grouped by their degree of separation:

- Nodes `2, 3, and 4` are within the first degree of separation.
- Nodes `5, 6, 7, and 8` are within the second degree of separation.
- Nodes `9 and 10` are within the third degree of separation.

This structure allows the Object Manager to efficiently process and query the Storage Manager for the detailed information of the nodes, categorized by their degrees of separation.

#### Example Query Results

The Object Manager then uses this set of node record IDs to query the Storage Manager, which retrieves the full details of each node from the database. The Object Manager formats this data and sends it back to the frontend interface for user interaction. An example of the JSON document representing the query results might look like this:

```json
{
  "results": [
    {
      "id": 2,
      "version": 1,
      "type": "pubkey",
      "signing_key": "Alice's public key",
      "attribute_key": "pubkey",
      "attribute_value": "Bob's public key",
      "vote": 1,
      "timestamp": 1648062000,
      "hash": "hash of the document",
      "signature": "cryptographic signature",
      "degree": 1
    },
    {
      "id": 5,
      "version": 1,
      "type": "pubkey",
      "signing_key": "Bob's public key",
      "attribute_key": "pubkey",
      "attribute_value": "Carol's public key",
      "vote": 1,
      "timestamp": 1648062010,
      "hash": "hash of the document",
      "signature": "cryptographic signature",
      "degree": 2
    }
  ]
}
```

In this example, the results include nodes for Bob's and Carol's public keys, which are within two degrees of separation from the user's public key and have been up-voted. Each result also includes the degree of separation for clarity.

#### Future Enhancements

While this proof-of-concept focuses on querying nodes based on public key attributes and their degrees of separation, future versions of 2WAY could incorporate more advanced querying capabilities. This might include filtering based on additional attributes or incorporating more complex relationship criteria. However, such enhancements are beyond the scope of this proof-of-concept.

In conclusion, querying nodes from the Graph in RAM in the 2WAY system is a streamlined process that leverages the Object Manager to handle user queries efficiently. By specifying query parameters and filtering criteria through JSON documents, the system ensures that users receive accurate and relevant data from the in-memory graph, enhancing the overall user experience.

<br><br>

## 2.7 Storage Manager <a name="27-storage-manager"></a>

### 2.7.1 Introduction to the Storage Manager

### 2.7.2 Storage Engine

#### 2.7.2.1 Create Database and Tables

#### 2.7.2.2 Storage and Retrieval

<br>

## 2.8 Key Manager <a name="28-key-manager"></a>

### 2.8.1 Introduction to the Key Manager

### 2.8.2 Key Engine

#### 2.8.2.1 Generate Keys

#### 2.8.2.2 Verify Signatures

#### 2.8.2.3 Sign Messages

#### 2.8.2.4 Encrypt Messages

#### 2.8.2.5 Decrypt Messages

### 2.8.3 Revocation and Re-Issuance

<br>

## 2.9 State Manager

### 2.9.1 Introduction to the State Manager

### 2.9.2 State Engine

#### 2.9.2.1 Querying States

#### 2.9.2.2 Sharing States

<br>

## 2.10 Network Manager <a name="29-network-manager"></a>

### 2.10.1 Introduction to the Network Manager

### 2.10.2 Networking

Tor integration, etc

### 2.10.3 Establishing Connections

### 2.10.4 Data Synchronization

### 2.10.5 Network Engine

#### 2.10.5.1 Introduction to the Network Engine

#### 2.10.5.2 Creating Onion Services

#### 2.10.5.3 Starting Onion Services

#### 2.10.5.4 Stopping Onion Services

#### 2.10.5.5 Revoking Onion Services

#### 2.10.5.6 Closing Sockets

#### 2.10.5.7 Receiving Messages

#### 2.10.5.8 Sending Messages

### 2.10.6 Client Puzzle Engine

#### 2.10.6.1 Introduction to the Client Puzzle Engine

#### 2.10.6.2 Creating and Solving Client Puzzles

#### 2.10.6.3 Querying and Verifying Client Puzzle Challenges and Solutions

### 2.10.7 Bastion Engine

#### 2.10.7.1 Introduction to the Bastion Engine

#### 2.10.7.2 Receiving Messages

### 2.10.8 Incoming Engine

#### 2.10.8.1 Introduction to the Incoming Engine

#### 2.10.8.2 Receiving Messages

### 2.10.9 Outgoing Engine

#### 2.10.9.1 Introduction to the Outgoing Engine

#### 2.10.9.2 Sending Messages

### 2.10.10 Network Startup Engine

#### 2.10.10.1 Introduction to the Network Startup Engine

#### 2.10.10.2 Creating and Solving Client Puzzles

#### 2.10.10.3 Starting Onion Services

#### 2.10.10.4 Connecting with First Degree Connections

<br>

## 2.11 DoS Guard Manager

### 2.11.1 Introduction to the DoS Guard Manager

### 2.11.2 DoS Guard Engine

#### 2.11.2.1 Receiving Bastion Alarms

<br>

## 2.12 Log Manager <a name="210-log-manager"></a>

### 2.12.1 Introduction to the Log Manager

### 2.12.2 Log Engine

#### 2.12.2.1 Logging Failed Operations

#### 2.12.2.2 Logging Failed Bastion Messages

#### 2.12.2.3 Logging Failed Incoming Messages

<br><br>

# 3 Practical Examples <a name="practical-examples"></a>

<br>

## 3.1 Introduction to the Practical Examples

<br>

## 3.2 Managing Contacts

<br>

## 3.3 Messaging

<br>

## 3.4 Social

<br>

## 3.5 Solving for Sybil Attacks

<br>

## 3.6 Markets

<br>

## 3.7 Verifying Binaries

<br>

## 3.8 Key Revocation, Re-Issuance, and Propagation

<br>

## 

<br>




<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>










[ ] Messages appended --> updated in database and can be logged to Log Manager
[ ] Latest message --> Update database records to newest state and log messages to Log Manager

[ ] Add "Modify Objects" between "2.5.2 Creating Objects" and "2.5.3 Hiding Objects"

[ ] Improve "2.5 Object Manager"
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
