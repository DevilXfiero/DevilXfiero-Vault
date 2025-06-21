
1. Observe the system
2. Determine the objects
3. Establish relationships between objects
4. Model and build the design


## Unified Modeling Language (UML)

This building block itself is divided into the following various types:

- Structural things
- Behavioural things
- Grouping things
- Annotation things

## Class Diagram

**Class diagrams** are used to depict the system's static perspective. They are used in the design process to show the shared roles and responsibilities of the entities that produce the behavior of the system.

### Class notation

![[Pasted image 20241005193243.png]]

### Interface, abstract class, and enumeration

![[Pasted image 20241005193407.png]]

### Access Modifiers
![[Pasted image 20241005193537.png]]

### Association

The association can be divided into two categories:

- Class association (Inheritance)
- Object association

Class Association
- Inheritance

![[Pasted image 20241005193653.png]]


### Object association

Object association (relationship between objects) can be divided into the following categories:

  1. Simple association
  2. Composition
  3. Aggregation

#### Simple association

The weakest connections between objects are made through **simple association**.
![[Pasted image 20241005193846.png]]


#### Aggregation

**Aggregation** describes the relationship between the container and the object it contains. An object may contain an aggregate of another object. Aggregation is denoted by a line with an unfilled diamond head towards the container.

Aggregation is a _weaker_ relationship because:

- Aggregate objects are not a part of the container.
- Aggregate objects can exist independently.
![[Pasted image 20241005194015.png]]


#### Composition


Composition is a _strong_ relationship because:

- The composed object becomes a part of the composer.
- Composed objects can not exist independently.


![[Pasted image 20241005194201.png]]

## Dependency

**Dependency** indicates that one class is dependent on another class(es) for its implementation. Another class may or may not depend on the first class. A dashed arrow denotes dependency.
![[Pasted image 20241005194338.png]]
