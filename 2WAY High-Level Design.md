



# 2WAY: High-Level Design Document

<br><br>

# Introduction

In today's digital landscape, centralized identity and reputation systems are ubiquitous, serving as the foundation for online interactions. While these systems offer convenience, they also introduce inherent vulnerabilities and limitations that impact both users and third-party service providers. From privacy concerns to regulatory compliance challenges, centralized systems pose significant risks and costs to all stakeholders.

For users, centralized identity and reputation systems often require the disclosure of sensitive personal information to third-party intermediaries. This reliance raises privacy concerns and exposes users to data breaches and unauthorized access. Additionally, users may face restrictions on their digital freedoms, as centralized systems are subject to censorship and control by a single authority.

For third-party service providers, managing and securing vast amounts of user data within centralized systems incurs significant costs related to data storage, security measures, and regulatory compliance. As these systems grow, they become more susceptible to attacks, posing reputational risks and potential legal liabilities.

Decentralizing identity and reputation management can mitigate these risks and costs for both users and service providers. By distributing user data across a decentralized network, the need for central intermediaries is reduced, minimizing the risk of data breaches and unauthorized access. Decentralized systems offer greater transparency and security, as user data is cryptographically secured and managed with the help of decentralized graphs.

For service providers, decentralizing applications can streamline operations and reduce overhead costs associated with data management and security. Leveraging decentralized technologies like distributed graphs and peer-to-peer (P2P) networks enhances data privacy, reduces regulatory burdens, and mitigates the risk of cyber attacks.

Enter 2WAY, a proposal for a proof-of-concept (PoC) offering a purely P2P version of electronic identity and reputation. At its core, 2WAY empowers users to issue their own cryptographic identities, control linked data, and establish secure communication channels without trusted intermediaries. Through digital signatures, a graph, and a P2P network, 2WAY enables users to curate their digital personas, filter information for relevancy, and interact directly with trusted parties securely.

Designed to be lightweight, 2WAY can run both the frontend (client) and backend (server) on a desktop computer, making it accessible and practical for a wide range of users. Although the main goal of the 2WAY PoC is to demonstrate the 2WAY protocol, the platform leverages the Flask framework for both the frontend and backend, merging them into a single application. This integrated approach simplifies development and deployment. Once the PoC has proven effective, the backend could be implemented as a daemon or service in a low-level language, and the frontend could be developed using any language or framework.

The foundation of 2WAY lies in its distributed identity, reputation, and access management server, which leverages cryptographic proof to verify message authenticity and establish secure communication channels between servers. Through a decentralized network of trusted nodes, users can exchange data with confidence, knowing that their identities and interactions are protected by robust cryptographic mechanisms.

Furthermore, 2WAY is designed with extensibility in mind, allowing developers to build plugins that serve as applications within the 2WAY system. These plugins can leverage the platform's core functionalities, enabling a diverse range of applications and services to be built on top of the 2WAY infrastructure.

Drawing inspiration from the principles of privacy by design, 2WAY ensures that personally identifiable information is processed minimally, with private messages and data shared only with consent and encrypted for the intended recipient. Public messages can be broadcast on a best-effort basis, though this remains outside the scope of this PoC.

This document navigates through the intricate layers of the 2WAY system, beginning with an exploration of its frontend infrastructure and extending to its backend architecture.

Within the Frontend section, we explain the Flask framework, the backbone of 2WAY's frontend, and examine the concept of plugins, from pre-installed options to the development of custom plugins.

Transitioning to the Backend section, we uncover the foundational elements of the 2WAY Graph, alongside the management of core 2WAY Objects such as Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). Additionally, we describe the Database Schema and dive deep into the functionalities of essential backend components, including the Message Manager, Graph Manager, Storage Manager, and more.

Finally, within the Practical Examples section, we illustrate the real-world applications of 2WAY across various scenarios, demonstrating its versatility and efficacy in managing contacts, messaging, social interactions, addressing security challenges like Sybil attacks, navigating markets, verifying binaries, and handling key management tasks.

In summary, 2WAY offers a groundbreaking approach to electronic identity and reputation management by decentralizing these processes and empowering users with greater control and security. By eliminating the need for centralized third parties, 2WAY reduces the risks and costs associated with managing and securing user data, benefiting both users and service providers. This PoC demonstrates the potential of running both frontend and backend on a single desktop computer, leveraging the Flask framework for a seamless, integrated experience. With its extensible plugin architecture, 2WAY provides a versatile platform for developers to create a wide range of applications, fostering a resilient and user-centric digital ecosystem. This document will guide you through the detailed workings of 2WAY, highlighting its potential to revolutionize the way we manage digital identities and interactions in a secure, decentralized manner.

<br><br>

# 1. Frontend

## 1.1 Introduction to the Frontend

The frontend of the 2WAY system serves as the user-facing interface, providing a gateway to interact with the platform's features and functionalities.

In this section, we explore the infrastructure that powers the frontend, starting with an exploration of the Flask framework. Flask serves as the foundation for building the frontend, offering a lightweight and flexible framework for web application development.

We also examine the concept of plugins, which extend the functionality of the frontend, enhancing its versatility and modularity.

From pre-installed plugins that come bundled with the system to the possibility of developing custom plugins, we uncover the diverse ways in which the frontend architecture of 2WAY can be tailored to meet specific user needs and preferences.

<br>

## 1.2 Flask

Flask serves as the cornerstone of both the frontend and backend architecture in the 2WAY system, offering a versatile and lightweight framework for web application development. Traditionally known for its usage in backend development, Flask is uniquely employed in 2WAY to power not only the server-side components but also the client-side user interface. This innovative approach merges the frontend and backend into a cohesive unit, simplifying development and deployment processes while promoting code reusability and maintainability.

Leveraging Flask for both frontend and backend operations streamlines communication between the user interface and the underlying server infrastructure, facilitating seamless data exchange and interaction. With its intuitive syntax and extensive ecosystem of extensions, Flask empowers developers to create responsive, dynamic, and feature-rich web applications that embody the principles of simplicity, flexibility, and scalability.

Through its integration into the 2WAY system, Flask provides a robust foundation for building a user-centric frontend experience that seamlessly integrates with the backend services, ensuring a cohesive and intuitive user interface for interacting with the platform's features and functionalities.

<br>

## 1.3 Plugins

Within the 2WAY system, Flask plugins are utilized on the frontend to facilitate communication with the Message Manager on the backend. These plugins serve as intermediary components that enable seamless interaction between the user interface and the backend services, allowing for efficient retrieval and display of data within the frontend application.

The Flask plugins encapsulate various functionalities and features designed to enhance the user experience and streamline interactions with the backend systems. These plugins are integrated into the frontend application built on the Flask framework, providing a modular and extensible architecture for managing data and user interactions.

At their core, Flask plugins leverage the Flask ecosystem's capabilities to establish connections with the backend's Message Manager, which serves as the central hub for handling all data operations within the system. Through these connections, the frontend can send requests and receive responses from the backend, enabling real-time updates and synchronization of data between the user interface and the underlying server infrastructure.

The Message Manager on the backend is responsible for processing incoming requests from the frontend, executing the necessary operations to retrieve, manipulate, or query data stored within the Server Graph, and returning the results to the frontend for display. This includes tasks such as retrieving user attributes, updating graph structures, querying for relevant information, and managing access control and permissions.

By leveraging Flask plugins, the frontend application can seamlessly interact with the Message Manager and access the full range of functionalities offered by the backend services. This enables users to perform various actions within the application, such as creating new objects, updating existing data, querying for information, and collaborating with other users, all while maintaining a responsive and intuitive user experience.

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

# 2. Backend

## 2.1 Introduction to the Backend

The backend of the 2WAY system is the cornerstone of its decentralized identity, reputation, and access management framework. It is meticulously designed to handle the complex processes required to maintain secure, efficient, and reliable operations within the 2WAY ecosystem. This backend infrastructure supports the creation, management, and verification of cryptographic identities and facilitates secure data exchanges between trusted nodes in a peer-to-peer (P2P) network.

At the core of the backend lies the 2WAY Graph, a comprehensive data structure that integrates both the User Graphs and the Server Graph. The User Graph represents the individual user's interactions. In contrast, the Server Graph is the aggregate of all User Graphs on a particular server, thereby encapsulating a subset of the network’s decentralized data.

The backend is responsible for managing various types of 2WAY Objects, which are fundamental to the system's operation. These objects include Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). Attributes are key-value pairs consisting of a type and a value, which can be up or down-voted, influencing their visible presence in the graph. Ratings are specific objects used to store reputation scores. Parents can have one or more Attributes as children, and the relationships between a Parent and its children are established through Edges. ACLs are used to define and manage access permissions within the system.

Several crucial components support the functionality and security of the 2WAY backend. The Database Schema ensures data is organized and structured efficiently. The Message Manager handles the reception of messages from the frontend, backend, or any connected application or device with access to the backend’s APIs, ensuring secure and reliable communication. The Graph Manager oversees the Graph in RAM only, maintaining the integrity and updates of the active data structure, while the overall 2WAY Graph encompasses the entire Server Graph, and is stored to disk.

The Key Manager is vital for handling the signing and verification of messages, as well as the encryption and decryption of communications. The ACL Manager oversees permissions and access rights, ensuring secure and authorized data access. The State Manager tracks the data that has been synchronized with other servers and manages data pending synchronization on the next connection.

Additional components enhance the backend's robustness and reliability. The Storage Manager handles the physical storage of data, while the Network Manager manages the network connections between nodes, ensuring efficient data exchange. The Denial of Service (DoS) Guard Manager protects the system from malicious attacks, maintaining network performance and availability. The Log Manager records system activities for auditing and troubleshooting, and the Installation and Startup Managers facilitate the deployment and initialization of the 2WAY system.

In essence, the 2WAY backend is a sophisticated and modular system that provides the secure and decentralized foundation needed for the 2WAY platform's operations. It integrates various components and data structures to create a resilient and efficient framework for managing digital identities and reputations in a P2P network. This section explains each element in detail, offering a comprehensive understanding of the backend architecture and its critical role within the 2WAY system.

<br>

## 2.2 2WAY Graph

### 2.2.1 Introduction to the 2WAY Graph

The 2WAY Graph lies at the core of the 2WAY system, serving as a dynamic and interconnected framework for representing and organizing data.

At its essence, the 2WAY Graph embodies a graph-based data model that leverages nodes and edges to model relationships and interactions between various entities within the system. Nodes represent individual objects such as Attributes, Parents, Ratings, and Access Control Lists (ACLs), while Edges denote the connections and associations between Parent objects and Attributes.

The 2WAY Graph is distinguished by its decentralized and distributed nature, empowering users to create, share, and collaborate on data in a flexible and scalable manner. By embracing a graph-based approach, the system facilitates intuitive navigation, exploration, and discovery of interconnected data, enabling users to traverse relationships and uncover valuable insights within their social or organizational networks.

### 2.2.2 User Graph

The User Graph in the 2WAY system represents the individualized network of nodes and edges maintained by the user. It comprises the user's personal data, connections, and interactions, encapsulating their contributions and relationships within the broader context of the Server Graph, which is the combined set of all User Graphs within the system. Each user's graph is unique and reflective of their specific interactions, preferences, and network connections within the system.

One notable aspect of the User Graph is that users always query data from their zeroth degree, from their point of view, within the Server Graph. This means that users primarily interact with and retrieve data that directly pertains to them or is within their immediate network connections. When querying the Server Graph, users traverse their own graph, exploring relationships, attributes, and interactions that are directly relevant to them.

From the user's perspective, data in other User Graphs that doesn't overlap with their own User Graph doesn't exist. In other words, users only perceive and interact with data that is within their own User Graph or is directly connected to them through their network connections. Data outside of their immediate network or areas of interest is effectively invisible or inaccessible to them within the Server Graph.

This approach ensures that users maintain a focused and personalized view of the data within the 2WAY system, allowing them to efficiently navigate and interact with information that is directly relevant to their needs and interests. By querying from their zeroth degree within the Server Graph, users can effectively manage their data, discover relevant connections, and collaborate with others within their network while maintaining privacy and control over their personal information.

### 2.2.3 Server Graph

The Server Graph in the 2WAY system represents the collective aggregation of all individual User Graphs stored on the server. Each user within the system maintains their own graph, comprising nodes and edges representing their objects and relationships among them. The Server Graph, therefore, encompasses the totality of these individual User Graphs, consolidating them into a comprehensive network of interconnected data within the system.

At its core, the Server Graph serves as a unified repository that encapsulates the entirety of the system's data landscape, encompassing Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs), contributed by users. By consolidating individual User Graphs into a centralized repository, the Server Graph facilitates seamless communication, collaboration, and data sharing among users within the system.

The Server Graph is dynamic and continually evolving, reflecting the real-time interactions and updates made by users across the platform. As users create, modify, or delete objects within their individual graphs, these changes are propagated to the Server Graph, ensuring that it remains synchronized and up-to-date with the latest data contributions from all users.

Overall, the Server Graph serves as the backbone of the 2WAY system, embodying the collective intelligence and contributions of its local user base. By consolidating individual User Graphs into a unified framework, the Server Graph enables seamless data management, discovery, and collaboration within the platform, while ensuring privacy, security, and access control based on user-defined permissions and network connections.

### 2.2.4 Graph on Disk

The Graph on Disk in the 2WAY system refers to the storage mechanism used to persist the Server Graph, comprising the aggregated data from all individual User Graphs, onto disk. This disk-based representation of the Server Graph ensures durability, accessibility, and scalability of the system's data, enabling efficient storage and retrieval of information across the entire user base.

The Server Graph, in its entirety, is stored to disk using the SQL schema as discussed in "2.4 Database Schema." This schema design organizes the data into pre-defined separate tables for each plugin, each corresponding to specific object types such as Attributes, Parents, Edges, Ratings, and Access Control Lists (ACLs). By leveraging a relational database management system (RDBMS) such as SQLite3, MySQL, or PostgreSQL, the Server Graph can be efficiently persisted and managed on disk, facilitating seamless data storage and retrieval operations.

The Graph on Disk serves as the authoritative source of truth for the 2WAY system, housing the complete dataset that encompasses the collective intelligence and contributions of the users. Updates, modifications, and interactions made by users are reflected in real-time within the Server Graph on disk, ensuring that the data remains synchronized and up-to-date with the latest user activity.

Furthermore, the Graph on Disk enables efficient querying, filtering, and analysis of data within the 2WAY system, empowering users to explore connections, discover insights, and collaborate effectively within their network. By persisting the Server Graph to disk using the established SQL schema, the 2WAY system maintains data integrity, consistency, and reliability, while facilitating seamless data management and scalability for future growth and expansion.

### 2.2.5 Graph in RAM

The Graph in RAM in the 2WAY system serves as an in-memory representation of a subset of the Server Graph, stored temporarily in the system's Random Access Memory (RAM). This in-memory graph is populated and maintained using the NetworkX library, a powerful tool for analyzing and manipulating graph data structures in Python.

One of the key functionalities of the Graph in RAM is to store the table record IDs of public key Attributes from the database on disk. These pubkey attributes serve as nodes within the graph, representing individual users within the system. By storing these record IDs in memory, the system can quickly retrieve and access relevant nodes during query operations, enabling efficient traversal and exploration of the Server Graph.

The Graph in RAM is designed to facilitate rapid querying of data from the disk-based Server Graph. When a user initiates a query, the system first retrieves relevant nodes from the in-memory graph based on the degree of separation specified in the query. These nodes serve as starting points for traversing the Server Graph stored on disk, allowing the system to narrow down the scope of the query and retrieve only the necessary data.

Furthermore, the Graph in RAM can be dynamically extended with additional 2WAY objects as needed to speed up querying for certain data. For example, if a user frequently queries for attributes or parents within their immediate network, these objects can be cached in memory to expedite future query operations.

However, it's essential to note that maintaining a Graph in RAM comes at a relatively high cost compared to directly retrieving data from the SQL database. While in-memory operations are faster, they consume system resources and memory, potentially impacting overall system performance. Therefore, the Graph in RAM should be used conservatively and selectively, focusing on caching frequently accessed data or optimizing specific query patterns to enhance overall responsiveness and user experience within the 2WAY system.

<br>

## 2.3 2WAY Objects

### 2.3.1 Introduction to 2WAY Objects

In 2WAY, a small set of simple data structures are used to construct objects. These objects, represented as nodes and edges within the 2WAY graph, encompass all of the data stored within the system. The following objects are used to construct the system in its entirety:

~~~
1. "Attribute": Key-value pair, consisting of a type and a value.

2. "Parent": Parent attribute, to be connected to one or more child attributes via edges.

3. "Edge": Edge between a single parent attribute and one or more child attributes.

4. "Rating": Score with rating scale and/or comment, assigned to attribute or parent.

5. "Access Control List" (ACL): Context-specific permissions for authorized users used to synchronize data.
~~~

Using these objects, any required application can be modeled atop.

### 2.3.2 Attribute

An attribute consists of a key-value pair, in the form of a "type" and a "value," functioning as a node within the server's graph structure. For instance, attributes such as type="name" with a corresponding value="Alice", or type="pubkey" with a lengthy public key value. Any attribute can be defined dynamically, either on the frontend, communicating with the backend through APIs, or by the backend itself.

The two discussed example attributes:

~~~
{
	"type": "name",
	"value": "Alice"
},

{
	"type": "pubkey",
	"value": "really long pubkey here"
}
~~~

Whenever a user initiates an action on the frontend that generates an attribute, it is transmitted to the backend's Message Manager API as a JSON document:

~~~
{
  "app_id": "2WAY, Contacts",
  "attribute_type": "name",
  "attribute_value": "Alice",
  "vote": "1",
  "timestamp": "1648062000"
}
~~~

Here, the "app_id" serves as the identifier for the frontend application, "2WAY," along with one of the application's sub-IDs, "Contacts." The backend uses this information to determine where to store the data. The attribute's key-value pair is defined as "name" for type, and "Alice" as its value. The vote is boolean. The value of "1" signifies that the object is relevant, whereas the value "0" indicates that the object is not relevant (any longer). When the latest version of an object contains the value "0" for "vote," the object is disregarded during future queries, unless specifically requested. The latest version of an object is the one returned when queried for, by default.

After the Message Manager receives a new object from the frontend application, the process starts that enables the creation of various object types within the system by authorized users. The newly created attribute is linked to the user's public key through an edge. This edge does not have to be stored separately, as the public key is also stored as an attribute (node within the graph), and the newly created attribute contains the signer's public key and signature. The message is signed by being passed to the Key Manager, that runs on the backend as well. This is where all key-management takes place, in an automated fashion.

Moreover, the Message Manager facilitates attribute querying, allowing for filtering based on the degree of separation and additional contextual criteria.

Once the data is stored, the following result is returned when the newly created object is queried:

~~~
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
~~~

### 2.3.3 Parent

The parent object consists of a single parent attribute and one or more other attributes and/or parents as its children. An example:

~~~
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
~~~

In this example, the parent's type is "pubkey" with the value "Alice's pubkey." The attributes with the types "name," "email," and "address" are child-attributes linking to a single attribute. The links are established outside of the parent as edges. However, note that the child with child_type="group" is a parent that serves as a child-attribute, and that the user who is creating the object(s) could be a part of this group themselves, as a child-attribute of said parent.

In the 2WAY system, users are typically identified within the graph by their public key (pubkey). Consequently, a user's parent attribute might appear as name="pubkey" with a corresponding value="really long pubkey". Subsequently, the user's name or email address can be associated as child attributes, such as type="username" with a value like "Alice", or type="email" with a value like "Alice@gmail.com". This approach enables the establishment of necessary parent-child relationships to organize and retrieve data effectively.

To create objects other than users, one simply needs to define the required attribute. For example, to store blog articles, one could utilize type="Post" with a corresponding value for the post title. Similarly, for building a marketplace and adding products, starting with type="category" and value="Books" could be a first step, followed by adding relevant children attributes. For a blog post, these children could include attributes like title, author name, content, and publication date, while for a book, attributes like author, ISBN code, or content could be added.

JSON document example for establishing a parent:

~~~
{
  "id": 1,
  "version": 1,
  "type": "defined by system or plugin",
  "signing_key": "Alice's public key",
  "parent_id": "4",
  "parent_version": "1",
  "vote": "1",
  "timestamp": "1648062000",
  "hash": "hash of the document",
  "signature": "cryptographic signature"
}
~~~

### 2.3.4 Edge

Whenever a new attribute or parent-child relationship is formed, an edge is established between the newly created object and the attribute containing the public key of the signer. Additionally, edges are created between parent and child attributes within the graph to denote their relationship. These edges serve to maintain the structural integrity of the graph and facilitate efficient data retrieval and organization.

Only edges between parents and children are stored separately, as edges between newly created attributes and public keys are established within the attributes themselves, as the linked public key is already present. The same goes for reputation ratings and access control lists (ACLs), who also contain the associated public keys within themselves.

JSON document example for establishing a parent-child edge:

~~~
{
  "id": 1,												# INT
  "version": 1,											# INT
  "type": "defined by system or plugin",				# TEXT
  "signing_key": "Alice's public key",					# TEXT
  "parent_id": "4",										# INT
  "parent_version": "2",								# INT
  "child_ids": "5,9,12,13,14",							# TEXT
  "child_versions": "1,1,2,1,1",						# INT
  "vote": "1",											# INT
  "timestamp": "1648062000",							# INT
  "hash": "hash of the document",						# TEXT
  "signature": "cryptographic signature"				# TEXT
}
~~~

### 2.3.5 Rating (Reputation)

In the context of 2WAY, the reputation of users or entities can be represented and managed through a JSON document structured to include various details related to reputation metrics, or, ratings. These metrics could encompass factors such as comments, scores, and scales, all of which contribute to the overall reputation score of users and entities within the system.

The data structure for ratings is designed to include fields such as:

~~~
"comment": A string field allowing users to provide comments or feedback about the entity being rated.

"score": A string field indicating a score assigned to the entity based on a predefined rating scale.

"scale": A string field specifying the type or category of the rating scale used for assigning scores.
~~~

By structuring the data in this manner, it becomes flexible and adaptable to different types of ratings and scales. This document can then be signed onto an attribute or parent within the system to ensure authenticity and integrity. The signature ensures that the reputation data is securely associated with the respective attribute or parent, providing a reliable record of reputation metrics within the 2WAY framework.

JSON document example for establishing a rating:

~~~
{
  "id": 1,												# INT
  "version": 1,											# INT
  "type": "defined by system or plugin",				# TEXT
  "signing_key": "Alice's public key",					# TEXT
  "attribute_id": "1",									# INT
  "attribute_version": "1",								# INT
  "parent_id": "",										# INT
  "parent_version": "",									# INT
  "comment": "wow this is really great!",				# TEXT
  "score": "13",										# TEXT
  "scale": "out-of-10-but-up-to-13",					# TEXT
  "vote": "1",											# INT
  "timestamp": "1648062000",							# INT
  "hash": "hash of the document",						# TEXT
  "signature": "cryptographic signature"				# TEXT
}
~~~

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

~~~
{
  "id": 1,												# INT
  "version": 1,											# INT
  "signing_key": "Alice's public key",					# TEXT
  "pubkey_id": "1",										# INT
  "permissions": "3,5",									# TEXT
  "vote": "1",											# INT
  "timestamp": "1648062000",							# INT
  "hash": "hash of the document",						# TEXT
  "signature": "cryptographic signature"				# TEXT
}
~~~

<br>

## 2.4 Database Schema

<br>

## 2.5 Message Manager

<br>



<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>




### 2.2.6 Graph Manager

The Graph Manager in the 2WAY system acts as an intermediary layer responsible for managing the Graph in RAM and facilitating its synchronization with the persistent disk-based Server Graph. It oversees the storage, retrieval, and manipulation of graph data, ensuring efficient access and maintenance of the system's graph structure.

One of the primary functions of the Graph Manager is to store and retrieve the in-memory graph to and from disk. When the system initializes or shuts down, or when there are significant updates to the graph data, the Graph Manager handles the transfer of graph data between RAM and disk storage. This ensures that the Graph in RAM remains synchronized with the persistent Server Graph, enabling seamless data access and manipulation.

Additionally, the Graph Manager serves as a gateway for processing changes received from the Message Manager, a component responsible for handling incoming messages and updates from users. When a change is received, such as the addition, removal, or update of nodes and edges within the graph, the Graph Manager processes the change and updates the relevant nodes and edges in the Graph in RAM accordingly.

For example, if a new connection with another user is created by a user, the Graph Manager adds the corresponding node/edge with the table record ID that stores the attribute of their pubkey to the Graph in RAM. Conversely, if a node or edge is deleted or modified, the Graph Manager performs the necessary adjustments to maintain data consistency within the Graph in RAM.

Furthermore, the Graph Manager facilitates query operations by providing methods to retrieve nodes by degree of separation from the user's zeroth degree within the Server Graph. Users can query the Message Manager, who then calls the Graph Manager to obtain table record IDs of relevant nodes within their User Graph, enabling efficient exploration and analysis of graph data.

Overall, the Graph Manager plays a critical role in ensuring the integrity, accessibility, and responsiveness of the graph data within the 2WAY system. By managing the synchronization between the Graph in RAM and the persistent Server Graph, as well as handling incoming changes and query requests, the Graph Manager facilitates efficient data management and interaction within the platform.

<br><br>


# 3. Storage & Querying

<br>

## 3.1 Storage Manager

<br>

The Storage Manager component of the current model leverages SQLAlchemy, a popular Object-Relational Mapping (ORM) tool in Python, to interact with the underlying database. SQLAlchemy simplifies database operations by providing a high-level abstraction layer that allows developers to work with databases using Python objects and methods.

However, it may be advantageous to forego the use of SQLAlchemy and instead manually code all the necessary SQL instructions directly within Python.

While SQLAlchemy and other ORMs offer convenience and productivity benefits, manually coding SQL instructions within Python provides greater control, performance optimization, and flexibility, albeit at the cost of increased development complexity and potential maintenance overhead.

The design for this proof-of-concept only ever appends new records to the database, and updates none. Instead of deleting objects, they can be down-voted, as any attribute can receive a boolean down-vote (false) through a new record with a newer version of said attribute. Only the newest version of any attribute is returned, by default, given that its vote is "true." However, the historical log of all interactions within the system is kept for the user to browse when needed. In a future version of the 2WAY system this could be optimized further for performance, as not all actions are always required to be stored indefinitely.

<br>

## 3.2 Message Manager

<br>

In the 2WAY system, the Message Manager serves as a central hub for creating and querying all the objects discussed earlier, including attributes, parents, edges, reputation data, and access control lists (ACLs). These objects are managed and accessed through APIs exposed by the backend's Message Manager.

When creating objects such as attributes or parents, users interact with the frontend interface, which in turn communicates with the backend's Message Manager via API calls. These API calls contain the necessary data to create the desired object, such as attribute key-value pairs or parent-child relationships. Upon receiving these requests, the Message Manager processes the data, passes it to the Key Manager for signing, and executes the corresponding database operations to create the requested objects within the system. It then passes any relevant changes to the ACL Manager, Graph Manager, and State Manager.

Similarly, when querying objects within the 2WAY system, users initiate requests through the frontend interface, which communicates with the backend's Message Manager via API calls. These API calls specify the parameters for the desired query, by degree of separation from the user's zeroth degree (their public key), for the object type being queried. The Message Manager then retrieves the relevant nodes from the Graph Manager (Graph in RAM) and uses the resulting record IDs to query data from the database, and returns it to the frontend.

By centralizing object creation and querying functionality within the Message Manager and exposing it through APIs, the 2WAY system ensures consistency, security, and scalability in managing various types of objects and data within the system. This approach abstracts the complexities of database interactions and provides a unified interface for interacting with the system's objects, enhancing usability and maintainability.

It is outside of the scope of this proof-of-concept to have messages signed on the frontend. In a future version, messages could theoretically be signed on the frontend or with hardware keys.

<br>

## 3.3 Querying

<br>

One of the unique features of the 2WAY system is its querying mechanism, which operates based on the concept of degree of separation. In this system, objects are always queried by considering their proximity or relationship to the user initiating the query. This approach allows users to retrieve not only the objects they have directly created but also those that are one or more degrees of separation away from their own node within the graph structure.

By leveraging the degree of separation in querying, users can access a comprehensive view of the data within the system, encompassing not only their own contributions but also those of their connections and extended network. This enables users to explore and analyze data within the broader context of their social or organizational graph.

Furthermore, the querying mechanism in 2WAY offers flexibility in filtering and refining query results based on specific contextual criteria. Users can apply additional filters to narrow down the results according to various parameters, such as object type to include/exclude, timestamp, time range, reputation rating, or relevance to any particular context.

For example, a user could initiate a query to retrieve all blog posts authored by their direct connections (one degree of separation), or they could expand the query to include posts authored by connections of their connections (two degrees of separation). Additionally, they could further filter the results based on criteria such as post topic, or publication date, or a filter by ratings assigned by their connections.

This degree-based querying approach empowers users to explore and navigate the interconnected web of data within the 2WAY system effectively, facilitating comprehensive data discovery and analysis while ensuring privacy and access control based on the user's network connections.

<br>

## 3.4 Filtering

<br>

In addition to querying based on degree of separation, the 2WAY system offers robust filtering capabilities to refine query results further according to specific contextual requirements. This filtering functionality allows users to tailor their queries to extract relevant data and insights from the vast pool of interconnected objects within the system.

Users can apply various filters to narrow down query results based on different criteria, including but not limited to:

	1. Object Type: Users can specify the type of objects they are interested in retrieving, such as attributes, parents, children, reputation data, or access control lists (ACLs). This ensures that query results are relevant to the user's specific needs and use cases.

	2. Contextual Relevance: Users can apply additional contextual filters to refine query results based on specific attributes or metadata associated with the objects. For example, users may filter blog posts by topic, author, timestamp, or popularity, or filter reputation data by rating score or reviewer identity.

	3. Degree of Separation: Building upon the querying mechanism discussed earlier, users can further filter query results based on the degree of separation from their own node within the graph structure. This enables users to narrow down results to objects within their immediate network or extend the scope to include connections of their connections.

By combining degree-based querying with flexible filtering options, the 2WAY system empowers users to extract actionable insights from the interconnected web of data within the system. This approach facilitates targeted data exploration and analysis while ensuring privacy, access control, and contextual relevance based on the user's specific requirements and network connections.

<br>

## 3.5 Backend Database Schema

<br>

The schema design for the relevant SQLite3 database in the 2WAY system should reflect the structure and relationships of the various objects discussed earlier, including attributes, parents, reputation data, access control lists (ACLs), and any additional metadata required for indexing and querying.

Here's a proposed schema design for the SQLite3 database:


	1. Attributes Table:

		id INT,
		version INT,
		type TEXT,
		signing_key TEXT,
		attribute_key TEXT,
		attribute_value TEXT,
		vote INT,
		timestamp INT,
		hash TEXT,
		signature TEXT,
		PRIMARY KEY (id, version)


	2. Parents Table:

		id INT,
		version INT,
		type TEXT,
		signing_key TEXT,
		parent_id INT,
		parent_version INT,
		vote INT,
		timestamp INT,
		hash TEXT,
		signature TEXT,
		PRIMARY KEY (id, version),
		FOREIGN KEY (parent_id, parent_version) REFERENCES twoway_connections_attributes(id, version)


	3. Edges Table:

		id INT,
		version INT,
		type TEXT,
		signing_key TEXT,
		parent_id INT,
		parent_version INT,
		child_ids TEXT,
		child_versions TEXT,
		vote INT,
		timestamp INT,
		hash TEXT,
		signature TEXT,
		PRIMARY KEY (id, version),
		FOREIGN KEY (parent_id, parent_version) REFERENCES twoway_connections_parents(id, version)


	4. Reputation Table:

		id INT,
		version INT,
		type TEXT,
		signing_key TEXT,
		attribute_id INT,
		attribute_version INT,
		parent_id INT,
		parent_version INT
		comment TEXT,
		score TEXT,
		scale TEXT,
		timestamp INT,
		hash TEXT,
		signature TEXT,
		PRIMARY KEY (id, version),
		FOREIGN KEY (attribute_id, attribute_version) REFERENCES twoway_connections_attributes(id, version),
		FOREIGN KEY (parent_id, parent_version) REFERENCES twoway_connections_parents(id, version)


	5. ACL Table:

		id INT,
		version INT,
		signing_key TEXT,
		pubkey_id INT,
		permissions TEXT,
		timestamp INT,
		hash TEXT,
		signature TEXT,
		PRIMARY KEY (id, version),
		FOREIGN KEY (pubkey_id) REFERENCES twoway_connections_attributes(id, version)


By organizing the data into separate tables and establishing appropriate relationships between them using foreign keys, the schema design ensures data integrity and facilitates efficient querying and retrieval operations within the SQLite3 database. Additionally, incorporating versioning fields allows for tracking changes over time and managing data revisions effectively.

This schema design can accommodate the creation, storage, and querying of various objects within the 2WAY system, providing a solid foundation for managing user data, reputation metrics, access controls, and other relevant information in a structured and organized manner.

The tables in this schema are created for each individual plugin, as described below, under "4.4 Replicating the Database Schema per Plugin".

<br><br>

## 4.5 Replicating the Database Schema per Plugin

<br>

In the 2WAY system, each plugin is responsible for creating its own set of tables within the backend database, following the schema outlined in "2.6 Backend Database Schema." This approach ensures that each plugin has its own dedicated space within the database to store and manage data specific to its functionality, without interfering with other plugins or the core system.

To achieve this, each plugin is assigned a unique "app_id" and can optionally have one or more "app_sub_id" identifiers. These identifiers are used to name the tables within the database, ensuring that each plugin's tables are distinct and identifiable. For example, the default Contacts plugin in 2WAY may have the app_id "twoway" and the app_sub_id "connections," resulting in table names such as "twoway_connections_attributes," "twoway_connections_parents," "twoway_connections_edges," "twoway_connections_ratings," and "twoway_connections_acl."

The schema design for plugins is carefully crafted to enable interoperability and seamless integration between different plugins within the system. Each plugin's tables adhere to the same structure and naming conventions, making it easy for plugins to interact with one another and share data as needed.

Furthermore, by following a consistent schema design, plugins can leverage common functionalities and utilities provided by the core system, such as access control lists (ACLs), data indexing, and query optimization. This promotes code reusability and simplifies plugin development, allowing developers to focus on implementing unique features and functionalities without worrying about low-level database management tasks.

Additionally, the use of app_id and app_sub_id identifiers allows plugins to coexist within the same database environment while maintaining isolation and encapsulation of data. This approach enables developers to mix and match plugins according to their specific requirements, creating customized configurations tailored to their unique use cases.

Overall, replicating the database schema per plugin ensures modularity, flexibility, and interoperability within the 2WAY system, enabling developers to build and extend the platform with new functionalities and features while maintaining consistency and compatibility across different plugins.

<br><br>

# 5. Network and Sync

In the 2WAY system, establishing secure connections between users distributed across the network and ensuring synchronized data exchange are paramount for seamless communication and collaboration.

Leveraging Tor for secure communication beyond local servers and employing a robust State Manager for efficient data synchronization, the 2WAY system prioritizes privacy, anonymity, and data integrity to facilitate seamless interaction and collaboration among users.

<br>

## 5.1 Network Manager

<br>

## 5.2 Tor Integration

<br>

Tor is a fundamental component within the 2WAY system, facilitating secure and anonymous communication between users across distributed networks. Tor integration represents a cornerstone of the platform's commitment to privacy and confidentiality, providing users with a robust layer of anonymity while establishing connections beyond the confines of local servers.

By harnessing Tor's capabilities, users can establish encrypted channels for communication, safeguarding their identities and ensuring confidentiality throughout their interactions within the network.

Moreover, Tor's architecture enables users to obscure their network activity and obfuscate their IP addresses, bolstering privacy and anonymity in communication. The utilization of Tor within the 2WAY system underscores a commitment to user-centric security practices, fostering a trust-driven environment where users can engage in interactions with confidence and peace of mind.

<br>

## 5.3 Establishing Connections

<br>

Within the 2WAY ecosystem, the process of establishing connections transcends mere networking protocols, encompassing a multifaceted approach to facilitate seamless communication between users.

At the heart of connection establishment lies a robust framework that leverages users' stored public keys and Tor onion addresses, ensuring the integrity and confidentiality of communication channels. By harnessing these cryptographic constructs, users can initiate connections with counterparts beyond the confines of their local server environment, fostering a networked ecosystem that transcends geographical boundaries and server limitations.

Moreover, the incorporation of Tor into the connection establishment process adds an additional layer of anonymity and privacy, safeguarding users' identities and communication activities from prying eyes. Through encrypted and anonymized channels, users can engage in interactions with confidence, knowing that their privacy and security are prioritized at every stage of the connection establishment process.

<br>

## 5.4 Data Synchronization

<br>

## 5.5 State Manager

<br>





<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>







2WAY: High-Level Design


	Introduction

	
1.	Frontend

		Introduction

		Flask

		Plugins

		Pre-Installed Plugins

		Custom Plugins


2.	Backend

		Introduction

		2WAY Graph
			Introduction
			User Graph
			Server Graph
			Graph on Disk
			Graph in RAM

		2WAY Objects
			Introduction
			Attribute
			Parent
			Edge
			Rating
			Access Control List (ACL)

		Database Schema
			Introduction
			The Schema
			Replicating the Schema per Plugin

		Message Manager
			Introduction
			Message Engine
				Create Objects
				Query Objects
				Filter Objects

		Graph Manager
			Introduction
			RAM Graph Engine
				Storage & Retrieval
				Changes to Graph in RAM
				Querying Nodes from RAM

		Storage Manager
			Introduction
			Storage Engine
				Create Datbase & Tables
				Storage & Retrieval

		Key Manager
			Introduction
				Key-Management
			Key Engine
				Generate Keys
				Verify Signatures
				Sign Messages
				Encrypt Messages
				Decrypt Messages
			Revocation & Re-Issuance

		ACL Manager
			Introduction
			ACL Engine
				Receive Instruction
				Create ACLs
				Remove ACLs
				Verify ACLs
				Query ACLs

		State Manager
			Introduction
			State Engine
				Receiving Requests
				Querying States

		Network Manager
			Introduction
			Networking / Tor Integration
			Establishing Connections
			Data Synchronization
			Network Startup Engine
				Introduction
				Creating and Solving Client Puzzles
				Starting Onion Services
				Connecting with 1st Degree Connections
			Network Engine
				Introduction
				Creating Onion Services
				Starting Onion Services
				Stopping Onion Services
				Revoking Onion Services
				Closing Sockets
				Receiving Messages
				Sending Messages
			Client Puzzle Engine
				Introduction
				Creating Client Puzzles
				Creating and Solving Client Puzzles
				Querying and Verifying Client Puzzle Challenges / Solutions
			Bastion Engine
				Introduction
				Receiving Messages
			Incoming Engine
				Introduction
				Receiving Messages
			Outgoing Engine
				Introduction
				Sending Messages

		DoS Guard Manager
			Introduction
			DoS Guard Engine
				Receiving Bastion Alarm

		Log Manager
			Introduction
			Log Engine
				Logging Failed Operations
				Logging Failed Bastion Messages
				Logging Failed Incoming Messages

		Installation Manager
			Introduction
			Installation Engine
				Create Database and Tables
				Generate Key-Pairs
				Create Onion Services
				Create Client Puzzles
				Create Required Objects

		Startup Manager
			Introduction
			Startup Engine
				Start Graph Manager
				Start Network Manager


3.	Practical Examples

		Introduction

		Contacts

		Messaging

		Social

		Solving for Sybil

		Markets

		Verifying Binaries

		Key Revocation, Re-Issuance, and Propagation
