# SP3-Store-Systemer: MyDRTV Solution Architecture Report

## Introduction
This report presents the proposed solution architecture and technology stack for the MyDRTV project, a digital transformation initiative for Denmark’s state broadcaster. The platform aims to promote Danish TV and film globally by offering access to a vast collection of old TV programs and films. Key features include user ratings, advanced search, personalized recommendations, and GDPR-compliant user interaction.

The report outlines our systematic approach to selecting the technology stack and architecture, comparing different architectural styles like layered and microservices. The architecture design will be supported by diagrams, including use case, domain model, and sequence diagrams.

## Project Overview

### Objective
The MyDRTV platform is designed to provide:
- Access to a global audience for Danish TV and films.
- User accounts with rating and interaction features.
- Advanced search capabilities based on year, title, genre, and other filters.
- Personalized recommendations through a "More Programs You May Like" feature.
- High availability and compliance with GDPR for handling personally identifiable information (PII).

### Key Functional Requirements
- **User Interaction:** Account creation, ratings, and conversations on TV programs and films.
- **Search System:** Advanced search using multiple filters such as year of production, title, and genre.
- **Personalization:** A recommendation system based on user ratings and interaction.
- **High Availability:** Ensuring uninterrupted global access to content.
- **GDPR Compliance:** Secure handling of PII with compliance to European regulations.

## Architectural Approach

### Architectural Styles Comparison
We considered multiple architectural styles for the MyDRTV project. Below is a summary of the criteria used in our comparison: 

## Technology Stack

- **Frontend:** Typescript React. This choice was made over Javascript because we while we prefer a strongly typed language we also feel it provides better tooling than Javascript. React was chosen as our design library because of how dynamic it makes coding applications, because of our familiarity with the technology. Also out of the box, TypeScript supports JSX and which allows us to get the full React Web support that we want.

- **Backend:** We chose C# because it's object-oriented and utilizes .NET which provides access to Entity Framework (EF). EF is an object-relational mapper (ORM) that simplifies performing CRUD operations on a relational database. While other programming langauges also offer the use of ORMs, such as JPA for Java, We prefer EF for its ease of use and intuitive design.

- **Database:** We believe PostgreSQL is a suitable choice because it is a relational database and we find it simple to use, Postgres is also known for its scalability and ability to handle large-scale data. It also offers JSON support giving us the flexibility we want combined with a decent community support, making this a dependable choice for managing our data needs we'd say.

- **Search Engine:** PostgreSQL already has a built-in full-text search engine, which we plan to use to use for the streaming service. It allows efficient searching throuhg large vollumes of text data, such as movie titles, metadata etc. Supports advanced phrase searching, ranking results by relevance, and filtering by specific fields, which will help users find content accurately and quickly. But if our choice turns out to not be efficient enough we'll explore building a custom search engine that suites our needs. One optimized for movie recommendations or real-time search results.

- **Recommendation Engine:** We will implement an machine learning algorithm that would use these factors for the recommendations:
    - The interactions the user has with the service ( such as viewing history and how they rated other titles),
    - Other members with similar tastes and preferences on our service, and
    - Informaiton about the titles, such as their genre, categories, actors, release year, etc.

    In addition to knowing what they have watches on MyDRTV, to best personalize the recommendations we also consider factors including:

    - the time of day they're watching
    - the languages your prefer
    - the device they're watching on, and
    - how long they've enjoyed a title.

- **Infrastructure:** We will use AWS for our infratructure. Utilizing their RDS to host the database and EKS to host pods of the front- and backend. Kubernetes will also ensure that the application experiences minimal to no down time. AWS was chosen based on our previous exeperience with the platform. 

## System Design

### Subsystems Overview (Bounded Contexts in Domain-Driven Design)
The system will be decomposed into the following bounded contexts:
1. **User Management:** Responsible for user accounts, authentication, and handling GDPR compliance.
2. **Ratings & Interactions:** Manages ratings, comments, and recommendations.
3. **Search & Content Delivery:** Provides advanced search functionality and efficient content delivery.
4. **Recommendation Engine:** Delivers personalized recommendations based on user preferences and interactions.

### Key Diagrams
- **Use Case Diagram:** Shows the main interactions between users and the system.
- **Domain Model:** Visualizes the main business concepts (e.g., User, Program, Rating).
- **Sequence Diagram:** Describes interactions between subsystems, such as how user ratings impact recommendations.

## Non-Functional Requirements

### High Availability
- **Redundancy & Failover:** Cloud infrastructure with auto-scaling and load balancing will ensure 99.9% uptime.
- **Scalability**

### Security & GDPR Compliance
- **Data Protection:** User PII will be encrypted and stored securely. Regular audits and compliance checks will ensure GDPR adherence.
- **User Privacy:** Clear user consent for data processing, with tools for data anonymization and deletion upon request.

### Performance
- **Response Time:** The system will be optimized for minimal latency, especially for content search and personalized recommendations.
- **Load Balancing:** Advanced load balancing will ensure consistent performance during peak times.

## Risk Management

### Reputational Risk
- A robust ratings system is critical for user trust and engagement. The architecture ensures accuracy and fairness in ratings and recommendations.

### Legal and Compliance Risks
- GDPR compliance is non-negotiable. Mismanagement of PII could lead to severe legal repercussions and loss of user trust. Security audits and compliance checks will be a regular part of the development cycle.

## Conclusion


