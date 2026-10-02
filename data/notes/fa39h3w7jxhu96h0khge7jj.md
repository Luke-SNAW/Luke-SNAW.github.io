
https://www.freecodecamp.org/news/react-interview-questions-to-know/

# What is the difference between state and props?

- States are **values we can read and update** in our React components.
- Props are values that are **passed to React components and are read only** (they should not be updated).

# What are React Fragments used for?

The fragment syntax looks like an empty set of tags <></> or are tags labeled React.Fragment.

# Why do we need keys for React lists?

React takes care of all of the business of updating the DOM for us (using a virtual DOM), but keys are necessary for React to update it properly.

# What are the useCallback & useMemo hooks used for?

`useCallback` is to prevent functions that are declared within the body of function components from being recreated on every render.

This can lead to unnecessary performance issues, especially for callback functions that are passed down to child components.
