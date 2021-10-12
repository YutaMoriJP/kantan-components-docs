---
sidebar_position: 1
---

# Getting Started

Start your React project with toolchains like [`Create-React-App`](https://create-react-app.dev/), [`NextJS`](https://nextjs.org/docs/), or [`GatsbyJS`](https://www.gatsbyjs.com/docs/tutorial/part-0/). Or use a bundler like [`Parcel`](https://parceljs.org/recipes/react/) and install `react` and `react-dom` yourself. Learn more from the [official docs](https://reactjs.org/docs/create-a-new-react-app.html).

```shell
npx create-react-app my-project && cd my-project
```

## Installation

Once you have your React project started, install the `kantan-components` package by using the command:

```shell
npm install kantan-components
```

Or do it with yarn:

```shell
yarn add kantan-components
```

After installing the package, simply import the Component that you want to use for your project.

### Example

```jsx
import { Message } from "kantan-components";
import { useState } from "react";

const App = () => {
  const [open, setOpen] = useState(false);
  return (
    <>
      <button onClick={() => setOpen(true)}>open message</button>
      {open ? (
        <Message onClose={() => setOpen(false)} ms={2000}>
          SUCCESS!
        </Message>
      ) : null}
    </>
  );
};
```
