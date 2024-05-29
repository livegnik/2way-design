



# 2WAY: Protocol Architecture and Flask Implementation Blueprint

<br><br>

# Table of Contents
[Introduction](#introduction)
1. [Frontend](#frontend)
   1. [1.1 Introduction to the Frontend](#11-introduction-to-the-frontend)
   2. [1.2 Flask](#12-flask)

2. [Backend](#backend)

3. [Practical Examples](#practical-examples)

<br><br>

# Introduction <a name="introduction"></a>

In today's digital landscape, centralized identity and reputation systems are ubiquitous, serving as the foundation for online interactions. While these systems offer convenience, they also introduce inherent vulnerabilities and limitations that impact both users and third-party service providers. From privacy concerns to regulatory compliance challenges, centralized systems pose significant risks and costs to all stakeholders.

For users, centralized identity and reputation systems often require the disclosure of sensitive personal information to third-party intermediaries. This reliance raises privacy concerns and exposes users to data breaches and unauthorized access. Additionally, users may face restrictions on their digital freedoms, as centralized systems are subject to censorship and control by a single authority.

For third-party service providers, managing and securing vast amounts of user data within centralized systems incurs significant costs related to data storage, security measures, and regulatory compliance. As these systems grow, they become more susceptible to attacks, posing reputational risks and potential legal liabilities.

Decentralizing identity and reputation management can mitigate these risks and costs for both users and service providers. By distributing user data across a decentralized network, the need for central intermediaries is reduced, minimizing the risk of data breaches and unauthorized access. Decentralized systems offer greater transparency and security, as user data is cryptographically secured and managed with the help of decentralized graphs.

For service providers, decentralizing applications can streamline operations and reduce overhead costs associated with data management and security. Leveraging decentralized technologies like distributed graphs and peer-to-peer (P2P) networks enhances data privacy, reduces regulatory burdens, and mitigates the risk of cyber attacks.

Enter 2WAY, a proposal for a proof-of-concept (PoC) offering a purely P2P version of electronic identity and reputation. At its core, 2WAY empowers users to issue their own cryptographic identities, control linked data, and establish secure communication channels without trusted intermediaries. Through digital signatures, a graph, and a P2P network, 2WAY enables users to curate their digital personas, filter information for relevancy, and interact directly with trusted parties securely, all through interfaces that already feel familiar to them.

Designed to be lightweight, 2WAY can run both the frontend (client) and backend (server) on a desktop computer, making it accessible and practical for a wide range of users. Although the main goal of the 2WAY PoC is to demonstrate the 2WAY protocol, the platform leverages the Flask framework for both the frontend and backend, merging them into a single application. This integrated approach simplifies development and deployment. Once the PoC has proven effective, the backend could be implemented as a daemon or service in a low-level language, and the frontend could be developed using any language or framework.

The foundation of 2WAY lies in its distributed identity, reputation, and access management server, which leverages cryptographic proof to verify message authenticity and establish secure communication channels between servers. Through a decentralized network of trusted nodes, users can exchange data with confidence, knowing that their identities and interactions are protected by robust cryptographic mechanisms.

Furthermore, 2WAY is designed with extensibility in mind, allowing developers to build plugins that serve as applications within the 2WAY system. These plugins can leverage the platform's core functionalities, enabling a diverse range of applications and services to be built on top of the 2WAY infrastructure.

Drawing inspiration from the principles of privacy by design, 2WAY ensures that personally identifiable information is processed minimally, with private messages and data shared only with consent and encrypted for the intended recipient. Public messages can be broadcast on a best-effort basis, though this remains outside the scope of this PoC.

This document navigates through the intricate layers of the 2WAY system, beginning with an exploration of its frontend infrastructure and extending to its backend architecture.

Within the Frontend section, we explain the Flask framework, the backbone of 2WAY's frontend, and examine the concept of plugins, from pre-installed options to the development of custom plugins.

Transitioning to the Backend section, we uncover the foundational elements of the 2WAY Graph, alongside the management of core 2WAY Objects such as Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). Additionally, we describe the Database Schema and dive deep into the functionalities of essential backend components, including the Object Manager, Graph Manager, Storage Manager, and more.

Finally, within the Practical Examples section, we illustrate the real-world applications of 2WAY across various scenarios, demonstrating its versatility and efficacy in managing contacts, messaging, social interactions, addressing security challenges like Sybil attacks, navigating markets, verifying binaries, and handling key management tasks.

In summary, 2WAY offers a groundbreaking approach to electronic identity and reputation management by decentralizing these processes and empowering users with greater control and security. By eliminating the need for centralized third parties, 2WAY reduces the risks and costs associated with managing and securing user data, benefiting both users and service providers. This PoC demonstrates the potential of running both frontend and backend on a single desktop computer, leveraging the Flask framework for a seamless, integrated experience. With its extensible plugin architecture, 2WAY provides a versatile platform for developers to create a wide range of applications, fostering a resilient and user-centric digital ecosystem. This document will guide you through the detailed workings of 2WAY, highlighting its potential to revolutionize the way we manage digital identities and interactions in a secure, decentralized manner.

<br><br>

# 1. Frontend <a name="frontend"></a>

<br>

## 1.1 Introduction to the Frontend <a name="11-introduction-to-the-frontend"></a>

The frontend of the 2WAY system serves as the user-facing interface, providing a gateway to interact with the platform's features and functionalities.

In this section, we explore the infrastructure that powers the frontend, starting with an exploration of the Flask framework. Flask serves as the foundation for building the frontend, offering a lightweight and flexible framework for web application development.

We also examine the concept of plugins, which extend the functionality of the frontend, enhancing its versatility and modularity.

From pre-installed plugins that come bundled with the system to the possibility of developing custom plugins, we uncover the diverse ways in which the frontend architecture of 2WAY can be tailored to meet specific user needs and preferences.

<br>

## 1.2 Flask <a name="12-flask"></a>

Flask serves as the cornerstone of both the frontend and backend architecture in the 2WAY system, offering a versatile and lightweight framework for web application development. Traditionally known for its usage in backend development, Flask is uniquely employed in 2WAY to power not only the server-side components but also the client-side user interface. This approach merges the frontend and backend into a cohesive unit, simplifying development and deployment processes while promoting code reusability and maintainability.

Leveraging Flask for both frontend and backend operations streamlines communication between the user interface and the underlying server infrastructure, facilitating seamless data exchange and interaction. With its intuitive syntax and extensive ecosystem of extensions, Flask empowers developers to create responsive, dynamic, and feature-rich web applications that embody the principles of simplicity, flexibility, and scalability.

Through its integration into the 2WAY system, Flask provides a robust foundation for building a user-centric frontend experience that seamlessly integrates with the backend services, ensuring a cohesive and intuitive user interface for interacting with the platform's features and functionalities.

<br>

## 1.3 Plugins

Within the 2WAY system, Flask plugins are utilized on the frontend to facilitate communication with the Object Manager on the backend. These plugins serve as intermediary components that enable seamless interaction between the user interface and the backend services, allowing for efficient retrieval and display of data within the frontend application.

The Flask plugins encapsulate various functionalities and features designed to enhance the user experience and streamline interactions with the backend systems. These plugins are integrated into the frontend application built on the Flask framework, providing a modular and extensible architecture for managing data and user interactions.

At their core, Flask plugins leverage the Flask ecosystem's capabilities to establish connections with the backend's Object Manager, which serves as the central hub for handling all data operations within the system. Through these connections, the frontend can send requests and receive responses from the backend, enabling real-time updates and synchronization of data between the user interface and the underlying server infrastructure.

The Object Manager on the backend is responsible for processing incoming requests from the frontend, executing the necessary operations to retrieve, manipulate, or query data stored within the Server Graph, and returning the results to the frontend for display. This includes tasks such as retrieving user attributes, updating graph structures, querying for relevant information, and managing access control and permissions.

By leveraging Flask plugins, the frontend application can seamlessly interact with the Object Manager and access the full range of functionalities offered by the backend services. This enables users to perform various actions within the application, such as creating new objects, updating existing data, querying for information, and collaborating with other users, all while maintaining a responsive and intuitive user experience.

Overall, Flask plugins play a crucial role in bridging the gap between the frontend and backend components of the 2WAY system, enabling efficient communication and data exchange between the user interface and the underlying server infrastructure. Through their integration into the Flask framework, these plugins empower developers to build rich, interactive applications that leverage the full capabilities of the 2WAY platform while providing a seamless and intuitive user experience.

<br>

## 1.4 Pre-Installed Plugins

Within the 2WAY system, the frontend comes equipped with several out-of-the-box plugins designed to enhance user experience and provide essential functionality. These plugins serve as integral components of the frontend application, offering seamless integration with the backend services and facilitating various interactions within the platform.

The first plugin, the Contacts plugin, serves as a contact list or address book, allowing users to manage their network connections and relationships within the 2WAY system. Leveraging the underlying 2WAY graph, the Contacts plugin provides users with an intuitive interface for organizing and accessing their contacts, enabling seamless communication and collaboration within their network.

Next, the Messages plugin builds upon the functionality of the Contacts plugin and the 2WAY graph to offer users peer-to-peer messaging capabilities. By leveraging the contact information stored in the Contacts plugin and the network connections represented in the 2WAY graph, the Messages plugin enables users to exchange messages with their contacts in real-time, fostering communication and collaboration within the platform.

Lastly, the Social plugin enriches the user experience by offering a social feed that aggregates the latest messages received from contacts within the user's network. This feed provides users with a centralized view of their interactions and conversations within the platform, allowing them to stay updated on relevant discussions and activities happening within their network.

Together, these out-of-the-box plugins provide users with essential functionality for managing contacts, exchanging messages, and staying connected within the 2WAY platform. By leveraging the underlying 2WAY graph and integrating seamlessly with the backend services, these plugins enhance the overall user experience and contribute to the platform's effectiveness as a communication and collaboration tool.

<br>

## 1.5 Custom Plugins

In addition to the out-of-the-box functionality provided by the default plugins, the 2WAY system offers support for custom plugins, empowering developers to extend the platform's capabilities and tailor the user experience to specific requirements. Custom plugins enable developers to introduce new features, integrate third-party services, and customize the frontend interface according to the unique needs of their users.

Custom plugins are built using the Flask framework and can leverage the extensive ecosystem of Flask extensions and libraries to streamline development and integration efforts. Developers have the flexibility to create plugins that cater to a wide range of use cases, from specialized communication tools to advanced data visualization and analytics functionalities.

One common use case for custom plugins is the integration of external services or APIs to extend the platform's functionality. For example, developers may create plugins that integrate with popular social media platforms, allowing users to share content, import contacts, or interact with external communities seamlessly.

Additionally, custom plugins can be tailored to specific industries or domains, providing targeted solutions for niche markets or specialized user groups. For instance, developers may create plugins for project management, customer relationship management (CRM), or e-commerce functionalities, enabling organizations to leverage the 2WAY platform for their specific business needs.

Furthermore, custom plugins can enhance user engagement and retention by introducing gamification elements, personalized experiences, or advanced collaboration features. Developers can leverage the flexibility of custom plugins to experiment with new ideas, gather user feedback, and iterate rapidly to refine and improve the user experience over time.

Overall, custom plugins play a crucial role in extending the functionality and versatility of the 2WAY platform, enabling developers to innovate and create tailored solutions that meet the unique requirements of their users. By providing a framework for custom plugin development, the 2WAY system empowers developers to unleash their creativity and build compelling experiences that drive user engagement and satisfaction.

<br><br>

# 2. Backend <a name="backend"></a>

<br>

## 2.1 Introduction to the Backend

The backend of the 2WAY system is the cornerstone of its decentralized identity, reputation, and access management framework. It is meticulously designed to handle the complex processes required to maintain secure, efficient, and reliable operations within the 2WAY ecosystem. This backend infrastructure supports the creation, management, and verification of cryptographic identities and facilitates secure data exchanges between trusted nodes in a peer-to-peer (P2P) network.

At the core of the backend lies the 2WAY Graph, a comprehensive data structure that integrates both the User Graphs and the Server Graph. The User Graph represents the individual user's interactions. In contrast, the Server Graph is the aggregate of all User Graphs on a particular server, thereby encapsulating a subset of the network’s decentralized data.

The backend is responsible for managing various types of 2WAY Objects, which are fundamental to the system's operation. These objects include Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). Attributes are key-value pairs consisting of a "type" and a "value." Ratings are specific objects used to store reputation scores. Parents can have one or more Attributes as children, and the relationships between a Parent and its children are established through Edges. ACLs are used to define and manage access permissions within the system. Each object can be up or down-voted, indefinitely, by means of a newer message, influencing its visible presence in the graph.

Several crucial components support the functionality and security of the 2WAY backend. The Database Schema ensures data is organized and structured efficiently. The Object Manager handles the reception of messages from the frontend, backend, or any connected application or device with access to the backend’s APIs, ensuring secure and reliable communication. The Graph Manager oversees the Graph in RAM only, maintaining the integrity and updates of the active data structure, while the overall 2WAY Graph encompasses the entire Server Graph, and is stored to disk.

The Key Manager is vital for handling the signing and verification of messages, as well as the encryption and decryption of communications. The ACL Manager oversees permissions and access rights, ensuring secure and authorized data access. The State Manager tracks the data that has been synchronized with other servers and manages data pending synchronization on the next connection.

Additional components enhance the backend's robustness and reliability. The Storage Manager handles the physical storage of data, while the Network Manager manages the network connections between nodes, ensuring efficient data exchange. The Denial of Service (DoS) Guard Manager protects the system from malicious attacks, maintaining network performance and availability. The Log Manager records system activities for auditing and troubleshooting, and the Installation and Startup Managers facilitate the deployment and initialization of the 2WAY system.

In essence, the 2WAY backend is a sophisticated and modular system that provides the secure and decentralized foundation needed for the 2WAY platform's operations. It integrates various components and data structures to create a resilient and efficient framework for managing digital identities and associated data in a P2P network. This section explains each element in detail, offering a comprehensive understanding of the backend architecture and its critical role within the 2WAY system.

<br>

## 2.2 2WAY Graph

### 2.2.1 Introduction to the 2WAY Graph

The 2WAY Graph lies at the core of the 2WAY system, serving as a dynamic and interconnected framework for representing and organizing data.

At its essence, the 2WAY Graph embodies a graph-based data model that leverages nodes and edges to model relationships and interactions between various entities within the system. Nodes represent individual objects such as Attributes, Parents, Ratings, and Access Control Lists (ACLs), while Edges denote the connections and associations between Parent objects and Attributes.

The 2WAY Graph is distinguished by its decentralized and distributed nature, empowering users to create, share, and collaborate on data in a flexible and scalable manner. By embracing a graph-based approach, the system facilitates intuitive navigation, exploration, and discovery of interconnected data, enabling users to traverse relationships and uncover valuable insights within their social or organizational networks.

<br>

### 2.2.2 User Graph

The User Graph in the 2WAY system represents the individualized network of nodes and edges maintained by the user. It comprises the user's personal data, connections, and interactions, encapsulating their contributions and relationships within the broader context of the Server Graph, which is the combined set of all User Graphs within the system. Each user's graph is unique and reflective of their specific interactions, preferences, and network connections within the system.

One notable aspect of the User Graph is that users always query data from their zeroth degree, from their point of view, within the Server Graph. This means that users primarily interact with and retrieve data that directly pertains to them or is within their immediate network connections. When querying the Server Graph, users traverse their own graph, exploring relationships, attributes, and interactions that are directly relevant to them.

From the user's perspective, data in other User Graphs that doesn't overlap with their own User Graph doesn't exist. In other words, users only perceive and interact with data that is within their own User Graph or is directly connected to them through their network connections. Data outside of their immediate network or areas of interest is effectively invisible or inaccessible to them within the Server Graph.

This approach ensures that users maintain a focused and personalized view of the data within the 2WAY system, allowing them to efficiently navigate and interact with information that is directly relevant to their needs and interests. By querying from their zeroth degree within the Server Graph, users can effectively manage their data, discover relevant connections, and collaborate with others within their network while maintaining privacy and control over their personal information.

<br>

### 2.2.3 Server Graph

The Server Graph in the 2WAY system represents the collective aggregation of all individual User Graphs stored on the server. Each user within the system maintains their own graph, comprising nodes and edges representing their objects and relationships among them. The Server Graph, therefore, encompasses the totality of these individual User Graphs, consolidating them into a comprehensive network of interconnected data within the system.

At its core, the Server Graph serves as a unified repository that encapsulates the entirety of the system's data landscape, encompassing Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs), contributed by users. By consolidating individual User Graphs into a centralized repository, the Server Graph facilitates seamless communication, collaboration, and data sharing among users within the system.

The Server Graph is dynamic and continually evolving, reflecting the real-time interactions and updates made by users across the platform. As users create, modify, or delete objects within their individual graphs, these changes are propagated to the Server Graph, ensuring that it remains synchronized and up-to-date with the latest data contributions from all users.

Overall, the Server Graph serves as the backbone of the 2WAY system, embodying the collective intelligence and contributions of its local user base. By consolidating individual User Graphs into a unified framework, the Server Graph enables seamless data management, discovery, and collaboration within the platform, while ensuring privacy, security, and access control based on user-defined permissions and network connections.

<br>

### 2.2.4 Graph on Disk

The Graph on Disk in the 2WAY system refers to the storage mechanism used to persist the Server Graph, comprising the aggregated data from all individual User Graphs, onto disk. This disk-based representation of the Server Graph ensures durability, accessibility, and scalability of the system's data, enabling efficient storage and retrieval of information across the entire user base.

The Server Graph, in its entirety, is stored to disk using the SQL schema as discussed in "2.4 Database Schema." This schema design organizes the data into pre-defined separate tables for each plugin, each corresponding to specific object types such as Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). By leveraging a relational database management system (RDBMS) such as SQLite3, MySQL, or PostgreSQL, the Server Graph can be efficiently persisted and managed on disk, facilitating seamless data storage and retrieval operations.

The Graph on Disk serves as the authoritative source of truth for the 2WAY system, housing the complete dataset that encompasses the collective intelligence and contributions of the users. Updates, modifications, and interactions made by users are reflected in real-time within the Server Graph on disk, ensuring that the data remains synchronized and up-to-date with the latest user activity.

Furthermore, the Graph on Disk enables efficient querying, filtering, and analysis of data within the 2WAY system, empowering users to explore connections, discover insights, and collaborate effectively within their network. By persisting the Server Graph to disk using the established SQL schema, the 2WAY system maintains data integrity, consistency, and reliability, while facilitating seamless data management and scalability for future growth and expansion.

<br>

### 2.2.5 Graph in RAM

The Graph in RAM in the 2WAY system serves as an in-memory representation of a subset of the Server Graph, stored temporarily in the system's Random Access Memory (RAM). This in-memory graph is populated and maintained using the NetworkX library, a powerful tool for analyzing and manipulating graph data structures in Python.

One of the key functionalities of the Graph in RAM is to store the table record IDs of public key Attributes from the database on disk. These pubkey attributes serve as nodes within the graph, representing individual users within the system. By storing these record IDs in memory, the system can quickly retrieve and access relevant nodes during query operations, enabling efficient traversal and exploration of the Server Graph.

The Graph in RAM is designed to facilitate rapid querying of data from the disk-based Server Graph. When a user initiates a query, the system first retrieves relevant nodes from the in-memory graph based on the degree of separation specified in the query. These nodes serve as starting points for traversing the Server Graph stored on disk, allowing the system to narrow down the scope of the query and retrieve only the necessary data.

Furthermore, the Graph in RAM could be dynamically extended with additional 2WAY objects as needed to speed up querying for certain data. For example, if a user frequently queries for attributes or parents within their immediate network, these objects could be cached in memory to expedite future query operations. However, this is outside of the scope of this proof-of-concept.

It's essential to note that maintaining a Graph in RAM comes at a relatively high cost compared to directly retrieving data from the SQL database. While in-memory operations are faster, they consume system resources and memory, potentially impacting overall system performance. Therefore, the Graph in RAM should be used conservatively and selectively, focusing on caching frequently accessed data or optimizing specific query patterns to enhance overall responsiveness and user experience within the 2WAY system.

<br>

## 2.3 2WAY Objects

### 2.3.1 Introduction to 2WAY Objects

In 2WAY, a small set of simple data structures are used to construct objects. These objects, represented as nodes and edges within the 2WAY graph, encompass all of the data stored within the system. The following objects are used to construct the system in its entirety:

~~~
1. "Attribute": Key-value pair, consisting of a "type" (the key, not to be confused with any cryptographic keys) and a "value."

2. "Parent": Parent attribute, to be connected to one or more child attributes via edges.

3. "Edge": Edge between a single parent attribute and one or more child attributes.

4. "Rating": Score with rating scale and/or comment, assigned to attribute or parent.

5. "Access Control List" (ACL): Context-specific permissions for authorized users used to synchronize data.
~~~

Using these objects, any required application can be modeled atop.

<br>

### 2.3.2 Attribute

An attribute consists of a key-value pair, in the form of a "type" and a "value," functioning as a node within the server's graph structure. For instance, attributes such as type="name" with a corresponding value="Alice", or type="pubkey" with a lengthy public key value. Any attribute can be defined dynamically, either on the frontend, communicating with the backend through APIs, or by the backend itself.

The two discussed example attributes:

```json
{
	"type": "name",
	"value": "Alice"
},

{
	"type": "pubkey",
	"value": "really long pubkey here"
}
```

Whenever a user initiates an action on the frontend that generates an attribute, it is transmitted to the backend's Object Manager API as a JSON document:

```json
{
  "object": "attribute",
  "signing_key": "user_public_key",
  "app_id": "2WAY, Contacts",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "1",
}
```

Here, the "app_id" serves as the identifier for the frontend application, "2WAY," along with one of the application's sub-IDs, "Contacts." The backend uses this information to determine where to store the data. The attribute's key-value pair is defined as "name" for type, and "Alice" as its value. The vote is boolean. The value of "1" signifies that the object is relevant, whereas the value "0" indicates that the object is not relevant (any longer). When the latest version of an object contains the value "0" for "vote," the object is disregarded during future queries, unless specifically requested. The latest version of an object is the one returned when queried for, by default.

After the Object Manager receives a new object from the frontend application, the process starts that enables the creation of various object types within the system by authorized users. The newly created attribute is linked to the user's public key through an edge. This edge does not have to be stored separately, as the public key is also stored as an attribute (node within the graph), and the newly created attribute contains the signer's public key and signature. The message is signed by being passed to the Key Manager, that runs on the backend as well. This is where all key-management takes place, in an automated fashion.

Moreover, the Object Manager facilitates attribute querying, allowing for filtering based on the degree of separation and additional contextual criteria.

Once the data is stored, the following result is returned when the newly created object is queried:

```json
{
  "id": 1,
  "version": 1,
  "signing_key": "Alice's public key",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "document hash",
  "signature": "cryptographic signature"
}
```

<br>

### 2.3.3 Parent

The parent object consists of a single parent attribute and one or more other attributes and/or parents as its children. An example:

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
      "child_type": "group",
      "child_value": "Enterprise LLC"
    }
  ]
}
```

In this example, the parent's type is "pubkey" with the value "Alice's pubkey." The attributes with the types "name," "email," and "address" are child-attributes linking to a single attribute. The links are established outside of the parent as edges. However, note that the child with child_type="group" is a parent that serves as a child-attribute, and that the user who is creating the object(s) could be a part of this group themselves, as a child-attribute of said parent.

In the 2WAY system, users are typically identified within the graph by their public key (pubkey). Consequently, a user's parent attribute might appear as name="pubkey" with a corresponding value="really long pubkey". Subsequently, the user's name or email address can be associated as child attributes, such as type="username" with a value like "Alice", or type="email" with a value like "Alice@gmail.com". This approach enables the establishment of necessary parent-child relationships to organize and retrieve data effectively.

To create objects other than users, one simply needs to define the required attribute. For example, to store blog articles, one could utilize type="Post" with a corresponding value for the post title. Similarly, for building a marketplace and adding products, starting with type="category" and value="Books" could be a first step, followed by adding relevant children attributes. For a blog post, these children could include attributes like title, author name, content, and publication date, while for a book, attributes like author, ISBN code, or content could be added.

JSON document example for establishing a parent:

```json
{
  "id": 1,
  "version": 1,
  "signing_key": "Alice's public key",
  "parent_id": "4",
  "parent_version": "1",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document",
  "signature": "cryptographic signature"
}
```

<br>

### 2.3.4 Edge

Whenever a new attribute or parent-child relationship is formed, an edge is established between the newly created object and the attribute containing the public key of the signer. Additionally, edges are created between parent and child attributes within the graph to denote their relationship. These edges serve to maintain the structural integrity of the graph and facilitate efficient data retrieval and organization.

Only edges between parents and children are stored separately, as edges between newly created attributes and public keys are established within the attributes themselves, as the linked public key is already present. The same goes for reputation ratings and access control lists (ACLs), who also contain the associated public keys within themselves.

JSON document example for establishing a parent-child edge:

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
  "hash": "hash of the document",
  "signature": "cryptographic signature"
}
```

<br>

### 2.3.5 Rating

In the context of 2WAY, the reputation of users or entities can be represented and managed through a JSON document structured to include various details related to reputation metrics, or, ratings. These metrics could encompass factors such as comments, scores, and scales, all of which contribute to the overall reputation score of users and entities within the system.

The data structure for ratings is designed to include fields such as:

~~~
"comment": A string field allowing users to provide comments or feedback about the entity being rated.

"score": A string field indicating a score assigned to the entity based on a predefined rating scale.

"scale": A string field specifying the type or category of the rating scale used for assigning scores.
~~~

By structuring the data in this manner, it becomes flexible and adaptable to different types of ratings and scales. This document can then be signed onto an attribute or parent within the system to ensure authenticity and integrity. The signature ensures that the reputation data is securely associated with the respective attribute or parent, providing a reliable record of reputation metrics within the 2WAY framework.

JSON document example for establishing a rating:


```json
{
  "id": 1,
  "version": 1,
  "signing_key": "Alice's public key",
  "attribute_id": "1",
  "attribute_version": "1",
  "parent_id": "",
  "parent_version": "",
  "comment": "wow this is really great!",
  "score": "13",
  "scale": "out-of-10-but-up-to-13",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document",
  "signature": "cryptographic signature"
}
```

<br>

### 2.3.6 Access Control List (ACL)

The Access Control List (ACL) in 2WAY serves as a crucial mechanism for managing user permissions within the system. This data structure acts as a link between a user's "pubkey" attribute and the specific attributes or parents for which they possess read permissions.

The ACL document is structured to include entries defining the access permissions granted to each user. These entries typically consist of:

~~~
"pubkey_id": The public key of the user for whom permissions are being defined.

"permissions": An array specifying the attributes or parents that the user is permitted to read.
~~~

Each entry in the ACL document establishes a direct association between a user's public key and the attributes or parents they are authorized to access.

During the synchronization of states between users, the ACL plays a crucial role in determining what data is to be synchronized for each connection in the User Graph. By referencing the ACL associated with each user, the system can efficiently ascertain the permitted data for synchronization based on the established permissions. This ensures that users only receive data for attributes or parents for which they have been explicitly granted read permissions, maintaining data privacy and security within the system.

JSON document example for establishing an ACL:


```json
{
  "id": 1,
  "version": 1,
  "signing_key": "Alice's public key",
  "pubkey_id": "1",
  "permissions": "3,5",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document",
  "signature": "cryptographic signature"
}
```

<br>

## 2.4 Database Schema

### 2.4.1 Introduction to the Database Schema

The database schema for the 2WAY system is designed to reflect the structure and relationships of the various objects discussed earlier, using SQLite3 as the chosen database. SQLite3 was selected for its versatility and ability to run on almost any (embedded) system, making it ideal for the lightweight and accessible nature of 2WAY. While future implementations could use other relational databases, graph databases, or alternative solutions, demonstrating the protocol's effectiveness at scale with SQLite3 will highlight its potential for increased efficiency as the system evolves and is deployed on more powerful hardware.

By organizing data into separate tables and establishing relationships between them through foreign keys, the schema ensures data integrity and enables efficient querying and retrieval operations within the SQLite3 database. Additionally, incorporating versioning fields allows for tracking changes over time and managing data revisions effectively. This schema design supports the creation, storage, and querying of various objects within the 2WAY system, providing a solid foundation for managing user data, reputation metrics, access controls, and other relevant information in a structured and organized manner.

In the 2WAY system, each plugin is responsible for creating its own set of tables within the backend database, adhering to the schema outlined in section 2.4.2, "Database Schema Design." Not only does this approach prevent plugins from interfering with each other, but it also enables plugins to access and utilize data from other plugins, fostering interoperability and collaboration within the system.

To achieve this, each plugin is assigned a unique "app_id" and can optionally have one or more "app_sub_id" identifiers. These identifiers are used to name the tables within the database, ensuring that each plugin's tables are distinct and identifiable. For instance, the default Contacts plugin in 2WAY might have the app_id "twoway" and the app_sub_id "connections," resulting in table names such as "twoway_connections_attributes," "twoway_connections_parents," "twoway_connections_edges," "twoway_connections_ratings," and "twoway_connections_acl."

The schema design for plugins is crafted to enable interoperability and seamless integration between different plugins within the system. Each plugin's tables follow the same structure and naming conventions, making it easy for plugins to interact with one another and share data as needed. By following a consistent schema design, plugins can leverage common functionalities and utilities provided by the core system, such as access control lists (ACLs), data indexing, and query optimization. This promotes code reusability and simplifies plugin development, allowing developers to focus on implementing unique features and functionalities without worrying about low-level database management tasks.

Additionally, the use of app_id and app_sub_id identifiers allows plugins to coexist within the same database environment while maintaining isolation and encapsulation of data. This approach enables developers to mix and match plugins according to their specific requirements, creating customized configurations tailored to their unique use cases.

Overall, replicating the database schema per plugin ensures modularity, flexibility, and interoperability within the 2WAY system. It empowers developers to build and extend the platform with new functionalities and features while maintaining consistency and compatibility across different plugins.

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

## 2.5 Object Manager

### 2.5.1 Introduction to the Object Manager

In the 2WAY system, the Object Manager serves as the central hub for creating and querying all the core objects, including Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). These objects are managed and accessed through APIs exposed by the backend's Object Manager, ensuring a streamlined and efficient handling of data interactions.

When users create objects such as Attributes or Parents, they interact with the frontend interface, which communicates with the backend's Object Manager via API calls. These API calls contain the necessary data to create the desired object, such as Attribute key-value pairs or parent-child relationships. Upon receiving these requests, the Object Manager processes the data, passes it to the Key Manager for signing, and then to the Storage Manager for the corresponding database operations to create the requested objects within the system. Additionally, it informs the ACL Manager, Graph Manager, and State Manager of any relevant changes, ensuring that the system remains up-to-date and consistent.

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
  "app_id": "2WAY, Contacts",
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
  "app_id": "2WAY, Contacts",
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
  "app_id": "2WAY, Contacts",
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
  "app_id": "2WAY, Contacts",
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
  "app_id": "2WAY, Contacts",
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
  "app_id": "2WAY, Contacts",
  "signing_key": "user_id",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "1",
  "timestamp": 1617000000,
  "hash": "generated_hash",
  "signature": "generated_signature"
}
```

Once signed, the messages are handed over to the Storage Manager, which appends them to the database. If the message pertains to an ACL, it is also relayed to the ACL Manager. Additionally, any necessary updates to the Graph in RAM are handled by passing the message to the Graph Manager.

When the Object Manager receives a message from the Network Manager (i.e., from another server), it directly appends the message by forwarding it to the Storage Manager. If the message involves an ACL, it is likewise relayed to the ACL Manager. Furthermore, any required updates to the Graph in RAM are managed by passing the message to the Graph Manager.

<br>

### 2.5.3 Hiding Objects

Objects within the 2WAY system are never deleted from the database. Instead, they can only be down-voted, which by default signifies their irrelevance or disapproval by the user. This approach ensures data integrity and historical traceability, as every interaction with an object is preserved. This is crucial because different users may have varying perspectives on the relevance or validity of an object, and preserving all objects allows the system to accommodate these differing opinions.

An examples of a JSON document for down-voting an Attribute, to be processed by the Object Manager:

```json
{
  "object": "attribute",
  "app_id": "2WAY, Contacts",
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
  "app_id": "2WAY, Contacts",
  "signing_key": "user_id",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "0",
  "timestamp": 1618000000,
  "hash": "generated_hash",
  "signature": "generated_signature"
}
```

The signed document is then appended to the database by the Storage Manager. The ACL Manager and Graph Manager are updated as necessary to reflect the down-vote in the Access Control Lists (ACLs) and in the Graph in RAM.

By preserving all objects and utilizing a down-vote mechanism, the 2WAY system allows users to filter and prioritize data according to their own preferences and judgments. This ensures a more personalized and user-centric experience, where each individual can curate their digital environment without permanently removing information that might be relevant to others.

While the current proof-of-concept (PoC) does not support automatic removal of objects, it is conceivable that future implementations could incorporate mechanisms for cleaning up the database. For example, duplicate objects, objects with an older version, or those beyond a certain age threshold could be automatically pruned to maintain database efficiency and manageability. However, such features are outside the scope of this PoC and would require careful consideration of criteria and processes to ensure consistency and data integrity.

<br>

### 2.5.4 Querying Objects

To query objects within the 2WAY system, users initiate requests through the frontend interface, which communicates with the backend's Object Manager via API calls. These API calls contain JSON documents specifying the parameters for the desired query, including the type of object and the degree of separation from the user's zeroth degree (their public key). By default, the system queries and returns the latest version of only the up-voted objects, ensuring that users receive the most relevant data.

Here is an example of a JSON document for querying up-voted objects:

```json
{
  "object": "attribute",
  "app_id": "2WAY, Contacts",
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
  "app_id": "2WAY, Contacts",
  "signing_key": "user_public_key",
  "degree": 2,
  "vote": 0,
  "latest": 0
}
```

By setting the "vote" parameter to "0," the system will retrieve the latest versions of down-voted objects, allowing users to access data that they or others might have found less relevant or disagreed with. This functionality provides a comprehensive view of the data landscape within the 2WAY system, accommodating different perspectives and preferences.

Upon receiving these JSON documents, the Object Manager processes the request by first interacting with the Graph Manager to identify the relevant nodes within the Graph in RAM. It then uses the resulting record IDs to query data from the database with the help of the Storage Manager. The system ensures that the queried objects match the specified parameters, including object type, degree of separation, and vote status, before returning the data to the frontend.

This approach to querying objects ensures that users can access the most relevant and up-to-date information by default, while still providing the flexibility to explore a broader range of data as needed. By supporting queries for both up-voted and down-voted objects, the 2WAY system offers a balanced and user-centric method for data retrieval, enhancing overall user experience and data discoverability.

<br>

### 2.5.5 Filtering Objects

In addition to querying objects, users can filter objects within the 2WAY system based on specific criteria. This filtering functionality allows users to narrow down their search results and focus on the most relevant information. Filtering can be applied to Attributes, Ratings, and other object types within the system, with the ability to specify voting status (1 for up-voted, 0 for down-voted). 

Below is an example of a JSON document for filtering objects based on specific criteria:

```json
{
  "object": "attribute",
  "app_id": "2WAY, Contacts",
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
  "app_id": "2WAY, Contacts",
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
  "app_id": "2WAY, Contacts",
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
- **app_id**: Specifies the application context, here it's "2WAY, Contacts."
- **signing_key**: The public key of the user initiating the query.
- **degree**: Limits the query to objects signed by anyone within 2 degrees of separation.
- **criteria**: Contains the filtering parameters:
  - **attribute_type**: "phone_number," indicating we want attributes of this type.
  - **vote**: 1, indicating we only want up-voted objects.
  - **parent**: Specifies the type of parent object we are interested in ("restaurant"), and excludes a specific value ("The French Cock").
  - **ratings**: Specifies criteria for ratings:
    - **min_score**: "1.75," indicating we want objects with a minimum score of 1.75.
    - **scale**: "out-of-5-stars," specifying the scale of the ratings.
    - **vote**: 1, indicating only up-voted ratings.
    - **signed_by**: Specifies that we want ratings from "Friends" and "Family."
  - **exclude_parents**: Excludes objects associated with specific parents ("people with bad taste in food").
  - **degree**: 0, limiting "exclude_parents" objects to those signed by the user, in the zeroth degree.

Upon receiving this JSON document, the Object Manager processes the request by first interacting with the Graph Manager to identify relevant nodes within the Graph in RAM. It then uses the resulting record IDs to query data from the database with the help of the Storage Manager, applying all specified filtering criteria before returning the data to the frontend.

This approach to filtering objects ensures that users can refine their queries to retrieve the most relevant and useful information, tailored to their specific needs and preferences. By supporting complex filtering criteria, the 2WAY system offers a robust and flexible method for data retrieval, enhancing overall user experience and data discoverability.

<br><br>

## 2.6 Graph Manager

### 2.6.1 Introduction to the Graph Manager

The Graph Manager in the 2WAY system manages the Graph in RAM and synchronizes it with the persistent disk-based Server Graph. It oversees storage, retrieval, and manipulation of graph data, ensuring efficient access and maintenance.

The Graph Manager handles the storage and retrieval of the in-memory graph to and from disk. During system initialization, shutdown, or significant updates, it transfers graph data between RAM and disk storage. This synchronization keeps the Graph in RAM aligned with the Server Graph for seamless data access and manipulation.

Additionally, the Graph Manager processes changes from the Object Manager, which handles object creation and querying by users. When changes occur, such as adding or removing nodes and edges, the Graph Manager updates the corresponding nodes and edges (not to be confused with the Edge object) in the Graph in RAM.

For example, when a user creates a new connection, the Graph Manager adds the corresponding node and edge with the table record ID that stores the Attribute of their public key to the Graph in RAM. Conversely, if a connection ("pubkey" Attribute) is down-voted, the Graph Manager removes the relevant node and edge from the Graph in RAM.

The Graph Manager also facilitates query operations by providing methods to retrieve nodes by degree of separation from the user's zeroth degree within the Server Graph. Users query the Object Manager, which then calls the Graph Manager to obtain table record IDs of relevant nodes within their User Graph, enabling efficient exploration and analysis.

The Graph Manager for this PoC focuses on storing record IDs of public key Attributes with app_id="twoway" and app_sub_id="connections" in the table "twoway_connections_attributes". For example, if Alice's first interaction is signing her own public key, storing it as an Attribute with the record ID "1" in the table, a node with the value "1" is added to the Graph in RAM. If Alice adds Bob's public key as an attribute with a record ID of "34", a node with the value "34" is added to the Graph in RAM, and an edge is established between nodes "1" and "34". When a "pubkey" Attribute is down-voted, it is removed from the Graph in RAM along with the edge between the two nodes.

Future versions of 2WAY may allow adding and removing other Attributes or Parents to and from the Graph in RAM, but this is outside the scope of the PoC.

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

The Graph Manager then adds a node with the value "34" to the Graph in RAM and creates an edge between nodes "1" (Alice) and "34" (Bob), establishing a connection between the two users.

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

While the current PoC focuses on managing connections represented by public key Attributes, future versions of 2WAY could potentially allow for the addition and removal of other types of Attributes or Parents from the Graph in RAM. However, these enhancements are beyond the scope of this PoC and would require additional considerations for implementation.

In summary, the Graph Manager in the 2WAY system dynamically adjusts the Graph in RAM to reflect changes in connections, ensuring data accuracy and efficient query operations. The use of JSON documents facilitates the management of nodes and edges, highlighting the flexibility and scalability of the system.

<br>

### 2.6.4 Querying Nodes from RAM

In the 2WAY system, querying nodes from the Graph in RAM allows users to efficiently retrieve relevant data based on specified criteria. This process involves traversing the in-memory graph to identify nodes that meet the query conditions, providing users with accurate and timely results.

Consider a scenario where a user wants to query nodes representing connections within their network, specifically retrieving Attributes of type "email" associated with their immediate connections. The following JSON document outlines the query parameters:

```json
{
  "object": "attribute",
  "attribute_type": "email",
  "degree": 1,
  "signing_key": "user_public_key",
  "app_id": "twoway",
  "app_sub_id": "connections"
}
```

Upon receiving this query, the Graph Manager utilizes NetworkX functionalities to traverse the Graph in RAM and identify nodes matching the specified criteria. The following Python code demonstrates how such a query could be executed:

```python
import NetworkX as nx

def query_nodes(graph, user_public_key, attribute_type, degree, app_id, app_sub_id):
    # Initialize list to store query results
    query_results = []
    
    # Traverse graph to identify nodes matching query criteria
    for node in graph.nodes():
        # Check if node meets query conditions
        if graph.nodes[node]['type'] == attribute_type and \
           nx.shortest_path_length(graph, source=user_public_key, target=node) <= degree and \
           graph.nodes[node]['app_id'] == app_id and \
           graph.nodes[node]['app_sub_id'] == app_sub_id:
            # Add node to query results
            query_results.append(node)
    
    return query_results

# Example usage
query_results = query_nodes(Graph_in_RAM, "user_public_key", "email", 1, "twoway", "connections")
```

In this example, the `query_nodes` function traverses the Graph in RAM, checking each node against the specified query criteria. Nodes meeting all conditions, including having the desired attribute type, being within the specified degree of separation from the user, and having the appropriate app_id and app_sub_id, are added to the list of query results.

Once the query is completed, the relevant node identifiers are returned as query results, providing users with the information they requested.

By leveraging the Graph in RAM and NetworkX functionalities, the 2WAY system enables efficient querying of nodes, empowering users to explore and interact with their network connections effectively.

<br><br>

## 2.7 Storage Manager

### 2.7.1 Introduction to the Storage Manager

### 2.7.2 Storage Engine

#### 2.7.2.1 Create Database and Tables

#### 2.7.2.2 Storage and Retrieval

<br>

## 2.8 Key Manager

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

## 2.10 Network Manager

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

## 2.12 Log Manager

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




[ ] 2.5.4 "latest" not described, 1 = latest object version and 0 = all object versions
[ ] Add "latest" to "2.5.5 Filtering Objects"
[ ] Querying Objects --> Vote = empty to query both up and down-voted objects
[ ] Add user_id description
[ ] Change user_public_key to user_id where needed
[ ] Rename Message Manager to Object Manager
[ ] Breakdown all the JSON documents like under "2.5.5 Filtering Objects"
[ ] Improve "2.3 2WAY Objects"
[ ] Change "2WAY" to "twoway" where needed
[ ] Change "Contacts" to "connections" where needed
[ ] Change database schema to prevent plugin name collision in table name
