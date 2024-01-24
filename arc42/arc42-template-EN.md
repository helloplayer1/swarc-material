# Introduction and Goals

The image sharing app allows users to upload, edit and share images with their friends, family and the wider community. 

## Requirements Overview
Main features of the app are:

* Upload photos
* Share photos with friends, family and the wider community
* Image editing with third party integration (Pixlr)
* Community feed, challenges and comment options for interacting with other users

## Quality Goals

| Priority | Quality     | Motivation                                                                                              |
| -------- | ----------- | ------------------------------------------------------------------------------------------------------- |
| 1        | Security    | Protect the private data and rights of our users to gather their trust                                  |
| 2        | Reliability | Allows for rapid growth of our app. The platform must be able to handle hundreds of thousands of users  |
| 3        | Usability   | Make sure the user loves using our app                                                                  |

## Stakeholders

| Role/Name               | Expectations                                                   |
| ----------------------- | -------------------------------------------------------------- |
| Investor 1              | Return of Investment (ROI) for his share on the company        |
| Investor 2              | Long term investment and growth                                |
| Team Leader             | Hassle-free execution of the project                           |
| Lead Marketing Engineer | Popularize and grow the app                                    |
| Lead System Architect   | Build and maintain a scalable and secure hardware architecture |
| Lead Software Architect | Implement the software itself                                  |

<div style="page-break-after: always;"></div>

# Architecture Constraints

| Constraints                       | Backgrounds and/or motivation                                                                         |
| --------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Ease of use                       | The goal is to ensure the app is as accessible as possible                                            |
| Advanced editing posibilities     | The objective is to keep users within the app                                                         |
| Crossplatform Development         | Maintaining two codebases is not feasible due to resource constraints                                 |
| Backend Implementation in Node.Js | While the Backend is implemented in JavaScript, the API will be designed based on the REST principles |
| OS Independent development        | The development should work regardless of the desktop OS, as our team uses multiple different devices |

# System Scope and Context
## Business Context

![diagram](../diagrams/business_context.svg)

Our system interacts with Pixlr to support advanced image editing use cases and also allows for sharing content on other social media platforms. To ensure compliance with legislation and also our own rules for allowed content, we use an external AI service to analize image uploads and classify them. 
The individuals engaging with our system include the user, other community members, and government entities.

## Technical Context
**Explanation of Technical Interfaces**

- **HTTP/HTTPS Protocol**: This protocol serves as the primary means of interaction with external services, enabling functionalities like image editing through Pixlr integration and sharing content on other social media platforms. It processes incoming requests from users for various app features and sends corresponding responses.

- **Internal Messaging System**: This system allows different components or microservices within our app's architecture to communicate seamlessly. For instance, it facilitates interactions between the image processing service, user authentication service, and content sharing service.

- **Database Connectivity**: The database serves as a central repository for storing user-generated content, including uploaded images, user profiles, and application settings. It is accessed by various components to fetch required data and store new information.

**Mapping Input/Output to Channels**

| Input/Output               | Channel                   |
| -------------------------- | ------------------------- |
| User image upload          | HTTP/HTTPS Protocol       |
| Image editing requests     | HTTP/HTTPS Protocol       |
| Content sharing            | HTTP/HTTPS Protocol       |
| Internal service requests  | Internal Messaging System |
| Database queries/retrieval | Database Connectivity     |

This mapping table outlines the correspondence between specific input/output actions and the channels through which they operate within the system's technical interfaces.

<div style="page-break-after: always;"></div>

# Solution Strategy

The app will be developed as a multiplatform app with a shared code base using the Flutter framework. While the flutter app represents the client side of the app, the backend and server will be implemented as a Node.JS application.

| Goal/Requirement          | Architectural Approach      | Details                                                 |
| ------------------------- | --------------------------- | ------------------------------------------------------- |
| Consistent Communication  | RESTful Architecture        | [Rest Api Details](#rest-api)                           |
| Image Handling Standard   | Standardization             | [Image Format](#image-format-png)                       |
| Data Security and Privacy | End-to-End Encryption (e2e) | [Security and Privacy Details](#security-and-privacy)   |
| Unified Logging           | Centralized Logging         | [Common logging format Details](#common-logging-format) |



<div  style="page-break-after: always;"></div>

# Building Block View
## Whitebox Overall System

![Level 1](../diagrams/building_block_view_level_1.svg)


Motivation

The motivation behind this decomposition is to achieve a modular and scalable design that enhances maintainability, flexibility, and collaboration among development teams. Each building block plays a importantrole in fulfilling specific functionalities and, when combined, forms a cohesive and robust system.

By breaking down the system into distinct components such as UI Client, Search, Posts, User Management, Third-party Integration, File Storage, and Authentication, we aim to encapsulate specific responsibilities within well-defined boundaries. This approach improves the code reusability, allows independent development and testing of each module.

As we explore the descriptions and connections of each black box, we will explain how our system works on the inside.



  | Building Block          | Description                                                                                                                   |
  | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
  | UI Client               | The user interface component responsible for rendering and interacting with the application on the client side.               |
  | Search                  | Functionality for searching and retrieving relevant information from the system, enhancing user experience.                   |
  | Posts                   | Manages the creation, retrieval, and manipulation of user-generated content, such as articles, posts, or messages.            |
  | User Management         | Handles user-related functionalities, including registration, login, profile management, and permissions.                     |
  | Third-party Integration | Enables the integration of external services or APIs to enhance the application's functionality through third-party services. |
  | File Storage            | Manages the storage and retrieval of files, images, or other media within the system.                                         |
  | Authentication          | Ensures secure access to the system by verifying and validating the identity of users during login and session management.    |


### UI Client

**Purpose/Responsibility:**  
The UI Client serves as the front-end interface responsible for rendering and facilitating user interaction with the application. It provides a visually appealing and user-friendly experience, ensuring seamless navigation and accessibility.

**Interface(s):**

-   User input handling
-   Communication with the server-side components through defined API endpoints

**Quality/Performance Characteristics:**

-   Responsiveness
-   Cross-browser compatibility
-   User interface responsiveness

**Directory/File Location:**

-   `/client/ui`

**Fulfilled Requirements:**

-   Requirement #1: Intuitive user interface design
-   Requirement #2: Cross-browser compatibility

**Open Issues/Problems/Risks:**

-   Potential latency issues in resource-intensive operations

### Search

**Purpose/Responsibility:**  
The Search component is responsible for enabling users to search and retrieve relevant information within the system efficiently. It enhances user experience by providing quick and accurate search results.

**Interface(s):**

-   Query processing and indexing
-   Integration with external search engines or algorithms

**Quality/Performance Characteristics:**

-   Search accuracy
-   Query response time

**Directory/File Location:**

-   `/services/search`

**Fulfilled Requirements:**

-   Requirement #5: Efficient and accurate search functionality

**Open Issues/Problems/Risks:**

-   Integration challenges with certain search algorithms

### Posts

**Purpose/Responsibility:**  
The Posts component manages the creation, retrieval, and manipulation of user-generated content such as articles, posts, or messages within the system.

**Interface(s):**

-   CRUD (Create, Read, Update, Delete) operations for posts
-   Integration with the authentication system for user-specific posts

**Quality/Performance Characteristics:**

-   Speed and efficiency in handling large datasets

**Directory/File Location:**

-   `/services/posts`

**Fulfilled Requirements:**

-   Requirement #3: Efficient handling of user-generated content

**Open Issues/Problems/Risks:**

-   Potential scalability concerns with a high volume of posts

### User Management

**Purpose/Responsibility:**  
User Management oversees user-related functionalities, including registration, login, profile management, and permissions.

**Interface(s):**

-   User authentication and authorization
-   User profile data retrieval and update operations

**Quality/Performance Characteristics:**

-   Secure user authentication
-   Authorization control based on user roles

**Directory/File Location:**

-   `/services/user_management`

**Fulfilled Requirements:**

-   Requirement #4: Secure user authentication and authorization

**Open Issues/Problems/Risks:**

-   Potential vulnerabilities in the authentication process

### Third-party Integration

**Purpose/Responsibility:**  
Third-party Integration facilitates the seamless integration of external services or APIs to enhance the application's functionality.

**Interface(s):**

-   Communication with third-party APIs
-   Data exchange formats and protocols

**Quality/Performance Characteristics:**

-   Reliability of third-party service connections

**Directory/File Location:**

-   `/integrations/third_party`

**Fulfilled Requirements:**

-   Requirement #6: Integration with specified third-party services

**Open Issues/Problems/Risks:**

-   Dependency on third-party service availability

### File Storage

**Purpose/Responsibility:**  
File Storage manages the storage and retrieval of files, images, or other media within the system.

**Interface(s):**

-   File upload and download operations
-   Integration with the authentication system for secure access control

**Quality/Performance Characteristics:**

-   Scalability and efficiency in handling large files

**Directory/File Location:**

-   `/services/file_storage`

**Fulfilled Requirements:**

-   Requirement #7: Efficient file storage and retrieval

**Open Issues/Problems/Risks:**

-   Potential constraints on storage capacity

### Authentication

**Purpose/Responsibility:**  
Authentication ensures secure access to the system by verifying and validating the identity of users during login and session management.

**Interface(s):**

-   User login and logout operations
-   Integration with user management for authentication data

**Quality/Performance Characteristics:**

-   Security of user credentials
-   Session management efficiency

**Directory/File Location:**

-   `/services/authentication`

**Fulfilled Requirements:**

-   Requirement #8: Secure user authentication

**Open Issues/Problems/Risks:**

-   Potential vulnerabilities in session management

  

## Level 2
 ![Level 2](../diagrams/building_block_view_level_2.png)

**Motivation**

The motivation behind this decomposition is to achieve a modular and maintainable design that allows for the efficient handling of user-generated content. By breaking down the "Posts" building block into distinct components—PostController, PostService, and PostRepository—we aim to encapsulate specific responsibilities within well-defined boundaries.

The PostController serves as the entry point for post-related operations, handling user requests and orchestrating the flow of data between the user interface and the underlying services. The PostService encapsulates the business logic and rules associated with posts, ensuring consistency and coherence in post-related functionalities. Lastly, the PostRepository manages the data access layer, handling database interactions and ensuring the persistence and integrity of post-related data.


  | Building Block | Description                                                                                                                                                                                                                                                   |
  | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | PostController | Responsible for handling incoming requests related to posts. It processes user input, communicates with the PostService, and manages the overall flow of post-related operations.                                                                             |
  | PostService    | Manages the business logic and application-specific rules related to posts. It coordinates with the PostRepository for data retrieval and storage, ensuring proper handling of post-related operations.                                                       |
  | PostRepository | Deals with the data access layer for posts. It is responsible for database interactions, including storing, retrieving, updating, and deleting post-related data. The PostRepository communicates with the database to ensure data integrity and persistence. |

### PostController

**Purpose/Responsibility:**  
The PostController is responsible for handling incoming requests related to posts. It processes user input, communicates with the PostService, and manages the overall flow of post-related operations.

**Interface(s):**

-   User input handling
-   Communication with the PostService

**Quality/Performance Characteristics:**

-   Responsiveness in processing user requests
-   Efficiency in managing the flow of data between the user interface and PostService

**Directory/File Location:**

-   `/controllers`

**Fulfilled Requirements:**

-   Requirement #9: Efficient handling of user requests for post-related operations

**Open Issues/Problems/Risks:**

-   Potential latency issues during peak usage periods

### PostService

**Purpose/Responsibility:**  
The PostService manages the business logic and application-specific rules related to posts. It coordinates with the PostRepository for data retrieval and storage, ensuring proper handling of post-related operations.

**Interface(s):**

-   Communication with the PostController and PostRepository
-   Business logic execution for post-related functionalities

**Quality/Performance Characteristics:**

-   Consistency in enforcing business rules
-   Efficiency in coordinating data flow between PostController and PostRepository

**Directory/File Location:**

-   `/services`

**Fulfilled Requirements:**

-   Requirement #10: Consistent application of business rules for post-related functionalities

**Open Issues/Problems/Risks:**

-   Potential complexity in managing intricate business rules for diverse post operations

### PostRepository

**Purpose/Responsibility:**  
The PostRepository deals with the data access layer for posts. It is responsible for database interactions, including storing, retrieving, updating, and deleting post-related data. The PostRepository communicates with the database to ensure data integrity and persistence.

**Interface(s):**

-   Communication with the PostService
-   Database operations for post-related data (CRUD operations)

**Quality/Performance Characteristics:**

-   Data integrity and consistency in database operations
-   Efficiency in handling a large volume of post-related data

**Directory/File Location:**

-   `/repositories`

**Fulfilled Requirements:**

-   Requirement #11: Reliable storage and retrieval of post-related data

**Open Issues/Problems/Risks:**

-   Potential challenges in optimizing database queries for performance in complex scenarios



# Runtime View
arc42 Runtime Views provide a dynamic perspective on a software system's architecture, detailing the interactions, sequences, and behavior of components during runtime execution.

## Runtime Scenario 1: Third-party Integration

![Sequence Diagram Third Party Integration](../diagrams/sequence_diagram_third_party_integration.svg)

## Runtime Scenario 2: Commenting and Liking Images

![Sequence Diagram Comment and Like](../diagrams/sequence_diagram_comment_and_like.svg)

# Deployment View

The Deployment View illustrates the centralized technical infrastructure used to execute the system, focusing on Frankfurt as the single location. The system is deployed on two servers, one serving as the UI Client and the other hosting the remaining building blocks. A centralized database with a file storage bucket manages persistent data. This streamlined deployment structure simplifies management, enhances reliability, and reduces latency.

## Environments

### Development Environment

-   **Distribution and Physical Connections:**
    
    -   Developers interact with local machines and a centralized development server in Frankfurt.
-   **Justification/Motivation:**
    
    -   Facilitates collaborative development and testing.
-   **Quality/Performance Features:**
    
    -   Streamlined development and debugging cycles.

### Test Environment

-   **Distribution and Physical Connections:**
    
    -   Load-balanced servers in Frankfurt.
    -   Centralized database with file storage.
-   **Justification/Motivation:**
    
    -   Mirrors the production environment for realistic testing.
    -   Simplifies quality assurance processes.
-   **Quality/Performance Features:**
    
    -   Real-world testing scenarios.
    -   Comprehensive quality assurance.

### Production Environment

-   **Distribution and Physical Connections:**
    
    -   Centralized servers in Frankfurt.
    -   Centralized database with file storage.
-   **Justification/Motivation:**
    
    -   Maximizes availability, scalability, and reliability.
    -   Reduces latency for an enhanced user experience.
-   **Quality/Performance Features:**
    
    -   High availability and reliability.
    -   Optimized performance through centralized deployment.

## Infrastructure Level 1

![Infrastructure overview digram](../diagrams/infrastructure_level1_overview.svg)

### Overview

The Infrastructure Level 1 details the centralized deployment of the system in Frankfurt, emphasizing quality, performance, and the mapping of building blocks.

### Development Environment

-   **Distribution:**
    
    -   Local machines for developers.
    -   Centralized development server in Frankfurt.
-   **Justification/Motivation:**
    
    -   Enables collaborative development and testing.
-   **Quality/Performance Features:**
    
    -   Streamlined development and debugging.
-   **Mapping of Building Blocks:**
    
    -   UI Client, Search, Posts, User Management, Third-party Integration, Authentication, File Storage, PostController, PostService, PostRepository on the development server.

### Test Environment

-   **Distribution:**
    
    -   Load-balanced servers in Frankfurt.
    -   Centralized database with file storage.
-   **Justification/Motivation:**
    
    -   Mirrors the production environment for realistic testing.
    -   Simplifies quality assurance processes.
-   **Quality/Performance Features:**
    
    -   Real-world testing scenarios.
    -   Comprehensive quality assurance.
-   **Mapping of Building Blocks:**
    
    -   All building blocks on load-balanced servers with a centralized database.

### Production Environment

-   **Distribution:**
    
    -   Centralized servers in Frankfurt.
    -   Centralized database with file storage.
-   **Justification/Motivation:**
    
    -   Maximizes availability, scalability, and reliability.
    -   Reduces latency for an enhanced user experience.
-   **Quality/Performance Features:**
    
    -   High availability and reliability.
    -   Optimized performance through centralized deployment.
-   **Mapping of Building Blocks:**
    
    -   All building blocks on centralized servers with a centralized database.

## Infrastructure Level 2

### Servers

**Diagram:**

![Infrastructure overview digram](../diagrams/infrastructure_level2_servers.svg)

**Explanation:** The internal structure of servers involves multiple components:

-   **Load Balancers:**
    
    -   Responsible for distributing incoming requests among application servers.
    -   Ensures optimal performance and reliability.
-   **Application Servers:**
    
    -   Host various building blocks, including UI Client, Search, and Posts.
    -   Allows for efficient load distribution and independent scaling of components.
-   **Database Server:**
    
    -   Manages data storage and retrieval for User Management, Authentication, Posts, and File Storage.
    -   Facilitates efficient communication between the application layer and the data access layer.

### Databases

**Diagram:**

![Infrastructure overview digram](../diagrams/infrastrucutre_level2_databases.svg)

**Explanation:** The internal structure of databases comprises multiple layers:

-   **Data Access Layer:**
    
    -   Handled by PostRepository, facilitating communication with the application layer.
    -   Ensures reliable storage and retrieval of post-related data.
-   **Query Processing and Indexing:**
    
    -   Enhances search accuracy and response time in the Search component.
    -   Optimizes the retrieval of relevant information from the database.
-   **File Storage Layer:**
    
    -   Manages integration with the authentication system for secure access control.
    -   Ensures efficient and secure storage and retrieval of files within the system.

### Cloud Network

**Diagram:**

![Infrastructure overview digram](../diagrams/infrastrucutre_level2_cloud.svg)

**Explanation:** The internal structure of the Cloud Network involves communication channels between building blocks and secure connections to third-party services:

-   **Communication Channels:**
    
    -   Enable seamless data flow between building blocks.
    -   Facilitate efficient interactions and data exchange within the system.
-   **Integration with Third-party Services:**
    
    -   Orchestrated through well-defined protocols and data exchange formats.
    -   Ensures reliable and secure connections, enhancing collaboration with external services.
    
# Cross-cutting Concepts

## REST API

to enable consistent communication between the client and the server, we will use a REST API. This will allow us to use the same endpoints for all platforms and also makes it easier to implement the backend. 

## Image format (PNG)

To simplify the handling of images in general, all images will be converted to the PNG format. This will allow us to use the same image format for all images and also makes it easier to implement the image editing feature.

## Security and Privacy

All data that is not public will be stored and send e2e encrypted. This includes the user data, images and all other data that is not public. This will ensure that no one can access the data without the permission of the user.

## Common logging format
We will use a common logging format for all layers of our application and collect them in a single logging analyzation tool. This will allow us to easily analyze the logs and find errors.

# Architecture Decisions

## Multiplatform App
Date: 23.11.2023
### Context
We want to have our application available on all major platforms, including Android, iOS and Web.
### Decision
We will use Flutter to develop our application, as it allows us to develop a single codebase for all platforms.
### Status
Accepted
### Consequences
There will be a single codebase and also one UI/UX design for all patforms.
If we need to implement a feature that is not supported by Flutter, we will need to implement it natively for each platform.

## Scalable platform
Date: 23.11.2023
### Context
We want our application to be able to handle a large amount of users.
### Decision
We will use a horizontally scalable platform using Node.js.
### Status
Accepted
### Consequences
We still need to keep the scalability of the whole application in mind. The application must support multiple containers to be able to scale horizontally.

## Basic architectural approach
Date: 23.11.2023
### Context
We need to decide on a basic architectural approach for our application.
### Decision
We will use a client/server architecture.
### Status
Accepted
### Consequences
We need to make sure that the communication between the client and the server is secure and that the server is able to handle a large amount of requests (see scalable platform).

# Quality Requirements

Security:

-   User data, including images and personal information, must be encrypted during transmission and storage
-   The app should comply with industry standards for data protection and privacy regulations

Reliability:

-   The app should be available for use 99.9% of the time to ensure a reliable user experience
-   In case of downtime or maintenance, users should be notified in advance, and the duration of downtime should be minimized

Usability:

-   The image posting process takes less than 30 seconds
-   The account creation process takes less than 2 minutes

Compliance:

-   The software adheres to DSGVO (Datenschutz-Grundverordnung), ensuring compliance with data protection regulations
-   If the user wishes to initiate a removal request, it should be carried out in less than 24 hours

Maintainability:

-   The code coverage exceeds 80%, and the documentation surpasses 90%
-   Every code change must undergo a review

Compatibility:

-   The app should be compatible with the latest versions of iOS and Android operating systems
-   It should support a range of devices and screen sizes to cater to a diverse user base
    
## Quality Tree

![Quality Tree](../diagrams/quality_tree.svg)

## Quality Scenarios

### Security: Data Encryption

Context:
-   A user uploads a private image to the app

Problem:
-   Ensure that the image, along with any personal data, is transmitted and stored securely through encryption mechanisms.

Solution:
-   Implement end-to-end encryption for data transmission, utilizing industry-standard encryption algorithms.
-   Employ encryption for stored images and user information in the database.
  
Consequences:
-   User data, including images, remains confidential and secure, meeting privacy and security standards
  
### Reliability: Availability during Peak Usage

Context:
-   A significant number of users access the app simultaneously during peak hours.

Problem:
-   Ensure the app remains available and responsive under high user load.

Solution:
-   Implement auto-scaling mechanisms to dynamically allocate resources based on demand.
-   Optimize database queries and image loading processes for efficient performance.

Consequences:
-   The app maintains stability and responsiveness during peak usage, preventing downtime and ensuring a reliable user experience.
  
### Usability: User Onboarding

Context:
-   A new user creates an account and navigates through basic features.

Problem:
-   Evaluate the onboarding process for simplicity and clarity, ensuring users can easily understand and use essential functionalities.

Solution:
-   Provide a guided onboarding experience with clear instructions for account creation, image sharing, and profile setup.

Consequences:
-   New users can quickly adapt to the app, leading to higher user satisfaction and engagement.

# Risks and Technical Debts

* Image editing might be a complex topic
  * None of us is experienced with editing of images, so we might need to do some trainings on this topic or even consult a professional to get this right. Another option would be to implement this feature later on.
* Content filtering
  * We need to think about how we can make sure that no nsfw or even illegal content is posted and can be removed immediately. One option would be to use AI Image detection to filter images with a high risk.
* Disk space
  * As everyone can upload images on our platform, we might need to figure out limits for the space people can use.

# Glossary

| Term                        | Definition                                                               |
| --------------------------- | ------------------------------------------------------------------------ |
| Image Sharing App           |A platform for users to upload, edit, and share images                    |
| Pixlr Integration           | Seamlessly incorporating Pixlr's image editing service into the app      |
| RESTful Architecture        | A scalable design using standard HTTP methods for networked applications |
| User-generated Content      | Content created by app users, including images and posts                 |
| Node.js                     | JavaScript runtime for scalable server-side applications                 |
| End-to-End Encryption (e2e) | Ensures secure transmission and storage of user data                     |
| Flutter Framework           | Cross-platform toolkit for unified codebase development                  |
| UI Client                   | Front-end interface handling user interaction                            |
| Security and Privacy        | Measures to protect user data and ensure privacy compliance              |
| Common Logging Format       | Standardized log format for systematic analysis and error detection      | 