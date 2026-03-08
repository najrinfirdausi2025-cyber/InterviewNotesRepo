https://www.geeksforgeeks.org/system-design/unified-modeling-language-uml-introduction/

# Unified Modeling Language (UML) Diagrams
`Unified Modeling Language (UML) is a general-purpose modeling language.`
- The main aim of UML is to define a standard way to visualize the way a system and documenting Software Detail Architeture Design has been designed. 
- It is quite similar to blueprints used in other fields of engineering. UML is not a programming language, it is rather a visual language.

- We use UML diagrams to show the behavior and structure of a system.
- UML helps software engineers, businessmen, and system architects with modeling, design, and analysis.

__Need of UML:__

- Provides a clear visual communication language for collaboration across multiple teams in complex projects.
- Helps non-technical stakeholders (business users, managers) understand system requirements and functionality without reading code.
- Saves development time by allowing teams to visualize workflows, interactions, and system structure early.
- Essential for large-scale systems where tracking thousands of classes and objects becomes difficult.
- Enables early detection of design problems like high coupling, excessive dependencies, and circular references.
- Supports major methodologies like Agile and Waterfall by enabling iterative and incremental system design.
- Works for many domains — e.g., banking, inventory, enterprise, and web applications.
- Improves team collaboration by giving everyone a common modeling language independent of programming language.
- Helps teams understand the complete system architecture and functionality, reducing future errors.
- UML diagrams are categorized into Structural diagrams (system components) and Behavioral diagrams (system behavior & interactions).


## Types of UML Diagrams
- UML is linked with object-oriented design and analysis. UML makes use of elements and forms associations between them to form diagrams. Diagrams in UML can be broadly classified as:-
     
     - 1. Structural Modeling
     - 2. Behavioral Modeling

### Structural Modeling
Structural modeling captures the static features of a system. They consist of the following −
```
Classes diagrams
Objects diagrams
Deployment diagrams
Package diagrams
Component diagram
```
- Structural model represents the framework for the system and this framework is the place where all other components exist.
- Hence, the class diagram, component diagram and deployment diagrams are part of structural modeling. They all represent the elements and the mechanism to assemble them.
- The structural model never describes the dynamic or Run-TIME behavior of the system. Class diagram is the most widely used structural diagram.

### Behavioral Modeling
Behavioral model describes the interaction in the system. It represents the interaction among the structural diagrams. Behavioral modeling shows the dynamic nature of the system. They consist of the following −

```
Activity diagrams
Interaction diagrams
Use case diagrams
```
All the above show the dynamic sequence of flow in a system.


<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/8ff30a0a-4470-476e-9ab9-9facec4a57c6" />

### Type 1: Class diagrams

__Member access modifiers:__
- All classes have different access levels depending on the access modifier (visibility). Here are the access levels with their corresponding symbols:

- Public (+)
- Private (-)
- Protected (#)
- Package (~)
- Derived (/)
- Static (underlined)

<img width="313" height="183" alt="image" src="https://github.com/user-attachments/assets/f16ba44c-73c4-4591-97b4-8a29080a7958" />
<img width="1700" height="925" alt="image" src="https://github.com/user-attachments/assets/bfba5ef0-4531-4212-81cf-d2aff231bcd7" />
<img width="1001" height="501" alt="image" src="https://github.com/user-attachments/assets/6599673a-9157-4483-8e26-c96816eb2338" />

### Abstract Class UML
<img width="1100" height="328" alt="image" src="https://github.com/user-attachments/assets/e0eb01b0-fa4e-450e-927b-4a25313513f2" />

### Interface UML
<img width="1100" height="408" alt="image" src="https://github.com/user-attachments/assets/70e82e8f-ad21-4cb5-b100-afecc507248c" />


###  Type 2 : Relationships:

<img width="1267" height="950" alt="image" src="https://github.com/user-attachments/assets/573d5163-b8a7-404f-bf4e-eed3e9e6c0c9" />

<img width="1700" height="1411" alt="image" src="https://github.com/user-attachments/assets/5b61ea1e-a098-4bfb-8886-215db1689fde" />

- `Associations:` Associations in a UML Class Diagram are relationships between classes. A solid line between classes is used to represent them. Associations are often labeled with a verb or verb phrase that matches the problem area in the real world.

- `Generalization or inheritance:` A taxonomic link between a broader and a more particular classifier is referred to as an inheritance or generalization. Each classifier instance is also an indirect instance of the general classifier. As a result, the particular classifier inherits the characteristics of the more general classifier. It symbolizes an "is-a" relationship.

- `Aggregation:` The construction of a specific class as a result of one class being aggregated or formed as a collection is referred to as aggregation. The class "library," for example, consists of one or more books, among other items. The included classes in aggregate are not heavily dependent on the container's lifespan. To depict aggregation in a diagram, draw a line from the parent class to the child class with a diamond shape near the parent class.

- `Composition:` The composition relationship and the aggregation connection are extremely similar. The main distinction is that it emphasizes the contained class's reliance on the life cycle of the container class. That is, when the container class is destroyed, the enclosed class is eliminated. A bag's side pocket, for example, will no longer exist after the bag is destroyed.

-`Realisation:` The implementation of functionality defined in one class by another class is referred to as realization. In UML, a broken line with an unfilled solid arrowhead is sketched from the class that defines the functionality to the class that implements the function to demonstrate the relationship. 

- `Dependency:` In the code of a method, an object of one class may use an object of another class. If the object is not kept in any field, the relationship is portrayed as a dependency.

- `Cardinality:` Cardinality is expressed as one-to-one, one-to-many, or many-to-many relationships.


<img width="1700" height="1243" alt="image" src="https://github.com/user-attachments/assets/1e2b8ddf-767e-4c8e-90ac-69d52791e95d" />

### Example
<img width="1700" height="2276" alt="image" src="https://github.com/user-attachments/assets/6cac9ce2-c920-4381-96cf-e5f6678cf24d" />


###  Type 3: Object Diagram:

<img width="961" height="745" alt="image" src="https://github.com/user-attachments/assets/bd170abc-b9b8-42e1-bf53-f3c7afd437e2" />


### Type 4: Component Diagram

<img width="948" height="867" alt="image" src="https://github.com/user-attachments/assets/f76440d5-d342-4dff-9164-66d40cf44990" />

### Type 5: Composite structure diagrams
<img width="1030" height="645" alt="image" src="https://github.com/user-attachments/assets/593d32a3-d727-4af7-be89-4b7f08c6a2d4" />

###  Type 6: Package Diagram:
<img width="951" height="677" alt="image" src="https://github.com/user-attachments/assets/17be6ee2-e071-4d0c-967b-891de0e9b653" />
<img width="1440" height="850" alt="image" src="https://github.com/user-attachments/assets/eeb887bd-6be1-4f43-919b-9e440f9384d0" />

###  Type 7: Deployment Diagram

<img width="965" height="645" alt="image" src="https://github.com/user-attachments/assets/262bd5d2-b8d6-42f1-98a6-5b98260144bc" />
<img width="479" height="417" alt="image" src="https://github.com/user-attachments/assets/221ddab8-b4bc-4b07-aadc-3f380c6ddb28" />


###  Type 8: Use Case UML diagram:

<img width="949" height="680" alt="image" src="https://github.com/user-attachments/assets/2a06e6ab-6a5f-48b8-8986-ca7665b09849" />
<img width="446" height="323" alt="image" src="https://github.com/user-attachments/assets/dd760d87-5877-420c-bbc3-71a040b92ccd" />
<img width="1440" height="850" alt="image" src="https://github.com/user-attachments/assets/402c6ded-92d3-49e5-b419-6fc61481f1a1" />

###  Type 9: User Activity Diagram:
<img width="952" height="738" alt="image" src="https://github.com/user-attachments/assets/749df185-aa09-4ac6-b0be-2075de074113" />


### Type 10: Communication Diagram
<img width="1042" height="746" alt="image" src="https://github.com/user-attachments/assets/870484d2-82b2-42dd-a446-d0697dc74148" />

### Type 11: Sequence diagram

<img width="1029" height="949" alt="image" src="https://github.com/user-attachments/assets/bc7fff98-5c84-45b7-be82-518c4ce67737" />
<img width="965" height="698" alt="image" src="https://github.com/user-attachments/assets/8b415f25-0324-4947-8ee2-911bf9da549e" />

###  Type 12: State Machine Diagrams/  State-chart Diagrams:

<img width="946" height="678" alt="image" src="https://github.com/user-attachments/assets/8a6ddd24-ee2c-493c-b6a6-699c77c53bfe" />

<img width="958" height="416" alt="image" src="https://github.com/user-attachments/assets/ac708568-0814-45b6-9049-8867a5a6fb59" />
