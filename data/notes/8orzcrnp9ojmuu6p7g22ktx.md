
> https://alexkondov.com/tao-of-node/
>
> https://news.ycombinator.com/item?id=30818914

Design, Architecture & Best Practices

---

I’ve been working with React since 2016 and still there isn’t a single best practice when it comes to application structure and design.

While there are best practices on the micro level, most teams build their own “thing” when it comes to architecture.

Of course, there isn’t a universal best practice that can be applied to all businesses and applications. But there are some general rules that we can follow to build a productive codebase.

The purpose of a software’s architecture and design is to keep it productive and flexible. Developers need to work on it effectively and modify it without rewriting its core.

This article is a collection of principles and rules that have proven to be effective for me and the teams I’ve worked with.

I outline good practices about components, application structure, testing, styling, state management and data fetching. Some of the examples are oversimplified so we can focus on the principle not on the implementation.

**Take everything here as an opinion**, not an absolute. There’s more than one way to build software.

## Table of Contents

- [Components](https://alexkondov.com/tao-of-react/#components)
  - [Favor Functional Components](https://alexkondov.com/tao-of-react/#favor-functional-components)
  - [Write Consistent Components](https://alexkondov.com/tao-of-react/#write-consistent-components)
  - [Name Components](https://alexkondov.com/tao-of-react/#name-components)
  - [Organize Helper Functions](https://alexkondov.com/tao-of-react/#organize-helper-functions)
  - [Don’t Hardcode Markup](https://alexkondov.com/tao-of-react/#dont-hardcode-markup)
  - [Component Length](https://alexkondov.com/tao-of-react/#component-length)
  - [Component Length](https://alexkondov.com/tao-of-react/#component-length)
  - [Write Comments](https://alexkondov.com/tao-of-react/#write-comments)
  - [Use Error Boundaries](https://alexkondov.com/tao-of-react/#use-error-boundaries)
  - [Destructure Props](https://alexkondov.com/tao-of-react/#destructure-props)
  - [Number of Props](https://alexkondov.com/tao-of-react/#number-of-props)
  - [Use Objects Instead of Primitives](https://alexkondov.com/tao-of-react/#objects-instead-of-primitives)
  - [Conditional Rendering](https://alexkondov.com/tao-of-react/#conditional-rendering)
  - [Avoid Nested Ternary Operators](https://alexkondov.com/tao-of-react/#avoid-nested-ternary-operators)
  - [Move Lists in Components](https://alexkondov.com/tao-of-react/#move-lists-in-components)
  - [Assign Default Props When Destructuring](https://alexkondov.com/tao-of-react/#default-props-when-destructuring)
  - [Avoid Nested Render Functions](https://alexkondov.com/tao-of-react/#avoid-nested-render-functions)
  - [Prefer Hooks](https://alexkondov.com/tao-of-react/#prefer-hooks)
- [State Management](https://alexkondov.com/tao-of-react/#state-management)
  - [Use Reducers](https://alexkondov.com/tao-of-react/#use-reducers)
  - [Use Data Fetching Libraries](https://alexkondov.com/tao-of-react/#use-data-fetching-libraries)
  - [State Management Libraries](https://alexkondov.com/tao-of-react/#state-management-libraries)
- [Component Mental models](https://alexkondov.com/tao-of-react/#component-mental-models)
  - [Container and Presentational](https://alexkondov.com/tao-of-react/#container-and-presentational)
  - [Stateless and Stateful](https://alexkondov.com/tao-of-react/#stateless-and-stateful)
- [Application Structure](https://alexkondov.com/tao-of-react/#application-structure)
  - [Group by Route/Module](https://alexkondov.com/tao-of-react/#group-by-route-module)
  - [Create a Common Module](https://alexkondov.com/tao-of-react/#create-a-common-module)
  - [Use Absolute Paths](https://alexkondov.com/tao-of-react/#use-absolute-paths)
  - [Wrap External Components](https://alexkondov.com/tao-of-react/#wrap-external-components)
  - [Move Components in Folders](https://alexkondov.com/tao-of-react/#move-components-in-folders)
- [Performance](https://alexkondov.com/tao-of-react/#performance)
  - [Don’t Optimize Prematurely](https://alexkondov.com/tao-of-react/#dont-optimize-prematurely)
  - [Watch Bundle Size](https://alexkondov.com/tao-of-react/#watch-bundle-size)
  - [Rerenders - Callbacks, Arrays and Objects](https://alexkondov.com/tao-of-react/#rerenders)
- [Testing](https://alexkondov.com/tao-of-react/#testing)
  - [Don’t Rely on Snapshot Tests](https://alexkondov.com/tao-of-react/#dont-rely-on-snapshots)
  - [Test Correct Rendering](https://alexkondov.com/tao-of-react/#test-correct-rendering)
  - [Validate State and Events](https://alexkondov.com/tao-of-react/#validate-state-events)
  - [Test Edge Cases](https://alexkondov.com/tao-of-react/#test-edge-cases)
  - [Write Integration Tests](https://alexkondov.com/tao-of-react/#write-integration-tests)
- [Styling](https://alexkondov.com/tao-of-react/#styling)
  - [Use CSS-in-JS](https://alexkondov.com/tao-of-react/#use-css-in-js)
  - [Keep Styled Components Together](https://alexkondov.com/tao-of-react/#keep-styled-components-together)
- [Data Fetching](https://alexkondov.com/tao-of-react/#data-fetching)
  - [Use a Data Fetching Library](https://alexkondov.com/tao-of-react/#use-a-data-fetching-library)

## Components [#](https://alexkondov.com/tao-of-react/#components)

### Favor Functional Components [#](https://alexkondov.com/tao-of-react/#favor-functional-components)

Favor functional components - they have a simpler syntax. No lifecycle methods, constructors or boilerplate. You can express the same logic with less characters without losing readability.

Unless you need an error boundary they should be your go-to approach. The mental model you need to keep in your head is a lot smaller.

```jsx
// 👎 Class components are verbose
class Counter extends React.Component {
  state = {
    counter: 0,
  };

  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState({ counter: this.state.counter + 1 });
  }

  render() {
    return (
      <div>
        <p>counter: {this.state.counter}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}

// 👍 Functional components are easier to read and maintain
function Counter() {
  const [counter, setCounter] = useState(0);

  handleClick = () => setCounter(counter + 1);

  return (
    <div>
      <p>counter: {counter}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}
```

### Write Consistent Components [#](https://alexkondov.com/tao-of-react/#write-consistent-components)

Stick to the same style for your components. Put helper functions in the same place, export the same way and follow the same naming patterns.

There isn’t a real benefit of one approach over the other

No matter if you’re exporting at the bottom of the file or directly in the definition of the component, pick one and stick to it.

### Name Components [#](https://alexkondov.com/tao-of-react/#name-components)

Always name your components. It helps when you’re reading an error stack trace and using the React Dev Tools.

It’s also easier to find where you are when developing if the component’s name is inside the file.

```jsx
// 👎 Avoid this
export default () => <form>...</form>

// 👍 Name your functions
export default function Form() {
  return <form>...</form>
}
```

### Organize Helper Functions [#](https://alexkondov.com/tao-of-react/#organize-helper-functions)

Helper functions that don’t need to hold a closure over the components should be moved outside. The ideal place is before the component definition so the file can be readable from top to bottom.

That reduces the noise in the component and leaves inside only those that need to be there.

```jsx
// 👎 Avoid nesting functions which don't need to hold a closure.
function Component({ date }) {
  function parseDate(rawDate) {
    ...
  }

  return <div>Date is {parseDate(date)}</div>
}

// 👍 Place the helper functions before the component
function parseDate(date) {
  ...
}

function Component({ date }) {
  return <div>Date is {parseDate(date)}</div>
}
```

You want to keep the least amount of helper functions inside the definition. Move as many as possible outside and pass the values from state as arguments.

Composing your logic out of pure functions that rely only on input makes it easier to track bugs and extend.

```jsx
// 👎 Helper functions shouldn't read from the component's state
export default function Component() {
  const [value, setValue] = useState('')

  function isValid() {
    // ...
  }

  return (
    <>
      <input
        value={value}
        onChange={e => setValue(e.target.value)}
        onBlur={validateInput}
      />
      <button
        onClick={() => {
          if (isValid) {
            // ...
          }
        }}
      >
        Submit
      </button>
    </>
  )
}

// 👍 Extract them and pass only the values they need
function isValid(value) {
  // ...
}

export default function Component() {
  const [value, setValue] = useState('')

  return (
    <>
      <input
        value={value}
        onChange={e => setValue(e.target.value)}
        onBlur={validateInput}
      />
      <button
        onClick={() => {
          if (isValid(value)) {
            // ...
          }
        }}
      >
        Submit
      </button>
    </>
  )
}
```

### Don't Hardcode Markup [#](https://alexkondov.com/tao-of-react/#dont-hardcode-markup)

Don’t hardcode markup for navigation, filters or lists. Use a configuration object and loop through the items instead.

This means you only have to change the markup and items in a single place.

```jsx
// 👎 Hardcoded markup is harder to manage.
function Filters({ onFilterClick }) {
  return (
    <>
      <p>Book Genres</p>
      <ul>
        <li>
          <div onClick={() => onFilterClick("fiction")}>Fiction</div>
        </li>
        <li>
          <div onClick={() => onFilterClick("classics")}>Classics</div>
        </li>
        <li>
          <div onClick={() => onFilterClick("fantasy")}>Fantasy</div>
        </li>
        <li>
          <div onClick={() => onFilterClick("romance")}>Romance</div>
        </li>
      </ul>
    </>
  );
}

// 👍 Use loops and configuration objects
const GENRES = [
  {
    identifier: "fiction",
    name: Fiction,
  },
  {
    identifier: "classics",
    name: Classics,
  },
  {
    identifier: "fantasy",
    name: Fantasy,
  },
  {
    identifier: "romance",
    name: Romance,
  },
];

function Filters({ onFilterClick }) {
  return (
    <>
      <p>Book Genres</p>
      <ul>
        {GENRES.map((genre) => (
          <li>
            <div onClick={() => onFilterClick(genre.identifier)}>
              {genre.name}
            </div>
          </li>
        ))}
      </ul>
    </>
  );
}
```

### Component Length [#](https://alexkondov.com/tao-of-react/#component-length)

A React component is just a function that gets props and returns markup. They adhere to the same software design principles.

If a function is doing too many things, extract some of the logic and call another function. It’s the same with components - if you have too much functionality, split it in smaller components and call them instead.

If a part of the markup is complex, requires loops and conditionals - extract it.

Rely on props and callbacks for communication and data. Lines of code are not an objective measure. Think about responsibilities and abstractions instead.

### Write Comments in JSX [#](https://alexkondov.com/tao-of-react/#write-comments)

when something needs more clarity open a code block and give additional information. The markup is a part of the logic so when you feel that something needs more clarity - provide it.

```jsx
function Component(props) {
  return (
    <>
      {/* If the user is subscribed we don't want to show them any ads */}
      {user.subscribed ? null : <SubscriptionPlans />}
    </>
  );
}
```

### Use Error Boundaries [#](https://alexkondov.com/tao-of-react/#use-error-boundaries)

An error in one component shouldn’t bring down the entire UI. There are rare cases in which we want to take down the whole page or redirect if a critical error happens. Most of the times we’d be fine if we just hide a specific element from the screen.

In a function that deals with data you may have multiple try/catch statements. Put error boundaries to use not just on the top level. Wrap elements on the screen that can exist separately to avoid cascading failures.

```jsx
function Component() {
  return (
    <Layout>
      <ErrorBoundary>
        <CardWidget />
      </ErrorBoundary>

      <ErrorBoundary>
        <FiltersWidget />
      </ErrorBoundary>

      <div>
        <ErrorBoundary>
          <ProductList />
        </ErrorBoundary>
      </div>
    </Layout>
  );
}
```

### Destructure Props [#](https://alexkondov.com/tao-of-react/#destructure-props)

Most React components are just functions. They get props and return markup. In a normal function you use the arguments it is passed directly, so it makes sense to apply the same principle here. No need to repeat `props` everywhere.

A reason not to destructure the props would be to distinguish what is external and what is internal state. But in a regular function there is no distinction between arguments and variables. Don’t create unnecessary patterns.

```jsx
// 👎 Don't repeat props everywhere in your component
function Input(props) {
  return <input value={props.value} onChange={props.onChange} />;
}

// 👍 Destructure and use the values directly
function Component({ value, onChange }) {
  const [state, setState] = useState("");

  return <div>...</div>;
}
```

### Number of Props [#](https://alexkondov.com/tao-of-react/#number-of-props)

The question of how many props should a component receive is a subjective one. The number of props that a component has is correlated to how much it’s doing. The more props you pass to it the more responsibilities it has.

A high number of props is a signal that a component is doing too much.

If I go above 5 props I consider whether this component should be split. In some cases, it may just need a lot of data. An input field, for example, may have a lot of props. In others it’s a sign that something needs to be extracted.

Note: The more props a component takes, the more reasons to rerender.

### Pass Objects Instead of Primitives [#](https://alexkondov.com/tao-of-react/#objects-instead-of-primitives)

One way to limit the amount of props is to pass an object instead of primitive values. Rather than passing down the user name, email and settings one by one you can group them together. This also reduces the changes that need to be done if the user gets an extra field for example.

Using TypeScript makes this even easier.

```jsx
// 👎 Don't pass values on by one if they're related
<UserProfile
  bio={user.bio}
  name={user.name}
  email={user.email}
  subscription={user.subscription}
/>

// 👍 Use an object that holds all of them instead
<UserProfile user={user} />
```

### Conditional Rendering [#](https://alexkondov.com/tao-of-react/#conditional-rendering)

In some situations using short circuit operators for conditional rendering may backfire and you may end up with an unwanted `0` in your UI. To avoid this default to using ternary operators. The only caveat is that they’re more verbose.

The short-circuit operator reduces the amount of code which is always nice. Ternaries are more verbose but there is no chance to get it wrong. Plus, adding the alternative condition is less of a change.

```jsx
// 👎 Try to avoid short-circuit operators
function Component() {
  const count = 0;

  return <div>{count && <h1>Messages: {count}</h1>}</div>;
}

// 👍 Use a ternary instead
function Component() {
  const count = 0;

  return <div>{count ? <h1>Messages: {count}</h1> : null}</div>;
}
```

### Avoid Nested Ternary Operators [#](https://alexkondov.com/tao-of-react/#avoid-nested-ternary-operators)

Ternary operators become hard to read after the first level. Even if they seem to save space at the time, it’s better to be explicit and obvious in your intentions.

```jsx
// 👎 Nested ternaries are hard to read in JSX
isSubscribed ? (
  <ArticleRecommendations />
) : isRegistered ? (
  <SubscribeCallToAction />
) : (
  <RegisterCallToAction />
);

// 👍 Place them inside a component on their own
function CallToActionWidget({ subscribed, registered }) {
  if (subscribed) {
    return <ArticleRecommendations />;
  }

  if (registered) {
    return <SubscribeCallToAction />;
  }

  return <RegisterCallToAction />;
}

function Component() {
  return <CallToActionWidget subscribed={subscribed} registered={registered} />;
}
```

### Move Lists in a Separate Component [#](https://alexkondov.com/tao-of-react/#move-lists-in-components)

Looping through a list of items is a common occurrence, usually done with the `map` function. However, in a component that has a lot of markup, the extra indentation and the syntax of `map` don’t help with readability.

When you need to map over elements, extract them in their own listing component, even if the markup isn’t much. The parent component doesn’t need to know about the details, only that it’s displaying a list.

Only keep a loop in the markup if the component’s main responsibility is to display it. Try to keep a single mapping per component but if the markup is long or complicated, extract the list either way.

```jsx
// 👎 Don't write loops together with the rest of the markup
function Component({ topic, page, articles, onNextPage }) {
  return (
    <div>
      <h1>{topic}</h1>
      {articles.map((article) => (
        <div>
          <h3>{article.title}</h3>
          <p>{article.teaser}</p>
          <img src={article.image} />
        </div>
      ))}
      <div>You are on page {page}</div>
      <button onClick={onNextPage}>Next</button>
    </div>
  );
}

// 👍 Extract the list in its own component
function Component({ topic, page, articles, onNextPage }) {
  return (
    <div>
      <h1>{topic}</h1>
      <ArticlesList articles={articles} />
      <div>You are on page {page}</div>
      <button onClick={onNextPage}>Next</button>
    </div>
  );
}
```

### Assign Default Props When Destructuring [#](https://alexkondov.com/tao-of-react/#default-props-when-destructuring)

One way to specify default prop values is to attach a `defaultProps` property to the component. This means that the component function and the values for its arguments are not going to sit together.

Prefer assigning default values directly when you’re destructuring the props. It makes it easier to read the code from top to bottom without jumping and keeps the definitions and values together.

```jsx
// 👎 Don't define the default props outside of the function
function Component({ title, tags, subscribed }) {
  return <div>...</div>;
}

Component.defaultProps = {
  title: "",
  tags: [],
  subscribed: false,
};

// 👍 Place them in the arguments list
function Component({ title = "", tags = [], subscribed = false }) {
  return <div>...</div>;
}
```

### Avoid Nested Render Functions [#](https://alexkondov.com/tao-of-react/#avoid-nested-render-functions)

When you need to extract markup from a component or logic, don’t put it in a function living in the same component. A component is just a function. Defining it this way is nesting inside its parent.

This means that it will have access to all the state and data of its parent. It makes the code more unreadable - what is this function doing in between all the components?

Move it in its own component, name it and rely on props instead of a closure.

```jsx
// 👎 Don't write nested render functions
function Component() {
  function renderHeader() {
    return <header>...</header>;
  }
  return <div>{renderHeader()}</div>;
}

// 👍 Extract it in its own component
import Header from "@modules/common/components/Header";

function Component() {
  return (
    <div>
      <Header />
    </div>
  );
}
```

## State Management [#](https://alexkondov.com/tao-of-react/#state-management)

### Use Reducers [#](https://alexkondov.com/tao-of-react/#use-reducers)

Sometimes you need a more powerful way to express and manage state changes. Start with `useReducer` before you reach for an external library. This is a great mechanism to do complex state management and it doesn’t require 3rd party dependencies.

In combination with React’s Context and TypeScript, `useReducer` can be really powerful. Unfortunately, it’s not that widely used. People still reach for 3rd party libraries.

If you need multiple pieces of state, move them to a reducer instead.

```jsx
// 👎 Don't use too many separate pieces of state
const TYPES = {
  SMALL: 'small',
  MEDIUM: 'medium',
  LARGE: 'large'
}

function Component() {
  const [isOpen, setIsOpen] = useState(false)
  const [type, setType] = useState(TYPES.LARGE)
  const [phone, setPhone] = useState('')
  const [email, setEmail] = useState('')
  const [error, setError] = useSatte(null)

  return (
    ...
  )
}

// 👍 Unify them in a reducer instead
const TYPES = {
  SMALL: 'small',
  MEDIUM: 'medium',
  LARGE: 'large'
}

const initialState = {
  isOpen: false,
  type: TYPES.LARGE,
  phone: '',
  email: '',
  error: null
}

const reducer = (state, action) => {
  switch (action.type) {
    ...
    default:
      return state
  }
}

function Component() {
  const [state, dispatch] = useReducer(reducer, initialState)

  return (
    ...
  )
}
```

### Prefer Hooks to HOCs and Render Props [#](https://alexkondov.com/tao-of-react/#prefer-hooks)

In some cases we need to enhance a component or give it access to external state. In general there are three ways to do this - higher order components (HOCs), render props and hooks.

Hooks have proven to be the most efficient way to achieve such composition. From a philosophical standpoint, a component is a function that **uses** other functions. Hooks allow you to tap into multiple sources of external functionality without them conflicting with each other. No matter the number of hooks, you know where each value comes from.

With HOCs you get values as props. This makes it unclear wether they come from the parent component or the wrapping one. Also, chaining multiple props together is known to cause errors.

Render props lead to high indentation and bad readability. Nesting multiple components with render props in the same tree makes the markup look even worse. Also it only exposes the values in the markup itself so you have to write the logic there or pass it down.

With hooks you work with simple values, which are easy to track and don’t interfere with the JSX.

```jsx
// 👎 Avoid using render props
function Component() {
  return (
    <>
      <Header />
      <Form>
        {({ values, setValue }) => (
          <input
            value={values.name}
            onChange={e => setValue('name', e.target.value)}
          />
          <input
            value={values.password}
            onChange={e => setValue('password', e.target.value)}
          />
        )}
      </Form>
      <Footer />
    </>
  )
}

// 👍 Favor hooks for their simplicity and readability
function Component() {
  const [values, setValue] = useForm()

  return (
    <>
      <Header />
      <input
        value={values.name}
        onChange={e => setValue('name', e.target.value)}
      />
      <input
        value={values.password}
        onChange={e => setValue('password', e.target.value)}
      />
    )}
      <Footer />
    </>
  )
}
```

### Use Data Fetching Libraries [#](https://alexkondov.com/tao-of-react/#use-data-fetching-libraries)

Often the data that we want to manage in state is retrieved from an API. We need to keep that data in memory, update it and access it in multiple places.

Modern data fetching libraries like [React Query](https://react-query.tanstack.com/) provide enough mechanisms to manage the external data. We can cache it, invalidate it and fetch it anew. They can be used for sending data as well, triggering a refresh for another piece of data.

It’s even easier if you’re working with a GraphQL client like [Apollo](https://www.apollographql.com/docs/react/). It has the concept of client state built in.

### State Management Libraries [#](https://alexkondov.com/tao-of-react/#state-management-libraries)

In most cases you don’t need a state management library. They should be used in large applications that require managing complex state. There are plenty of guides on this topic so I’ll just mention the two libraries that I would explore in such a situation - [Recoil](https://recoiljs.org/) and [Redux](https://redux.js.org/).

## Component Mental Models [#](https://alexkondov.com/tao-of-react/#component-mental-models)

### Container & Presentational [#](https://alexkondov.com/tao-of-react/#container-and-presentational)

The predominant line of thinking is to split components in two groups - presentational and container components. Also known as smart and dumb.

The idea is that some components don’t have any functionality and state. They are just called by the parent component with some props. The container components contain the business logic, do the data fetching and manage the state.

This mental model is what the MVC structure is for back-end applications. It’s generic enough to work everywhere and you can’t go wrong with it.

**But**, in modern UI applications that pattern falls short. Pulling all the logic in a few components leads to bloat. They end up with too many responsibilities and become hard to manage. As an app grows putting the complexity in a few concentrated places is just not good for maintainability.

### Stateless & Stateful [#](https://alexkondov.com/tao-of-react/#stateless-and-stateful)

Think of components as stateful and stateless. The mental model mentioned above implies that a few components should be managing a lot of the complexity. Instead, it should be spread throughout the app.

Data should live close to where it is used. When you’re using a GraphQL client you fetch the data in the component that displays it. Even if it’s not a top level one. Don’t think about **containers**, think about **responsibilities**. Consider what is the most logical component to hold a piece of state.

For example, a `<Form />` component should own the data of the form. An `<Input />` should be receiving values and calling callbacks when a change occurs. A `<Button />` should notify the form that it was pressed and let the form handle what happens.

Who does the validation in a form? Is the input field responsible? That would mean that this component becomes aware of the business logic of your application. How will it notify the form that there is an error? How will that error state be refreshed? Will the form know about that? If there’s an error but you try to submit, what will happen?

When faced with questions like this you should become aware that responsibilities are getting mixed up. In this case it’s better for the input to be left stateless and receive an error message from the form.

## Application Structure [#](https://alexkondov.com/tao-of-react/#application-structure)

### Group by Route/Module [#](https://alexkondov.com/tao-of-react/#group-by-route-module)

Grouping by containers and components makes applications hard to navigate. To understand what component belongs where you need a good level of familiarity.

Not all components are equal - some are used globally, others are made for a specific part of the app. This structure works well for the smallest of projects. But anything that goes beyond a handful of components becomes hard to manage.

```js
// 👎 Don't group by technical details
├── containers
|   ├── Dashboard.jsx
|   ├── Details.jsx
├── components
|   ├── Table.jsx
|   ├── Form.jsx
|   ├── Button.jsx
|   ├── Input.jsx
|   ├── Sidebar.jsx
|   ├── ItemCard.jsx

// 👍 Group by module/domain
├── modules
|   ├── common
|   |   ├── components
|   |   |   ├── Button.jsx
|   |   |   ├── Input.jsx
|   ├── dashboard
|   |   ├── components
|   |   |   ├── Table.jsx
|   |   |   ├── Sidebar.jsx
|   ├── details
|   |   ├── components
|   |   |   ├── Form.jsx
|   |   |   ├── ItemCard.jsx
```

Group by route/module from the start. This is a structure that supports change and growth. The point is not to have your application outgrow the architecture quickly. If it’s based on components and containers that will happen too fast.

A module based architecture is easy to extend. You can just add modules on top of it without increasing the complexity.

The container/component structure is not wrong but it’s too generic. It doesn’t tell the reader anything about the project besides that it uses React.

### Create a Common Module [#](https://alexkondov.com/tao-of-react/#create-a-common-module)

Components like buttons, inputs and cards are used all over the place. Even if you’re not going with a module based structure it’s good to extract those.

You can see what common components you have even if you’re not using Storybook. It helps to avoid duplication. You don’t want everyone on the team to make their own version of a button. Unfortunately, this happens way too often because of badly structured projects.

### Use Absolute Paths [#](https://alexkondov.com/tao-of-react/#use-absolute-paths)

Making things easier to change is fundamental for your project structure. Absolute paths mean that you will have to change less if you need to move a component. Also it makes it easier to find out where everything is getting pulled from.

```jsx
// 👎 Don't use relative paths
import Input from "../../../modules/common/components/Input";

// 👍 Absolute ones don't change
import Input from "@modules/common/components/Input";
```

I use the `@` prefix to signal that it’s an internal module but I’ve seen it done with `~` as well.

### Wrap External Components [#](https://alexkondov.com/tao-of-react/#wrap-external-components)

Try not to import too many 3rd party components directly. By creating an adapter around them we can modify the API if we have to. Also, we can change the library in a single place.

This goes for component libraries like Semantic UI and utility components as well. The simplest thing you can do is reexport them from the common module so they’re pulled from the same place.

A component doesn’t need to know what library we’re using for the date picker - only that it exists.

```jsx
// 👎 Don't import directly
import { Button } from "semantic-ui-react";
import DatePicker from "react-datepicker";

// 👍 Export the component and use it referencing your internal module
import { Button, DatePicker } from "@modules/common/components";
```

### Move Components in Folders [#](https://alexkondov.com/tao-of-react/#move-components-in-folders)

I create a components folder for each module in my React applications. Whenever I need to create a component I create it there first. If it needs extra files like styles or tests, I create its own folder and put them there.

As a general practice it’s good to have an `index.js` file which exports the React component so you don’t have to change import paths or have repetitive ones like `import Form from 'components/UserForm/UserForm'`. Still, keep the component file with its name so you don’t get confused when you have multiple ones open.

```js
// 👎 Don't keep all component files together
├── components
    ├── Header.jsx
    ├── Header.scss
    ├── Header.test.jsx
    ├── Footer.jsx
    ├── Footer.scss
    ├── Footer.test.jsx

// 👍 Move them in their own folder
├── components
    ├── Header
        ├── index.js
        ├── Header.jsx
        ├── Header.scss
        ├── Header.test.jsx
    ├── Footer
        ├── index.js
        ├── Footer.jsx
        ├── Footer.scss
        ├── Footer.test.jsx
```

## Performance [#](https://alexkondov.com/tao-of-react/#performance)

### Don't Optimize Prematurely [#](https://alexkondov.com/tao-of-react/#dont-optimize-prematurely)

Before you make any kinds of optimizations, make sure that there is a reason for them. Following e best practice blindly is a waste of effort unless it’s impacting your application in a way.

Yes, it’s important to be aware of certain things but prioritize building readable and maintainable components before performance. Well written code is easier to improve.

When you notice a performance problem in your application - measure and identify the cause of your problem. No point in trying to reduce rerender count if your bundle size is enormous.

Once you know where the performance problems are coming from, fix them in the order of their impact.

### Watch The Bundle Size [#](https://alexkondov.com/tao-of-react/#watch-bundle-size)

The amount of JavaScript that has to be sent to the browser is the most important factor of your application’s performance. Your app can be blazing fast but chances are no one will find out about this if they have to load 4MB of JS to load it.

Don’t ship a single JS bundle. Split your application on the route level and even further. Make sure you’re sending the least amount of JS possible.

Load in the background or when the user shows intent that they’ll need another bundle. If a button press is triggering a PDF download, you can delay the download of the PDF library until the button is hovered.

### Rerenders - Callbacks, Arrays and Objects [#](https://alexkondov.com/tao-of-react/#rerenders)

It’s good to try and reduce the amount of unnecessary rerenders that your app makes. Keep this in mind but also note that unnecessary rerenders will rarely have the greatest impact on your app.

The most common advice is to avoid passing callback functions as props. Using one means that a new function will be created each time, triggering a rerender. I haven’t faced any performance problems with callbacks and in fact that’s my go to approach.

If you are experiencing performance problems and the closures are the cause then remove them. But don’t make your code less readable ot more verbose unnecessarily.

Passing down arrays or objects directly falls into the same category of problems. They fail the reference check so they will trigger a rerender. If you need to pass a fixed array extract it as a constant before the component definition to make sure the same instance is passed each time.

## Testing [#](https://alexkondov.com/tao-of-react/#testing)

### Don't Rely on Snapshot Tests [#](https://alexkondov.com/tao-of-react/#dont-rely-on-snapshots)

Ever since I started working with React in 2016 I’ve had only one situation in which snapshot tests have caught a problem in my components. A call to `new Date()` without an argument had slipped and it always defaulted to the current date.

Besides this, snapshots have only been a cause for failed builds when a component is changed. The usual workflow is to make a change to the component, see that snapshots are failing, update them and proceed.

Don’t get me wrong, they are a good sanity check but they are not a replacement for good component level tests. I avoid even creating them anymore.

### Test Correct Rendering [#](https://alexkondov.com/tao-of-react/#test-correct-rendering)

The main thing that your tests should validate is whether the component works as expected. Make sure that it renders correctly with its default props and with ones passed to it.

Validate that for a given input (props) the function returns the correct result (JSX). Validate that everything you need is on the screen.

### Validate State & Events [#](https://alexkondov.com/tao-of-react/#validate-state-events)

A stateful component will most likely change as a response of an event. Simulate the events and make sure that the component responds properly to them.

Validate that the handler functions were called and correct arguments were passed. Check if internal state was properly set.

### Test Edge Cases

### Test Edge Cases [#](https://alexkondov.com/tao-of-react/#test-edge-cases)

When you have the basic tests covered, make sure you add some to handle edge cases.

That would mean passing an empty array to make sure you’re not accessing an index without checking. Throw an error in an API call to make sure the component handles it.

### Write Integration Tests [#](https://alexkondov.com/tao-of-react/#write-integration-tests)

Integration tests are meant to validate an entire page or a larger component. It tests whether it works well as an abstraction. They give us the most confident that the application works as expected.

The components on their own could be working well and their unit tests could be passing. The integration between them could have problems, though.

## Styling [#](https://alexkondov.com/tao-of-react/#styling)

### Use CSS-in-JS [#](https://alexkondov.com/tao-of-react/#use-css-in-js)

That’s a really controversial take which many people won’t agree with. I’d rather use a library like Styled Components or Emotion because it allows me to express everything about my component in JavaScript. One less file to maintain. No CSS conventions to think about.

The logical unit in React is the component so in terms of separation of concerns it should own everything related to it.

_Note: There is no wrong option when it comes to styles - SCSS, CSS modules, libraries like Tailwind. CSS-in-JS is just the approach I would recommend._

### Keep Styled Components Together [#](https://alexkondov.com/tao-of-react/#keep-styled-components-together)

When it comes to CSS-in-JS components it’s normal to have multiple ones in the same file. Ideally we’d like to keep them in the same file as the regular component that uses them.

However, if they become too lengthy, as styles can get, extract them in their own file living next to the component that uses them. I’ve seen this pattern used in open source projects like Spectrum.

## Data Fetching [#](https://alexkondov.com/tao-of-react/#data-fetching)

### Use a Data Fetching Library [#](https://alexkondov.com/tao-of-react/#use-a-data-fetching-library)

React doesn’t come with an opinionated way of fetching or updating data from an API. Each team creates their own implementation usually involving a service that holds async functions which communicate with the API.

Going that route means that we need to manage loading states and handle http errors on our own. That leads to verbose code with a lot of boilerplate.

Instead of doing that we should use libraries like [React Query](https://react-query.tanstack.com/) or [SWR](https://swr.vercel.app/). They make communicating with a server a natural part of the component lifecycle in an idiomatic way - a hook.

They come with caching built in and manage loading and error states for us. We just need to handle them. Also, they remove the need to use a state management library to handle that data.
