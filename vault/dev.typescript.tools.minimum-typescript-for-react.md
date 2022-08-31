---
id: j45wy3zvrlupjtlj8tfw2z9
title: The minimum TypeScript you need for React
desc: ""
updated: 1661900962551
created: 1661900707615
---

> https://ente.io/blog/tech/typescript-for-react/

# Add property

```ts
import React from "react";

const Hello: React.FC<{ name: string }> = ({ name }) => {
  return <div>{`Hello, ${name}!`}</div>;
};
```

# Use interface

```ts
import React from "react";

interface HelloProps {
  name: string;
}

const Hello: React.FC<HelloProps> = ({ name }) => {
  return <div>{`Hello, ${name}!`}</div>;
};
```

# Add children

```ts
import React, { PropsWithChildren } from "react";

interface HelloProps {
  name: string;
}

const Hello: React.FC<PropsWithChildren<HelloProps>> = ({ name, children }) => {
  return (
    <div>
      <div>{`Hello, ${name}!`}</div>
      {children}
    </div>
  );
};
```

# Add rest

```ts
import React, { HTMLAttributes, PropsWithChildren } from "react";

interface HelloProps extends HTMLAttributes<HTMLDivElement> {
  name: string;
}

const Hello: React.FC<PropsWithChildren<HelloProps>> = ({
  name,
  children,
  ...rest
}) => {
  return (
    <div>
      <div {...rest}>{`Hello, ${name}!`}</div>
      {children}
    </div>
  );
};
```
