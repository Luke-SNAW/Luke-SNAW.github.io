
> https://feature-sliced.design/  
> https://github.com/feature-sliced/documentation

## Overview

### Is it right for me?[#](https://feature-sliced.design/docs/get-started/overview#is-it-right-for-me "Direct link to heading")

FSD can be implemented in projects and teams of any size, but there are a few things to keep in mind:

- This methodology is for front-end projects only. If you're looking for a back-end architecture, consider [Clean Architecture](https://medium.com/codex/clean-architecture-for-dummies-df6561d42c94).
- A very simple app of a single page might not need the benefits of FSD and suffer from the overhead. However, FSD promotes a nice way of thinking, so feel free to use on the tiniest projects if you want.
- A huge app, the size of the Google Cloud admin dashboard, will require a custom architecture. It could still be based on FSD, by the way.

FSD doesn't enforce a particular programming language, UI framework or state manager — bring your own or see some [examples](https://feature-sliced.design/examples).

If you have an existing project, fear not — FSD can be adopted incrementally. Just make sure that your team is **in pain** from the current architecture, otherwise a switch might not be worth it. For migration guidance, see the [Migration section](https://feature-sliced.design/docs/guides/migration).

### Basics[#](https://feature-sliced.design/docs/get-started/overview#basics "Direct link to heading")

In FSD, a [project consists](https://feature-sliced.design/docs/reference/units/decomposition) of layers, each layer is made up of slices and each slice is made up of segments.

![themed--scheme](/assets/images/visual_schema-ca092cc631de8c129dfb48174d0a927a.jpg)

The **layers** are standardized across all projects and vertically arranged. Modules on one layer can only interact with modules from the layers strictly below. There are currently seven of them (bottom to top):

1. `shared` — reusable functionality, detached from the specifics of the project/business.(e.g. UIKit, libs, API)
2. `entities` — business entities.(e.g., User, Product, Order)
3. `features` — user interactions, actions that bring business value to the user.(e.g. SendComment, AddToCart, UsersSearch)
4. `widgets` — compositional layer to combine entities and features into meaningful blocks.(e.g. IssuesList, UserProfile)
5. `pages` — compositional layer to construct full pages from entities, features and widgets.
6. `processes` — complex inter-page scenarios. (e.g., authentication)
7. `app` — app-wide settings, styles and providers.

Then there are **slices**, which partition the code by business domain. This makes your codebase easy to navigate by keeping logically related modules close together. Slices cannot use other slices on the same layer, and that helps with high cohesion and low coupling.

Each slice, in turn, consists of **segments**. These are tiny modules that are meant to help with separating code within a slice by its technical purpose. The most common segments are `ui`, `model` (store, actions), `api` and `lib` (utils/hooks), but you can omit some or add more, as you see fit.

note

In most cases, [it is recommended](https://github.com/feature-sliced/documentation/discussions/66) to place `api` and `config` only in the shared layer

### Example[#](https://feature-sliced.design/docs/get-started/overview#example "Direct link to heading")

Let's consider a social network application.

- `app/` contains setup of routing, store and global styles.
- `processes/` contains the part of authentication that is responsible for reading/writing authentication tokens.
- `pages/` contains the route components for each page in the app, mostly composition, hardly any logic.

Within that application, let's consider a post card in a news feed.

- `widgets/` contains the "assembled" post card, with content and interactive buttons that are wired up to the relevant calls on the back-end.
- `features/` contains the interactivity of the card (e.g., like button) and the logic of processing those interactions.
- `entities/` contains the shell of the card with slots for content and the interactive elements. The tile representing the post author is also here, but in a different slice.

### Advantages[#](https://feature-sliced.design/docs/get-started/overview#advantages "Direct link to heading")

- **Uniformity**  
   The code is organized by scope of influence (layers), by domain (slices), and by technical purpose (segments).  
   This creates a standardized architecture that is easier to comprehend for newcomers.
- **Controlled reuse of logic**  
   Each architectural component has its purpose and predictable dependencies.  
   This keeps a balance between following the **DRY** principle and adaptation possibilities.
- **Stability in face of changes and refactoring**  
   A module on a particular layer cannot use other modules on the same layer, or the layers above.  
   This enables isolated modifications without unforeseen consequences.
- **Orientation to business and users needs**  
   App splitting by business domains help to deeper understand, structure and discovery project features.

### Incremental adoption[#](https://feature-sliced.design/docs/get-started/overview#incremental-adoption "Direct link to heading")

The power of FSD lies in _structured_ decomposition. At its finest, it enables to locate any part of code near-deterministically. However, the level of decomposition is a parameter, and each team can tweak it to strike a balance between simple adoption and the amount of benefits.

Here's a proposed strategy to migrate an existing codebase to FSD, based on experience:

1. Start by outlining the `app` and `shared` layers to create a foundation. Usually, these layers are the smallest.
2. Distribute all of the existing UI across `widgets` and `pages`, even if they have dependencies that violate the rules of FSD.
3. Start gradually increasing the precision of decomposition by separating `features` and `entities`, turning pages and widgets from logic-bearing layers into purely compositional layers.

It's advised to refrain from adding new large entities while refactoring or refactoring only certain parts of the project.

## [Structure](https://github.com/feature-sliced/documentation/blob/master/README.md#structure)

```
└── src/
    ├── app/                    # Layer: Application
    |                           #
    ├── processes/              # Layer: Processes (optional)
    |   ├── {some-process}/     #     Slice: (e.g. CartPayment process)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   └── model/          #         Segment: Business Logic
    |   ...                     #
    |                           #
    ├── pages/                  # Layer: Pages
    |   ├── {some-page}/        #     Slice: (e.g. ProfilePage page)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   ├── model/          #         Segment: Business Logic
    |   |   └── ui/             #         Segment: UI logic
    |   ...                     #
    |                           #
    ├── widgets/                # Layer: Widgets
    |   ├── {some-widget}/      #     Slice: (e.g. Header widget)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   ├── model/          #         Segment: Business Logic
    |   |   └── ui/             #         Segment: UI logic
    ├── features/               # Layer: Features
    |   ├── {some-feature}/     #     Slice: (e.g. AuthByPhone feature)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   ├── model/          #         Segment: Business Logic
    |   |   └── ui/             #         Segment: UI logic
    |   ...                     #
    |                           #
    ├── entities/               # Layer: Business entities
    |   ├── {some-entity}/      #     Slice: (e.g. entity User)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   ├── model/          #         Segment: Business Logic
    |   |   └── ui/             #         Segment: UI logic
    |   ...                     #
    |                           #
    ├── shared/                 # Layer: Reused resources
    |   ├── api/                #         Segment: Logic of API requests
    |   ├── config/             #         Segment: Application configuration
    |   ├── lib/                #         Segment: Infrastructure-application logic
    |   └── ui/                 #         Segment: UIKit of the application
    |   ...                     #
    |                           #
    └── index.tsx/              #
```
