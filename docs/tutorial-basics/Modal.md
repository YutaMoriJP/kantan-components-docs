# Modal

The `Modal` component helps you to intergrate a Modal UI to your app. For it to work, you must manage a `boolean` state that conditionally renders the component. It could look like `{open ? <Modal>HI</Modal> : null}`. You could also use a `Logical AND` operator, but you might want to read [this](https://kentcdodds.com/blog/use-ternaries-rather-than-and-and-in-jsx) on why a ternary might be a better option.

## The Syntax

```jsx
const [open, setOpen] = useState(false);
return (
  <div>
    {open ? (
      <Modal handleClose={onClose}>
        <h1>Hello, World!</h1>
      </Modal>
    ) : null}
  </div>
);
```

### Props

| Prop             | Type                          | Explanation                                                                                               |
| ---------------- | ----------------------------- | --------------------------------------------------------------------------------------------------------- |
| `handleClose`    | `Function`                    | The state update function that must unmount the `Modal` component, i.e. set the `boolean` state to false. |
| `children`       | `String` or `React.ReactNode` | The modal content, which is up to your creativity.                                                        |
| optional `color` | `String`                      | This is an optional prop that you can pass to control the background color of your Modal.                 |

### Example 1

The first example illustrates how you could approach rendering a Modal for your app. An user action like a click even can update the `open` state to true, and render `Modal` as a result. It can be for things like `Learn more` that gives users more information on certain things.

[CodeSandbox](https://f0524.csb.app/modal)

```jsx title/App.js
import { useState } from 'react'
import { Modal } from 'kantan-components'

const App = () => {
  const [open, setOpen] = useState(false);
  const onOpen = () => setOpen(true);
  const onClose = () => setOpen(false);
  return (
    <>
      <button onClick={onOpen}>Open Modal</button>
      {open ? (
        <Modal handleClose={onClose} color="rgb(204, 204, 204)">
         {/* apply custom style here*/}
          <article>
            <h1>Welcome to Kantan-Component</h1>
            <p>
              You might to want to install the `useToggle` hook from the
              `kantan-hooks` library to manage your boolean state.
            </p>
          </article>
        </Modal>
      ) : null}
    </>
  );
};
};
```

### Example 2

For this example, we will use the `useToggle` hook from `kantan-hooks` to more easily manage the `boolean` state.

Unlike the first example, the Modal is rendered upon page load, or more specifically, when `App` has mounted, and the `useEffect` callback runs. You might have seen something like this on websites that ask you to subscribe to their news letter.

[CodeSandbox](https://f0524.csb.app/modal)

```jsx
import { useState, useEffect } from "react";
import { useToggle } from "kantan-hooks";
import { Modal } from "kantan-components";

const App = () => {
  const { open, onOpen, onClose } = useToggle(false);

  useEffect(() => {
    onOpen();
  }, [onOpen]);
  return (
    <>
      {open ? (
        <Modal handleClose={onClose} color="rgb(204, 204, 204)">
          {/* apply custom style here*/}
          {/*Note that the color prop and the background color of your own CSS should match*/}
          <article className="box-space">
            <h1>Newsletter</h1>
            <p>Please consider subscribing to our newsletter.</p>
            {/* component allowing email subscription*/}
            <EmailSubscription />
          </article>
        </Modal>
      ) : null}
    </>
  );
};
```
