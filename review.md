#Software Engineering (CSC 510)

__Agile__ is an improvement over waterfall. Continuous integration, test first programming, etc.

- __Individuals and interactions__ over processes and tools
- __Working software__ over comprehensive documentation
- __Customer collaboration__ over contract negotiation
- __Responding to change__ over following a plan

###Design:
- __UML__ (Unified Modeling Language) 
- __Wireframe__ is a view schematic that captures all layout and content decisions of that view (*Balsamiq*).
- __Storyboard__ illustrates the timeline of user performing a task as a sequence of frames.

#####Design process:

- Idea Generation. What is the problem? What is the user trying to do? 
- Screening. Why is this a problem? What are competitors doing?
- Design Specification. What patterns can we use? What is core product concept (sketches)?
- Feasibility. What would be first step? What are core technologies to leverage?
- Feedback. What does users say?  What do peers say?

###Architectural Design 
#####Goals:

- Skeleton of system, repositories for designs (Templates for programmers to build systems).
- Concepts and constraints (Provide framework for how components interact).
- Stakeholder communication (Abstract enough to explain to non-experts).

#####System Requirements Affect Architecture:

- Performance
- Security
- Safety
- Availability / Replicability
- Maintainability

#####An architectural pattern consists of:

- a set of component types (e.g. process, procedure) that perform some function at runtime.
- a topological layout of the components showing their runtime relationships.
- a set of connectors (e.g. data streams, sockets) that mediate communication among components.

####Data Centered Patterns:
When a system can be described as a centralized data store that communicates with a number of clients.

- (+) Easy to administer.
- (–) Hard to track down errors/dependencies.

#####Repository Model (pull)
Components must exchange information so they can work together effectively.<br>
Data held in central database that is accessible by all components.

- Components write data in the repository
- Components read data from the repository
- (+) Easy to implement as a whole
- (–) Clients may become complex when polling

#####Blackboard Model (push)
Three components: Knowledge sources, Blackboard, Control component. 

- Components register data subscription
- Components are notified when data is available
– (-) Infrastructure complex
- (+) Client programming is simplified

####Call and Return Patterns
Typical control flow imposed by modern programming languages.

- (+) Easy to reason about behavior from static code
- (–) Sometimes not flexible enough

#####Main and Subprogram
- (+) Easy to program
- (+) Easy to understand
- (–) Performance can suffer without multiple threads
- (–) Can be hard to extend

#####Object-Oriented
- (+) Well defined interfaces
- (–) Interface changes break all users of a particular class
- (–) Multiple threads may contend for access to object data

#####Layered Model
- (+) Easy to extend system by inserting new layer which provides same interface
- (–) Structuring layers can be difficult as layers may require services of non-adjacent layers
- (–) Performance can suffer since requests must pass through many layers

####Data Flow Pattern
Architectural pattern for stream processing.<br>
Every component defines a processing/computational step.<br>
Data flows through components and connections.

- (+) Supports easy reuse of components
- (+) Fairly easy to reason about (composition)
- (+) Easy to maintain by adding components
- (–) Some component may have to wait for the output of the previous pipe to finish
- (–) Sometimes difficult to maintain correspondences between separate streams


#####Pipe-And-Filter
- Components (Filters)
	- Set of inputs and outputs
	- Local transformation
- Connectors (Pipes)
	- Facilitate data flow
- Constraints
	- Do not share state
	- Have no knowledge of other filters

#####Batch Sequential
Each component completes transformation of input before passing to output.<br>
A degenerate case of pipe-and-filter where no streaming occurs.

####Event System
Execution is controlled by events; a packet coming in, a button being clicked, etc…

####Design Pattern
- Creational <br>
Concerned with the process of object creation.

- Structural <br>
Deal with the composition of classes or objects.

- Behavioral <br>
Characterize the ways in which classes or objects interact and distribute responsibility.

#####Singleton Pattern
- Intent
	- To ensure that a class has only one instance and provide a global point of access to it.
- Applicability
	- Use when there must be exactly one instance of a class, and it must be accessible to clients from a well-known access point.
- Benefits
	- Provider controls access to sole instance
	- Permits a variable number of instances later
	- Reduced name space (avoids polluting the name space with global variables)

#####Visitor Pattern
- Allows operations to be performed on data structures without knowledge of transversal.
- Used on complex data structures such as graphs or trees.

#####Builder Pattern
- Separates object construction from its representation. 
- Construction processes can create different representations.

#####Abstract Factory Pattern
- Abstract creation of a family of objects
- Use the Abstract Factory pattern when
	- need to maintain parallel families of objects but hide from client.
	- you want to localize the knowledge object creation

####API principle
- Do one thing well
- Implementation should not impact API
- Minimize accessibility of EVERYTHING
- Names Matter
- Don’t make the client do something the API could easily do

####Frameworks
Frameworks are domain-specific design made up of a collection of abstract and concrete classes and the interfaces between them.
#####Type:
- White-box framework
- black-box framework

#####Rule of three:
- Take 3 applications in same domain.
- Refactor duplicated code into common components.
- Identify common concepts and abstract as framework.

#####Dependency Injection Roles
- Service object, Client object, Interfaces, Injector.
- Pros
	- Configurable and isolated client
	- Configurations in external files (annotations also possible)
	- Changes without recompilation
	- Different configurations for different scenarios (testing)
- Cons
	- Clients demand config details in construction code
	- Hard to trace code 
	- Explosion of types
	- Complexity moved to links between classes

####REST verbs
- POST (create)
- GET (read)
- PUT (update)
- DELETE (delete)

####Types of Testing
#####Unit Testing
Goal: Confirm that the component or subsystem is correctly coded and carries out the intended functionality
#####Integration Testing
Goal:  Test the interfaces among the subsystems.
#####System Testing
Goal:  Determine if the system meets the requirements (functional and nonfunctional)
#####Acceptance Testing
Goal: Demonstrate that the system meets the requirements and is ready to use.

####Styles of Testing
- black box testing
- white box testing

####Code Metrics
- Lines of code
- Halstead Complexity: Number of operations and symbols in code.
- Cyclomatic Complexity: Number of independent paths in program.
- Dep Degree: Number of data flow paths in code.

####OO Metrics
- Weighted Methods Per Class

####Configuration Management 
#####Traditional SCM Process
- Identify all items related to software.
- Manage changes to those items.
- Enable variations of items and changes. 
- Maintain quality of versions and releases.
- Provide traceability between changes and requirements.

#####Modern SCM Process
- In traditional configuration management, the process is not fully triggered until deployment.
- In modern configuration management, lightweight CM is integrated throughout the  software process.

####Continuous Deployment
#####Continuous Integration
- A practice where developers automatically build, test, and analyze a software change in response to every software change committed to the source repository.

#####Continuous Delivery
- A practice that ensures that a software change can be delivered and ready for use by a customer by testing in production-like environments.

#####Continuous Deployment
- A practice where incremental software changes are automatically tested, vetted, and deployed to production environments.

#####Dark Launches
- A strategy to release software without any user-facing elements exposed.
- Can help eliminate the need to support long-running release branch. Reduces merge issues.
- Collect performance data, stabilize feature。

#####Big Flip
- Start with two identical infrastructure. Slowly build up second. Switch.
- Can support “stress-free” deployment and preparation of “blue environment”.
- Extra cost in infrastructure overhead.
- Data migration issues (switch cost might be high if migration slow and not mirrored).

#####Canary Releasing
- Benefits:
	- Rolling back is easy, stop routing users.
	- Can combine with A/B testing
	- Can check if meeting capacity requirements by gradually ramping up load.
- Issues:
	- Deployment to client installed computers.
	- Any shared resource (cache, services) need to work will all versions in production.
	- May be supporting multiple versions in production.

####Infrasturcture
- DNS Services
- Load Balancing
- Content Delivery
	- Don’t waste CPU, sockets, and worker threads on static requests.
	- For example: JS library, CSS, images, videos, popular objects.
- Caches
- Availability Zones
- Regions(Geographically)



