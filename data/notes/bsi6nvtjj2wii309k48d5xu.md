
> https://www.workingsoftware.dev/software-architecture-documentation-the-ultimate-guide/  
> https://arc42.org/download

This guide shows you how to write, structure, visualize and manage software architecture documentation in a lean way using appropriate documentation tools.

The [C4 model](https://c4model.com/) and the [arc42](https://www.arc42.de/) template will help you write a good software architecture documentation. This guide shows you how.

**Table of Contents**

- [Why should we document software architecture?](https://www.workingsoftware.dev/software-architecture-documentation-the-ultimate-guide/#why-should-we-document-software-architecture)
- [How should we structure software architecture documentation?](https://www.workingsoftware.dev/software-architecture-documentation-the-ultimate-guide/#how-should-we-structure-software-architecture-documentation)
- [How should we visualize software architecture?](https://www.workingsoftware.dev/software-architecture-documentation-the-ultimate-guide/#how-should-we-visualize-the-software-architecture)
- [How do we write and manage software architecture documentation?](https://www.workingsoftware.dev/software-architecture-documentation-the-ultimate-guide/#how-do-we-write-and-manage-software-architecture-documentation)

## Why should we document software architecture?

An often expressed opinion about software architecture documentation in "agile" teams is:

> The code documents the system. We don't need any further documentation.

But this statement is only half the truth. There are several questions that remain unanswered in the code.

- What are the goals of the system?
- What are the non-functional requirements?
- What are the architectural decisions and their arguments?
- ...

As [Simon Brown](https://simonbrown.je/) has correctly pointed out:

> The code doesn't tell the whole story.

Long story short: You should document the software architecture of your system. Take a look at the **goals** you should fulfil with your documentation, and you'll understand **why**.

Blog Post: Technical debt due to lack of documentation

> [Technical Debt Scenario #5: The code documents the system.](https://www.workingsoftware.dev/technical-debt-scenario-5-the-code-documents-the-system/) - Unfortunately, several long-time developers have left the product team. In addition, there is virtually no technical documentation for the system. Even the architectural decisions are no longer traceable. What would you do to eliminate this kind of technical debt?

### Goals of software architecture documentation

There are three goals that your software architecture documentation should fulfil.

> **Software architecture documentation creates a common understanding**

Software architecture documentation should at least support the development team, for example, when a new team member starts.

Let's take the onboarding example, a new team member has a lot of questions:

- Where can I find an overview of the system's building blocks?
- Why are you using [Angular](https://angular.io/) and not [React](https://reactjs.org/)? Why are you using [Hibernate](https://hibernate.org/) and not [jOOQ](https://www.jooq.org/)?
- Where and how is the system deployed?
- Are there any conventions I need to be aware of?

This brings us to the first goal of software architecture documentation:

**Software architecture documentation creates a common understanding of the solution behind the system for various stakeholders**

There are usually many different stakeholders interested in different aspects of our system: Software Architects, Software Engineers, Ops, Support, Testing, POs, Project Managers, SMEs, Business Sponsors and so on.

You can create different views of your system's architecture by developing a common understanding of your system's software architecture.

With this understanding, the various stakeholders can evaluate the underlying software architecture from their perspective.

In this way, we can concretize the goal described above with the evaluation part:

**The documentation makes it possible to evaluate the software architecture from the perspective of the various stakeholders**

Software architecture documentation allows your stakeholders to judge whether the system is achieving the goal, since they often can't dive into the code.

With good architecture documentation, they can answer the following questions:

- Does the chosen architecture fit the solution?
- Is the architecture appropriate?

In this way, architectural documentation often prevents other goals, constraints, and non-functional requirements from creeping in.

Let me give a practical example here.

I've often heard from various stakeholders: "_The system must be fast_."

But what does that mean?

As a software architect, you have to turn these expectations into concrete quality goals, i.e., non-functional requirements with supporting quality scenarios. You record these quality goals in the architecture documentation, which in turn helps your team to implement the solution with the agreed non-functional requirements.

> Software architecture documentation supports architectural work

**Software architecture documentation supports team work**

Software architecture is a team effort, so it's most important that the software architecture documentation supports your team effort.

See also this article about the role of the software architect

> [Do we need a software architect in our agile team?](https://www.workingsoftware.dev/do-we-need-a-software-architect-in-our-agile-team/) - This question often comes up in agile teams. In this blog post, we look for the answer to this question in the context of the various agile and organisational frameworks like Scrum, LeSS, SAFe, Disciplined Agile and draw a conclusion.

As a team member, it's important to actively know (and pass on to new team members) the goals, constraints, and non-functional requirements within the team. This information is often very important in team architecture workshops.

It's important to make understandable and comprehensible architecture decisions. Nothing is more annoying than not knowing why you decided the way you did.

> Software architecture documentation guides the development team in implementing new product features

Documenting software architecture helps the entire development team implement the solution.

- What _constraints_ do I need to consider?
- Which _non-functional_ requirements do I need to test?
- Which _overarching_ concepts do I need to follow?
- Are there architectural decisions I need to consider when implementing a particular feature?

**Software architecture documentation supports the communication with external stakeholders**

A large part of software architecture work is communication. In particular, communication with stakeholders is key to effective and focused discussion outcomes.

Good software architecture documentation supports communication with external stakeholders. It contains different and stakeholder-appropriate views of the software architecture.

### How should we structure software architecture documentation?

An proven approach to structuring software architecture documentation is the [arc42 template](https://arc42.org/).

### What is the arc42 template?

- [arc42](https://arc42.org/) provides a template for documenting and communicating software  
   and system architectures.
- [arc42](https://arc42.org/) is based on practical experience of many systems in various domains,  
   from information and web systems, real-time and embedded to business  
   intelligence and data warehouses.
- [arc42](https://arc42.org/) supports arbitrary technologies and tools.
- [arc42](https://arc42.org/) is completely process independent and is particularly well suited for lean and agile development approaches.
- [arc42](https://arc42.org/) is open source and can be used free of charge in both the commercial and private sectors.
- [arc42](https://arc42.org/) is available in several languages.
- [arc42](https://arc42.org/) is available in different formats like .adoc, .docx, .rst, .md, .tex, ...

GitHub Repository of the arc42 Template

> [GitHub - arc42/arc42-template: arc42 - the template for software architecture documentation and communication](https://github.com/arc42/arc42-template) - the template for software architecture documentation and communication

### How is the Software Architecture according to the arc42 template structured?

The following figure shows the resulting structure of the [arc42](https://www.workingsoftware.dev/software-architecture-documentation-the-ultimate-guide/arc42.de) template.

![](https://www.workingsoftware.dev/content/images/2022/12/image-50.png)

The structure of the arc42 template ([Source](https://dev.to/arc42/brief-introduction-to-arc42-1c0l))

### Good examples of an arc42 documentation

- [HTML Sanity Checker (HtmlSC) Architecture Documentation](https://hsc.aim42.org/documentation/hsc_arc42.html) (Gernot Starke)  
   HTML Sanity Checker (HtmlSC) shall support authors creating digital formats  
   with hyperlinks and integration of images and similar resources.
- [DokChess](https://www.dokchess.de/) (Stefan Zörner) 🇩🇪  
   DokChess is a fully functional chess engine.
- [Gradle as an example for arc42](https://www.embarc.de/arc42-starschnitt-gradle/) (Stefan Zörner) 🇩🇪  
   Gradle automates the building, testing and delivery of software.

### Are there any possible pitfalls in the handling with arc42?

❌ **Upfront document everything**

Don't document everything in advance. Think of the arc42 template as a cabinet for documentation. You put something on a shelf as you work on it. This is how software architecture documentation emerges, evolves, and stays  
current.

❌ **Don't includes Tutorials or Q&A sections**

The most important thing in arc42 is the structure. The structure doesn’t  
provide a space for guides or Q&A sections.

❌ **Don't put any specific things like customer names or similar**

Don't write customer-specific things in the software architecture documentation, unless your building blocks are structured in a customer-oriented way.

### Alternative documentation and structuring approaches

There are some alternative structuring and documentation approaches.

- [Recommended Practice for Architectural Description of Software-Intensive Systems (IEEE 1417)](http://cabibbo.dia.uniroma3.it/ids/altrui/ieee1471.pdf)
- [Documenting Software Architecture (SEI)](https://learning.oreilly.com/library/view/documenting-software-architectures/9780132488617/)
- [Software Architecture for Developers (Simon Brown)](https://softwarearchitecturefordevelopers.com/)

## How should we visualize the software architecture?

The [C4 model](https://c4model.com/) is a good approach to obtain a common set of abstractions. It's an abstraction-first approach and is notation independent.

The [C4 model](https://c4model.com/) looks at the static structures of a **software system** in terms of **containers**, **components** and **code**. And **people** use the software systems we build.

![](https://www.workingsoftware.dev/content/images/2022/12/image-60.png)

Abstractions of the C4 Model ([Source](https://c4model.com/))

**What is a software system in C4?**  
A software system is the highest level of abstraction and describes  
something that adds value to its users, whether they are human  
or not.

**What is a Container in C4?**  
A container (not Docker!) is a separately deployable / executable thing.

**What is Component in C4?**  
A component is a grouping of related functionality encapsulated  
behind a well-defined interface. If you're using a language like Java or C#, the easiest way to think of a component is that it's a collection of implementation classes behind an interface.

### What are the core views of C4?

With these abstractions, we can create a [context view (Level 1)](https://c4model.com/), [a container view (Level 2)](https://c4model.com/#ContainerDiagram), [a component view (Level 3)](https://c4model.com/#ComponentDiagram) and [a code view (Level 4)](https://c4model.com/#CodeDiagram).

![](https://www.workingsoftware.dev/content/images/2022/12/image-55.png)

The four levels of the C4 Model. Each level has a different target audience ([Source](https://c4model.com/))

**Level 1: System Context Diagram**

The following illustration shows the system which is embedded in its context.

![](https://www.workingsoftware.dev/content/images/2022/12/image-56.png)

A system context diagram ([Source](https://c4model.com/))

**Level 2: Container Diagram**

If we zoom into the system (the internet banking system in the figure above), we get the container view of this system.

Each of these containers is separately deployable.

![](https://www.workingsoftware.dev/content/images/2022/12/image-57.png)

A container diagram ([Source](https://c4model.com/))

**Level 3: Component Diagram**

If we want to take a look inside a specific container, like the API application, we get the component view of that container.

![](https://www.workingsoftware.dev/content/images/2022/12/image-58.png)

A component diagram ([Source](https://c4model.com/))

**Level 4: Code**

If we go deep into a particular component, we arrive at a "code" view.

![](https://www.workingsoftware.dev/content/images/2022/12/image-59.png)

Level 4: Code Diagram ([Source](https://c4model.com/))

This can be a class diagram. But you can often generate this kind of view by an idea, if necessary.

[UML class diagrams | IntelliJ IDEA](https://www.jetbrains.com/help/idea/class-diagram.html#manage_class_diagram)

### Is the C4 model compatible with arc42?

Yes, arc42 and C4 can be used complementarily.

The C4 diagrams are relevant in the following arc42 chapters:

- [C4 System Context diagram](https://c4model.com/#SystemContextDiagram) can be placed in [arc42 chapter 3 "Context and Scope"](https://docs.arc42.org/section-3/)
- [C4 Container Diagram](https://c4model.com/#ContainerDiagram) can be placed in [arc42 Chapter 5 Building Block View (Level 1)](https://docs.arc42.org/section-5/)
- [C4 Component Diagram](https://c4model.com/#ComponentDiagram) can be placed in [arc42 Chapter 5 Building Block View (Level 2)](https://docs.arc42.org/section-5/)
- [Code Diagram](https://c4model.com/#ComponentDiagram) can be placed in [arc42 Chapter 5 Building Block View (Level 3)](https://docs.arc42.org/section-5/)

Besides the C4 diagrams presented above, there are some additional diagrams of C4 that can be inserted into arc42.

- [C4 Dynamic Diagram](https://c4model.com/#DynamicDiagram) can be placed into [arc42 Chapter 6 Runtime View](https://docs.arc42.org/section-6/)
- [C4 Deployment Diagram](https://c4model.com/#DynamicDiagram) can be placed into [arc42 Chapter 7 Deployment View](https://docs.arc42.org/section-7/)

## How do we write and manage software architecture documentation?

As with any software, there are requirements for technical documentation. Gernot Starke has excellently documented these requirements in the following blog post:

[Principles of technical documentation](https://www.innoq.com/en/articles/2022/01/principles-of-technical-documentation/) - This article collects fundamental requirements for technicaldocumentation, especially software architecture documentation, togetherwith ideas how to _satisfy_ those.

A summary of the documentation requirements can be seen in the following figure from the blog post above:

![](https://www.workingsoftware.dev/content/images/2022/12/image-61.png)

All documentation requirements ([Source](https://www.innoq.com/en/articles/2022/01/principles-of-technical-documentation/))

Meeting some of these requirements (e.g., [req-7](https://www.innoq.com/en/articles/2022/01/principles-of-technical-documentation/#sect-maintainable), [req-9](https://www.innoq.com/en/articles/2022/01/principles-of-technical-documentation/#sect-version-controlled), [req-10](https://www.innoq.com/en/articles/2022/01/principles-of-technical-documentation/#sect-tools), and [req-11](https://www.innoq.com/en/articles/2022/01/principles-of-technical-documentation/#sect-continuously)) leads to the conclusion that we should treat the document as code "Documentation as Code" or "Docs-as-Code".

### What is "Documentation as Code" ?

"Documentation as Code" means that your documentation process benefits from the same practices you use to develop successful software.

Some of these practices are:

- Storing content in a version control system
- Separation of content, configuration, and presentation
- Use of automation for compilation, validation, verification and publishing (CI/CD)
- Reuse shared materials (DRY)
- ...and use your IDE to write content ;-)

With this technique we get some value out-of-the-box:

- Structuring of the whole document into subdocuments
- Restructuring of the documentation according to specific stakeholder
- Reference images, not embedding
- Simple versioning "handle documentation as code”
- Format of the documentation content like source code
- Documentation Reviews, pull requests, versioning through Git tooling
- Conversion to various presentation formats like HTML5, PDF, DocBook, Confluence, ...

![](https://www.workingsoftware.dev/content/images/2022/12/image-62.png)

Treat documentation like code in a common development workflow

### Are there any recommended tools for Documentation as Code?

In Documentation as Code we can distinguish the following process steps: **_Authoring_** (write, validate and preview the documentation content), _**Converting**_ (documents to the pulication formats like HTML, DocBook, PDF, etc.), and **_Publishing_** (Build and deploy documentation artefacts). For each of these steps there are some tools that I can recommend to fulfil the process step.

**_Authoring_: [_AsciiDoc_](https://asciidoc.org/)**

[AsciiDoc](https://asciidoc.org/) is a plain text markup language for writing technical content. Use the [AsciiDoc](https://asciidoc.org/) format to write your content.

_**Convert: [Asciidoctor](https://asciidoctor.org/)**_

[Asciidoctor](https://asciidoctor.org/) is a fast processor for parsing AsciiDoc® into a document model and converting it to output formats such as HTML 5, DocBook 5, manual pages, PDF, EPUB 3, and other formats.

**_Publish:_** _Maven, Gradle, [docToolChain](http://doctoolchain.org/)_

[docToolchain](http://doctoolchain.org/) is a collection of scripts that makes it easy to create and maintain powerful technical documentation. Built on best-of-breed open source technologies, we deliver the best docs toolchain so you don’t have to.

Available tasks of the docToolchain ([Source](http://doctoolchain.org/docToolchain/v2.0.x/015_tasks/03_tasks.html))

### And what's about diagrams?

Like documentation, you can treat diagrams like code.

**Diagrams as Code 1.0**

A classical approach to describe diagrams in text can be done with [PlantUML](https://plantuml.com/de/), [Mermaid](https://mermaid.js.org/#/) or [GraphViz](https://graphviz.org/).

Describe a diagram with text in PlantUML

These diagrams can be embedded directly into AsciiDoc content and converted with AsciiDoctor.

```
[plantuml, target=diagram-classes, format=png]
....
class BlockProcessor
class DiagramBlock
class DitaaBlock
class PlantUmlBlock

BlockProcessor <|-- DiagramBlock
DiagramBlock <|-- DitaaBlock
DiagramBlock <|-- PlantUmlBlock
....
```

PlantUML Code in AsciiDoc embedded

Now let's combine diagrams as code and the C4 model. This brings us to Diagrams as Code 2.0.

**Diagrams as Code 2.0**

What if we could describe our C4 model in text form and generate the C4 diagrams directly?  
This is where [Structurizr](https://structurizr.com/) comes in. It brings diagrams as code into a new dimension - Diagrams as Code 2.0.

With the [Structurizr DSL](https://structurizr.com/dsl) we can describe the Software with the C4 abstractions.

Structurizr DSL Example ([Source](https://structurizr.com/dsl?example=big-bank-plc))

After describing the C4 model of our software system, we can create all defined views directly (with different representations).

![](https://www.workingsoftware.dev/content/images/2022/12/image-70.png)

Awesome, isn't it?

By the way: Simon Browns gave a great talk about diagrams as code 2.0 with [Structurizr](https://structurizr.com/dsl).

### Combine everything together

Now you have the whole toolbox for software architecture documentation:

- Structure it with [arc42](https://arc42.org/)
- Describe and visualize it with the [C4 model](https://c4model.com/)
- Treat your documentation and diagrams like code with [AsciiDoc](https://asciidoc.org/), [AsciiDoctor](https://asciidoctor.org/), [docToolChain](http://doctoolchain.org/) and [Structurizr](https://structurizr.com/)
- ...and integrate it into your development workflow.

![](https://www.workingsoftware.dev/content/images/2022/12/image-77.png)

Combine everything together and get a powerful software architecture documentation

I've created an example repository where I've brought all these techniques and technologies together. Check it out.

[GitHub - bitsmuggler/arc42-c4-software-architecture-documentation-example: This example shows how you can use arc42 in combination with the C4 model and the Documentation as Code technique.](https://github.com/bitsmuggler/arc42-c4-software-architecture-documentation-example) - This example shows how you can use arc42 in combination with the C4 model and the Documentation as Code technique.

### Further supporting software architecture documentation tools

- [D2 Lang](https://d2lang.com/tour/intro/)
- [Diagrams](https://diagrams.mingrammer.com/)
- [Kroki](https://kroki.io/)
- [Terrastruct](https://terrastruct.com/)
- [Context Mapper](https://contextmapper.org/docs/home/)
- [Spring Modulith](https://spring.io/projects/spring-modulith)

All Documentation as Code Tools can be found under the following link 👇

[Documentation as Code Tools](https://www.workingsoftware.dev/documentation-as-code-tools/) - This page contains all the modern tools, languages and frameworks, platforms and techniques you need to know to treat documentation like code.
